`2021-01-18, Async vs Sync - Concurrent vs Parallel`

# Async vs Sync - Concurrent vs Parallel

## Parallelism

_Parallelism_ is when tasks run at the exact same time, e.g., on a multicore processor where each task has a thread

- **Oracle**: A condition that arises when at least two threads are executing simultaneously.

## Concurrency

_Concurrency_ is when two or more tasks can start, run, _and_ complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. For example, multitasking on a single-core machine.

- **Oracle**: A more generalized form of parallelism were at least two threads are making progress via time-slicing (virtual parallelism).

## Asynchronism

The term _asynchronous_ refers to two or more objects or events not existing or happening at the same time (or multiple related things happening without waiting for the previous one to complete)

- _Asynchronous software design_ expands upon the concept by building code that allows a program to ask that a task be performed alongside the original task (or tasks), without stopping to wait for the task to complete.
- When the secondary task is completed, the original task is notified using an agreed-upon mechanism so that it knows the work is done, and that the result, if any, is available.
- When software communicates asynchronously, a program may make a request for information from another piece of software (such as a server), and continue to do other things while waiting for a reply.

## Synchronism

_Synchronous_ refers to real-time communication where each party receives (and if necessary, processes and replies to) messages instantly (or as near to instantly as possible).

- Many programming commands are also synchronous — for example when you type in a calculation, the environment will return the result to you instantly, unless you program it not to.
