# Writing Loosely Coupled Code

## CUPID (Dan North)

### Composable

"Prefer composition over inheritance"

Lots of little pieces working together for a requirement.

"Plays well with others"

Emphasize encapsulation
    - The WHAT something does is way more important than how it does it.


Design of your programmatic interface (the description of what it does) is the primary thing, 
the implementation is important but secondary.

### Unix Philosophy
- Small focused bits of functionality.
- Better to have a bunch of small tools that can work together than one big one that everything.

### Predictable
Follows the "principle of least suprise" - does what you think it will do.
(Expresses Intent)


### Idiomatic
"feels natural"

use the language and "idioms" and conventions of that language.
but also of your problem space. This is the "Ubiquitious Language" from Eric Evans "Domain Driven Design"


### Domain Based ("Business")

- Be skeptical when you are spending more time solving technical requirements than business requirements.
- Pick tools, frameworks, runtimes, etc. that take the technical requirements away from your ability to fulfill business requirements.





## Four Rules of Simple Design (Kent Beck, Martin Fowler)

[Linky](https://martinfowler.com/bliki/BeckDesignRules.html)

1. Passes all the Tests
2. Reveals intention - WAYYYY the most important thing. Duplicate a TON of stuff it makes the test more understandable.
    - "programming at the lowest common denominator"
    
3. No duplication
4. Fewest elements - the fewer decisions, variables, and loops you have it is less likely you will have bugs.



"Don't Repeat Yourself" (DRY)
- Didn't we already pay you to write that once?
- "If you have to change it, you have to change it multiple places"
    - multiple ways to do the same thing that change over time, which means you wil have an INCONSISTENT SYSTEM.



## SOLID (Distillation of stuff, 'codified' by Robert C. Martin)

### Single Responsibility Priciple (SRP)

"Code modules should have a single axis of change"
single == reason


## Open/Closed Principle

"Code modules should be open for extension but closed for modification"

Find ways to make it so you rarely have to change existing code, instead you have way to add new behavior and functionality by adding new stuff.

## Liskov Substitution Principle

"Derived types should be substituable for their base types"

Prefer composition over inheritance.

## Interface Segregation Principle

"Depend on small, client specific interfaces"


## Dependency Inversion Principle
- Depend on abstractions, not concretions.
- our bank account relies on a "what", not a "how" (the bonus calculation)

- "new is glue"
-  Depend on someone that can do the job description.