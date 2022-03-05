# Chapter 1: Clean Code

## There Will Be Code

Code is the language in which we ultimately express the requirements. Even though we can create langauges that are closer to those requirements (level of abstractions in coding languages will increase), there will never be a perfect machine that could eliminate the need of code.

> No machine can eliminate the need of code.

## Bad Code

We wade thorugh bad code. We struggle to find our way, hoping for some hint, some clue, of what is going on; but all we see is more senseless code.

We tend to write bad code when 

- we are in rush, 
- we have a lot of backlog items that needs to be done,
- we decide working mess is better than nothing, and we promise to clean it up later.

> Later equals never, so never write bad code.

## The Total Cost of Owning a Mess

Over the span of year or two, teams that were moving very fast at the beggining of a project can find themselves moving at a snail's pace. Every change they make to the code breaks two or three other parts of the code. No change is trivial. Every addition or modification to the system requires that the thangles, twists and knots to be "understood", which drives the productivity toward zero.

The management will then hire more people to increase the productivity but the new staff won't be able to understand the system. Eventually, the team will uprise and inform the management for a redesign, which is very costly and time consuming.

> The only way to make the deadline is to keep the code as clean as possible.

### What is Clean Code?

- *Pleasing to read (it should be readable just as a novel).*
- *Should contain only what is necessary. (minimal)*
- *Focused, each function, each class each module exposes a single responsibility.*
- *Should be enhancable by other developers.*
- *Should have tests.*
- *Should look like that the code has been taken care of to keep it simple and orderly.*
- *Should not have duplications, instead, should have abstractions.*
- *Each line of code should be pretty much what you expected (i.e the code should be obvious)*

> Leave the campground cleaner than you found it.

If we all checked-in our code a little cleaner than when we checked it out, the code
simply could not rot.
