# Test Doubles

## Feedback Loops Again (or, "Levels of Testing")

### Static Testing

That means you have things like a compiler. The compiler won't let you put code into production if it won't compile.

Warnings from the compiler - really try not to ship any code that has compiler warnings. 

(tools like "Linters" in TypeScript, JavaScript, etc.) are another set of "tests" at this level.

- Almost INSTANT. You spell something wrong, whatever, you get the red squigglies. Fix it.


### Unit Testing

Your unit tests should be designed to just be a *little bit* slower than the compiler itself.

For example if your unit tests suite takes more than say 5-10 seconds to run, it isn't a super helpful inner loop.


### Integration Testing

This is where you test databases, networks, file systems, all that stuff.
You automate the user (driver) of your application.

Often we *fake* the database, network, filesystem etc. for different scenarios.

These are slower. You won't run these as often. 


### End-to-End Tests (Outer loop)

The "real" tests - nothing is faked (other than the user usually).



## Why Do We use Them?

- Sometimes we have to write code against a system, service, library and it doesn't even exist yet. 

- We have to simulate stuff that could happen in production environments to make sure our coded responds to that properly.

    - SRE (Site reliability engineering).

    - "Simian Army" - "Chaos Monkey" 


### Modes of Using Test Doubles

- Dummies - almost don't even count. They don't have anything to do with testing. Which why we mostly use them when we are testing something that doesn't have anything to do with the code we are "doubling"

- Stubs - For "State based" testing (Beckian Testing) - your dependency is something you "ask" or  "query" things of and it changes your state based on the response.

- Mocks - For Interaction testing ("Mockist" or "London School") which is "tell, don't ask"

- Fakes - replace a real but expensive thing for testing purposes, like using a fake database or something. 
    - Only used in integration testing.