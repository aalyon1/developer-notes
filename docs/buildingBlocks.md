# Building Blocks of Things in C#

## Generally "Objects"

Objects are things we can do stuff to. Objects have *affordances*.

BankAccount:

- Get the Balance `var currentBalance = account.GetBalance()` "Safe"
- Make a deposit `account.Deposit(1_000_000);` "Unsafe" 
- Make a withdrawal `account.Withdraw(800);` "Unsafe"

*Command-Query Responsibility Separation* - (CQRS)

```csharp
var myAccount = new BankAccount();

var myBalance = myAccount.GetBalance();

myBalance += 1_000_000; // my god this stupid!

Assert.Equal(myAccount.GetBalance(), myBalance);

var myCustomerName = myAccount.Customer.Name;

myAccount.Customer.Name = myCustomerName.ToUpper();

```


### Some Objects we Call "Entities"

These are objects that are in some way "specific". They are related to a real "thing".
That two instances of an entity are considered equal if they have the same identifier.

objects that are "tracked" by an Id. 

The behaviors on an entity are ALL ABOUT the thing identified by that entity.



```csharp

var myAccount = AccountLookupService.GetAccountFor("9398938983");

myAccount.Deposit(15.23M);


```

### Some Objects we Call "Values"

An object that is compared to other objects based on their "value".

If you have two instances of the same date, does it matter which one you have?

"DTOs" "Data Transfer Objects" are a name sometimes used for "Values"

Records are really great for expressing that an object is a DTO, or not an entity, etc.

Just "here is the receipt"





### Some Objects we Call "Services"