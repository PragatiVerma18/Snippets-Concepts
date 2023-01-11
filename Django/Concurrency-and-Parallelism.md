## Concurrency in Python

- An effective definition for concurrency is "being able to perform multiple tasks at once".
- The tasks may or may not actually be performed at exactly the same time.
- Instead, a process might start, then once it's waiting on a specific instruction to finish, switch to a new task, only to come back once it's no longer waiting. 
- Once one task is finished, it switches again to an unfinished task until they have all been performed. 
- Tasks start asynchronously, get performed asynchronously, and then finish asynchronously.

- **Concurrency is great for I/O-intensive processes -- tasks that involve waiting on web requests or file read/write operations.**

### Thread

- A thread is a way of allowing your computer to break up a single process/program into many lightweight pieces that execute in parallel. 
- Python's standard implementation of threading limits threads to only being able to execute one at a time due to something called the **Global Interpreter Lock (GIL)**.
- The GIL is necessary because CPython's (Python's default implementation) memory management is not thread-safe. 
- Because of this limitation, threading in Python is concurrent, but not parallel.

- To get around this, Python has a separate multiprocessing module not limited by the GIL that spins up separate processes, enabling parallel execution of your code.

### Drawbacks of threading
- Multi-threaded programs are more complicated, and typically more error prone, they include common troublesome issues: race-conditions, dead-locks, live-locks, and resource-starvation.

- aiohttp 
  - This will allow us to make non-blocking requests and receive responses using the async/await syntax.
  - It also has the extra benefit of a function that converts a JSON response without needing to import the json library. 

## Event Loop
- Event loops are constructs inherent to asynchronous programming that allow performing tasks asynchronously.
- In its purest essence, an event loop is a process that waits around for triggers and then performs specific (programmed) actions once those triggers are met. 
- They often return a "promise" (JavaScript syntax) or "future" (Python syntax) of some sort to denote that a task has been added. 
- Once the task is finished, the promise or future returns a value passed back from the called function (assuming the function does return a value).
- The idea of performing a function in response to another function is called a "callback."

Threading in Python allows asynchronicity, but our program could theoretically skip around different threads that may not yet be ready, wasting time if there are threads ready to continue running.

### So when should I use threading, and when should I use asyncio?
When you're writing new code, use asyncio. If you need to interface with older libraries or those that don't support asyncio, you might be better off with threading.

## Asyncio
- **CPU Context switching**: asyncio is asynchronous and uses an event loop; it allows you to have application controlled context switches while waiting for I/O. No CPU switching found here!
- **Race Conditions**: Because asyncio only runs a single coroutine at a time and switches only at points you define, your code is safe from race conditions.
- **Dead-Locks/Live-Locks**: Since you don’t have to worry about race conditions, you don’t have to use locks at all. This makes you pretty safe from dead-locks. You could still get into a dead-lock situation if you require two coroutines to wake each other, but that is so rare you would almost have to try to make it happen.
- **Resource Starvation**: Because coroutines are all run on a single thread, and dont require extra sockets or memory, it would be a lot harder to run out of resources. Asyncio however does have an “executor pool” which is essentially a thread pool. If you were to run too many things in an executor pool, you could still run out of resources. However, using too many executors is an anti-pattern, and not something you would probably do very often.

### Drawbacks of Asyncio
- When you go fully asynchronous, it means your entire codebase has to be asynchronous.
- This is because synchronous functions might take up too much time, thereby blocking your event loop.

## Parallelism
- Parallelism is a subset of concurrency: whereas a concurrent process performs multiple tasks at the same time whether they're being diverted total attention or not, a parallel process is physically performing multiple tasks all at the same time.
- the major benefit of multiprocessing happens when you perform multiple cpu-heavy tasks

- threading allows your applications to focus on new tasks while others are waiting. In this case, we're never sitting idly by. 
- Multiprocessing, on the other hand, spins up totally new services, usually on separate CPU cores, ready to do whatever you ask it completely in tandem with whatever else your script is doing.

## Recap: When to use multiprocessing vs asyncio or threading
- Use multiprocessing when you need to do many heavy calculations and you can split them up.
- Use asyncio or threading when you're performing I/O operations -- communicating with external resources or reading/writing from/to files.
- Multiprocessing and asyncio can be used together, but a good rule of thumb is to fork a process before you thread/use asyncio instead of the other way around -- threads are relatively cheap compared to processes.

---
## References - 
- https://testdriven.io/blog/concurrency-parallelism-asyncio/
- https://testdriven.io/blog/python-concurrency-parallelism/
