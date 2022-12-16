# Microsoft Visual Studio Gifting Solution API

Program Main
```cs
using GiftingApi.Adapters;
using GiftingApi.Domain;
using GiftingAPI.Adapters;
using GiftingAPI.Domain;
using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

builder.Services.AddTransient<ICatalogPeople, EfPeopleCatalog>();

builder.Services.AddDbContext<GiftingDataContext>(options =>
{
    options.UseSqlServer(builder.Configuration.GetConnectionString("gifts"));
});

builder.Services.AddHttpClient<OnCallLookupApiAdapter>(client =>
{
    client.BaseAddress = new Uri(builder.Configuration.GetValue<string>("developer-api"));
});

//Example of CORS
builder.Services.AddCors(builder =>
{
    builder.AddDefaultPolicy(pol =>
    {   // "Promiscuous Mode"
        pol.AllowAnyHeader();
        pol.AllowAnyOrigin();
        pol.AllowAnyMethod();
    });
});

var app = builder.Build();
app.UseCors();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseAuthorization();

app.MapControllers();

app.Run();

```

People Controller
```cs
using GiftingAPI.Domain;
using GiftingAPI.Models;

namespace GiftingApi.Controllers;

[ApiController]
public class PeopleController : ControllerBase
{

    private readonly ICatalogPeople _personCatalog;
    private readonly ILogger<PeopleController> _logger;

    public PeopleController(ICatalogPeople personCatalog)
    {
        _personCatalog = personCatalog;
    }

    [HttpGet("/people/{id:int}")]
    public async Task<ActionResult<PersonItemResponse?>> GetPersonById(int id)
    {
        PersonItemResponse response = await _personCatalog.GetPersonByIdAsync(id);
        if (response is null)
        {
            return NotFound();
        }
        else
        {
            return Ok(response);
        }
    }

    [HttpPost("/people")]

    public async Task<ActionResult<PersonItemResponse>> AddPerson([FromBody] PersonCreateRequest request)
    {
        // Validate request
        // If valid add to database send 201, if not send 400 (bad rewquest)

        PersonItemResponse response = await _personCatalog.AddPersonAsync(request);
        return StatusCode(201, response);
    }

    // GET /people
    [HttpGet("/people")]
    public async Task<ActionResult<PersonResponse>> GetAllPeople(CancellationToken token)
    {
        _logger.LogInformation("Get a request to get somse people... ");
        await Task.Delay(3000);
        PersonResponse response = await _personCatalog.GetPeopleAsync(token);
        _logger.LogInformation($"Got some people from the DB {response.Data.Count} persons ");
        return Ok(response);
    }
}

```
ICatalogPeople Domain
```cs
using GiftingAPI.Models;

namespace GiftingAPI.Domain
{
    public interface ICatalogPeople
    {
        public Task<PersonItemResponse> AddPersonAsync(PersonCreateRequest request);

        public Task<PersonResponse> GetPeopleAsync(CancellationToken token);
        public Task<PersonItemResponse?> GetPersonByIdAsync(int id);
    }
}

```
Gifting Data Context Adapter
```cs
using GiftingApi.Domain;
using Microsoft.EntityFrameworkCore;
namespace GiftingAPI.Adapters;

public class GiftingDataContext : DbContext
{
    public GiftingDataContext(DbContextOptions<GiftingDataContext> options): base(options)
    {

    }
    public DbSet<PersonEntity> People { get; set; } = null;

}

```
People Model
```cs
using System.ComponentModel.DataAnnotations;

namespace GiftingAPI.Models;

public record PersonItemResponse(string Id, string FirstName, string LastName);

public record PersonResponse(List<PersonItemResponse> Data);

public record PersonCreateRequest : IValidatableObject
{
    [Required, MaxLength(100)]
    public string FirstName { get; init; } = string.Empty;

    [Required, MaxLength(100)]
    public string LastName { get; init; } = string.Empty;

    public IEnumerable<ValidationResult> Validate(ValidationContext validationContext)
    {
        if (FirstName.Trim().ToUpperInvariant() == "DARTH" && LastName.Trim().ToUpperInvariant() == "VADER")
        {
            yield return new ValidationResult("We have a strict no Sith policy", new string[] { nameof(FirstName), nameof(LastName) });
        }
    }
}
```