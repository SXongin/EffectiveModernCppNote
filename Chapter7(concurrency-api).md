# The Concurrency API

## item 35 Prefer task-based programming to thread-based

- The std::thread API offers no direct way to get return values from asynchronously run functions, and if those functions throw, the program is terminated.
- Thread-based programming calls for manual management of thread exhaustion, oversubscription, load balancing, and adaptation to new platforms.
- Task-based programming via std::async with default launch policy handles most of these issues for you.

## item 36 Specify std::launch::async if asynchronicity is essential

- The default launch policy for std::async permits both asynchronous and synchronous task execution.
- This flexibility leads to uncertainty when assessing thread_locals, implies that the task may never execute, and affects program logic for timeout-based wait calls.
- Specify std::launch::async if asynchronous task execution is essential.

## item 37 Make std::threads unjoinable on all paths

- Make std::threads unjoinable on all paths.
- join-on-destruction can lead to difficult-to-debug performance anomalies.
- detach-on-destruction can lead to difficult-to-debug undefined behavior.
- Declare std::thread objects last in lists of data members.

## item 38 Be aware of varying thread handle destructor behavior

- Future destructors normally just destroy the future's data members.
- The final future referring to a shared state for a non-deferred task launched bia std::async blocks until the task completes.

## item 39 Consider void futures for one-shot event communication

- For simple event communication, condvar-based designs require a superfluous mutex, impose constraints on the relative progress of detecting and reacting tasks, and require reacting tasks to verify that the event has taken place.
- Designs employing a flag avoid those problems, but are based on polling, not blocking.
- A condvar and flag can be used together, but the resulting communications mechanism is some what stilted.
- Using std::promises and futures dodge these issues, but the approach uses heap memory for shared states, and it's limited to one-shot communication.

## item 40 Use std::atomic for concurrency, volatile for special memory

- std::atomic is for data accessed from multiple threads without mutexes. It's a tool for writing concurrent software.
- volatile is for memory where reads and writes should not be optimized away. It's a tool for working with special memory.
