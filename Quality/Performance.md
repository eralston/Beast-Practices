# Performance
Performance standards aim to enforce best practices to achieve highly responsive functionality, mainly in the context of web applications. The goal is to minimize the time between user action (cause) and result (effect) and maintain an illusion of immediacy despite the application being composed of several different, distant computers.

Each layer of the software stack must be considered, from the browser/client, to the web server, the database, hosting, and everything in between.

This document is concerned purely with the performance of the running application without concern for other areas such as security, design patterns or build/compile speed. It is up to the software design process to decide how to balance performance against other concerns. There is no objective standard, there is an asymptotic ideal of instant performance, but the best we can do is approach zero.

## Resources
---
[Martin Fowler: Yet Another Optimization Article](https://www.martinfowler.com/ieeeSoftware/yetOptimization.pdf)
[MSDN: Asynchronous programming](https://docs.microsoft.com/en-us/dotnet/csharp/async)
[MDN: Asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
[Premature Optimization](http://wiki.c2.com/?PrematureOptimization)
[Index Tuning Week: How Many Indexes Are Too Many?](https://www.brentozar.com/archive/2018/10/index-tuning-week-how-many-indexes-are-too-many/)

## Principles
---
### Architecture

The earliest stage to consider performance is in planning the software architecture. Consider the following questions either when making architectural decisions or when evaluating current architecture.

### Scalability

Is the architecture scalable? Are there any technical limitations that may be encountered when scaling out the application? The architecture should be considered for its capability for horizontal scaling -- scaling by adding more computers or services in parallel -- or vertical scaling -- adding more resources to a single computer or service.

### Modularity

Is the architecture modular? Does it allow for the project to designed as a set of discrete, loosely coupled components? Having a modular design makes it easier to isolate and analyze performance issues.

### Appropriate optimizations

When choosing an area to optimize, the impact of the optimization should be considered and evaluated. Is this a critical region of the code?  Optimizing code that is not frequently run is usually not a candidate for optimization. For example, with CRUD applications, the most critical operation is typically read, as this is far more common than the other operations.

### Effective optimizations

Consider the effectiveness of an optimization, either for new optimizations or for evaluating existing ones. Is the code readable and not overly clever? Clear, readable code is easier to analyze for performance impact, and there is usually little benefit to no benefit, either to readability or performance, to utilize minute syntactical tricks.

### Performance Logging and Notification

Does the project utilize performance logging along with notification of performance degradation events in its deployed state? Especially with web applications with highly variable workloads, it's important to recognize performance issues can be addressed quickly.

## Asynchronous Programming
---
**Is everything asynchronous that should be?** Any remote procedure call or I/O operation such as network calls, file operations, database queries, etc., should be handled asynchronously wherever possible. This means the main thread, either a UI thread for a GUI application or any thread in a web application, is free to continue working while awaiting the response of the call.

**Can asynchronous operations be reduced?** Remote operations are basically always slower, and reducing them generally improves responsiveness. There are a variety of ways of reducing them

**Can consecutive asynchronous calls run concurrently?** If you need to make multiple asynchronous calls, can they be started and awaited simultaneously? Rather than awaiting one call, then the next, and so on. For example, in TypeScript use Promise.all, in C# use Task.WhenAll wherever possible.

**Can multiple asynchronous calls be combined?** If an async call is using an API you control, can you instead create a single API call to aggregate multiple calls together into a single payload?

**Are results cached appropriately?** If data received from async calls can be cached and reused, instead of calling the API every time the data is needed, then do so.

**Are connections minimized through pooling?** For any resource that depends on a connection which can be maintained, the connection should be reused if possible to avoid opening/closing the connection redundantly which can be expensive. For example, a connection to a database should be maintained for at least the duration of a web request, or on a web page a web socket connection should be maintained until the page closes or until a timeout is reached.

**Can async calls be deferred?** Avoid making async calls prematurely, especially if they may impact performance. Especially startup calls defer until necessary, which may avoid some calls entirely in some cases.

**Is extraneous/debug logging removed or disabled?** Logging can result in potentially expensive I/O operations and should be removed or disabled for production code.

## General Programming
---
**Are loops/enumerations/iterations as shallow and tight as possible?** These can easily grow as the application scales and datasets grow. Redundant iterations should be eliminated if possible. Loops should break if they don't need to continue before reaching their end. Datasets should be filtered before they're accessed (more on this later).

**Are recursive functions predictably shallow?** With imperative languages like C# and JavaScript, there's no optimization for recursion so it is possible to reach the maximum call stack size. It's preferable to refactor recursive algorithms to instead use loops where possible.

**Are reference types always used for data structures?** Data structures are typically more efficient when used with reference types (classes, objects), as they avoid performance penalties involved with a copy by value and boxing (moving from stack to heap). So, value-based data structures (mainly C# structs) should generally be avoided when multiple data members are intended to be stored. (structs like DateTime are a good example of struct usage, the struct is essentially wrapping a single primary value with a variety of methods).

**Are resources safe for concurrent access?** Ensure that resources that might be used by multiple threads are thread-safe. Particularly for caches, ensure the cache itself as well as the cached items are thread-safe. In C# read/get operations on classes are generally thread-safe, but setting data isn't without be specifically concurrent.

## Server and Database Programming
---
**Are long-running processes avoided?** Web servers tend to kill long-running threads, so long-running operations should generally be avoided.

**Are database indexes used appropriately?** Indexing certain database columns, especially those which are commonly used to filter a table, can speed up database reads. However, the faster reads come at the cost of the slower insert and delete operations, so they should be avoided for commonly changed columns.

**Are database queries paging and filtering data appropriately?** Avoid loading unnecessary data by handling paging and filtering operations on both the server and the database. This is generally the fastest method, such as in cases of loading a single page of a large database table, but there may be rare cases where loading the data set first and then filtering after is more performant.

**For efficient ORM usage:**

**Are database queries cachable?** ORM's often convert code into database queries. Often this conversion is expensive, but the results are cachable. However, dynamic code for ORM queries can miss the cache, incurring a performance penalty. Generally, ORM query code that remains static (additional filter/page method calls aren't added conditionally/dynamic), but that vary based on parameters, will reliably utilize the cache.

**Is object tracking only used when necessary?** ORM's often introduce some performance overhead by tracking changes to entities upon load, which significantly slows down database reads. So, when object tracking is not necessary (such as for simple gets/reads), it should be disabled (for example: EF AsNoTracking method).

## Front-end/browser Programming
---
**Is UI manipulation appropriately minimized?** UI rendering is expensive, and it's very easy to add additional animations and tweaks which compound on each other and eventually reduce UI responsiveness, so UI manipulation should be reduced as much as possible (including browser DOM manipulation).

**Are remote assets appropriately small?** Remote assets such as browser scripts and style sheets should be minimized through methods such as dead code reduction, tree-shaking, code-splitting, minification, etc. These separate assets can then be downloaded many at a time, often up to 6 at a time using HTTP/2.

**Is DOM access efficient?** DOM accessing functions vary considerably in performance; generally, narrowly scoped functions work much quicker than broader query-centric ones. In other words, the getElement(s)By* functions work much quicker than querySelector, which sometimes works faster than jQuery.

## Production Server Environment
---
**Are application service resources appropriate?** The application runtime environment, typically a web server running on some virtual machine, should have appropriate resources assigned to it such as number and speed of processor cores and amount of memory. As mentioned previously this covers vertical scaling.

**Are database resources appropriate?** Databases should be configured appropriately for their expected load, such as adequate storage for large datasets, appropriate compute resources from heavy writing, etc.