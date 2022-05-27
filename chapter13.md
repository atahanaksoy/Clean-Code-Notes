# Chapter 13: Concurrency

## Why Concurrency?

Concurrency helps us decouple *what* gets done from *when* it gets done.

However:

- Concurrency incurs some overhead, both in performance as well as writing additional code.
- Correct concurrency is complex, even for simple problems.
- Concurrency bugs aren't usually repeatable, so they are often ignored as one-offs instead of the true defects they are.
- Concurrency often requires a fundamental change in design strategy.

## Concurrency Defense Principles

### Single Responsibility Principle

The SRP states that a given method/class/component should have a single reason to change. However:

- Concurrency related code has its own life cycle of development, change and tuning.
- Concurrency related code has its own challenges, which are different from noncurrent code.

> **Keep your concurrency-related code separate from other code.**

### Corollary: Limit the Scope of Data

> Take data encapsulation to heart; severely limit the access of any data that may be shared.

### Corollary: Use Copies of Data

- If there is an easy way to avoid sharing objects, the resulting code will be far less likely to cause problems. Therefore, use read-only copies (if possible)

### Corollary: Threads Should Be as Independent as Possible

- Each thread should exist in its own world, sharing no data with any other thread. This removes the synchronization requirements.

## Know your Execution Models

| Bound Resources  |                                                 Resources of a fixed size or number used in a concurrent environment. (database connections,read/write buffers)                                                 |
| ---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Mutual Exclusion |                                                                                     Only one thread can access shared data                                                                                      |
| Starvation       | One thread or a group of threads is prohibited from proceeding for an excessively long time or forever. For example, always letting fast running threads through first could starve out longer running threads. |
| Deadlock         |                                                Two or more threads waiting for each other to finish. Each thread has a resource that the other thread requires.                                                 |
| Livelock         |             Threads in lockstep, each trying to do work but finding another "in the way". Due to resonance, threads continue trying to make progress but are unable to for an excessively long time             |


## Testing Threaded Code

> Write tests that have the potential to expose probvlems and then run them frequently, with different programmatic configurations, system configurations and load.

- Treat spurious failures as candidate threading issues. Do not ignore system failures as one-offs.
- Get your nonthreaded code working first.
- Make your threaded code pluggable. Write the concurrency supporting code such that it can be run in several configurations: One thread, several threads, varied as it executes.
- Make your threaded code tunable. Early on, find ways to time the performance of your system under different configurations.
- Run with more threads than processors. The more frequently your tasks swap, the more likely you'll encounter code that is missing a critical section or causes deadlock.
- Run on different platforms.
- Try to force failures


