---
ms.custom:
  - build-2023
---
The optimizer in SQL Server in some cases runs pieces of the query plan called *operators* using parallelism with multiple concurrent threads. The number of threads used for a query plan operator is called *Degree of Parallelism* (DOP).

The Degree of Parallelism that a query is executed with can greatly affect its performance. When a query uses parallelism, there's always the question of whether it's using the right amount of parallelism. Sometimes, if the DOP is too high, it can introduce inefficiencies into the query execution. If the DOP is too low, you might miss some of the increase speed that parallelism can provide.  

SQL Server can control the maximum number of threads per operator using server, database, resource governor, or query settings called *max Degree of Parallelism* (MAXDOP). Setting the right MAXDOP for a SQL Server deployment can be complex and sometimes difficult.

## DOP enhancements in SQL Server 2022

SQL Server 2022 introduces a new feature called *DOP feedback*. The optimizer uses DOP feedback to find the parallel efficiency for a query. Parallel efficiency is the minimum DOP for a query that can result in the same overall query duration, factoring our common waits. This feature looks at any parallel query and determine if it might perform better with a lower Degree of Parallelism than currently being used. Reducing the DOP for a query can provide more threads and CPU resources for other queries of the application.  

DOP feedback never increases the DOP. At best, DOP feedback reverts to a stable previous DOP, and it works incrementally. Instead of trying to drastically lower the DOP all at once, DOP feedback tries a slightly lower DOP. If the DOP is good, it might try another slightly lower DOP. If the new, even lower DOP is good, DOP feedback might try to reduce again down to the DOP of two. It won't make a parallel plan become serial. If the new, lower DOP isn't as good, it goes back to the previous known good DOP and keep the query at that level.

:::image type="content" source="../media/degree-of-parallelism-feedback-step.png" alt-text="Diagram showing that DOP feedback reduces the Degree of Parallelism in a stepwise fashion, incrementally decreasing the Degree of Parallelism and verifying at each step.":::

## DOP feedback example

A query is compiled with a Degree of Parallelism of 8. If DOP feedback detects a fair amount of wait times between threads and CPU overhead, it suggests a lower DOP, such as DOP of 6. On the next execution, the query executes with a DOP of 6. If the performance is better over the next several executions, the DOP of 6 is considered stabilized.

However, DOP feedback might then determine that there are still too many waits and further attempt a DOP of 4. Again, several executions are used to verify the feedback. DOP feedback might then try a DOP of 2. If after several executions the DOP 2, performance isn't determined to be better, the system returns to suggesting a DOP of 4 as the most recent, stable, and verified DOP.

## DOP feedback architecture

:::image type="content" source="../media/degree-of-parallelism-feedback-architecture.png" alt-text="A diagram of Degree of Parallelism feedback architecture.":::

DOP feedback requires the Query Store to be enabled, database compatibility level 160, and a database setting called `DOP_FEEDBACK` to be enabled. With these settings, the optimizer works in coordination with Query Store background tasks to look for repetitive and long-running queries that could benefit from a lower DOP.

A feedback cycle validates an adjusted query duration, factoring out waits, doesn't regress with a lower DOP value, and that lower overall CPU is observed for the query. After a period of validation, a lower DOP is considered stabilized and is persisted in the Query Store. The optimizer continues to validate lower DOP values in a stepwise down fashion to find the best parallel efficiency or a minimum DOP, which is 2.

DOP feedback never increases DOP. It honors the MAXDOP setting for a query depending on server, database, resource governor, or query hint that has been applied.

## Simple setup and easy optimization with DOP feedback

With DOP feedback enabled, all of these steps are done without triggering query recompiles, and without user action.  

DOP feedback for SQL Server 2022 addresses a long-held challenge for our customers: finding the right Degree of Parallelism for each query without having to manually test and tweak each query for optimal performance.

For more information, see [Degrees of Parallelism (DOP) feedback](/sql/relational-databases/performance/intelligent-query-processing-feedback#degree-of-parallelism-dop-feedback).
