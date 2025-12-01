# Chapter 1: Reliable, Scalable, and Maintainable Applications

This chapter introduces fundamental terminolgy and concepts to shape our frame of thinking when designing data systems. There are many types of data systems - databases, caches, search indexes, stream processing, batch processing, etc.

While they all serve their own purposes, the lines are more blurred than we think, with services having broad requirements, requiring more than one tool. One example is having a cache and primary DB at the same time.

When it comes to designing a data system, there are 3 overarching factors: reliability, scalability, and maintainability.

## Reliability
The system should function **correctly** even in the face of **adversity**.

Reliability is about "continuing to work correctly, even when things go wrong," i.e. fault-resilient. A fault is a a single component deviation, while a failure is a full system stop.

Sometimes, we want to handle the faults. Sometimes, we want to trigger more faults, to highlight major problems (e.g. compromised security).

- Hardware faults
    - In a data center with tens of thousands of drives, we can expect at least one drive to die per day.
- Software faults
    - Usually unpredictable faults. Best resolved through good practices, monitoring, and thorough testing.
    - Make sure to have good rollbacks processes in place.
- Human faults
    - A person provdies a wrong input -> the API/interface is too easy to do the wrong thing.
    - Decouple common human error points. Use a non-production sandbox to test these stress points.
    - Utilize unit tests, integration tests, and manual tests.


## Scalability
The system should be able to **grow** to handle increased loads/users.

A *load* is described with a few numbers called *load parameters*. A load parameter is a specific measure related to our service: requests per second, ratio of reads/writes, cache hit rate, and so on.

Performance is about describing the changes to the service in relation to the load parameter:
- When a load parameter is increased to keep the system sources unchanged, how does the system performance change?
- When a load paramter is increased, how much increase do resources need to keep the performance the same?

We want to see how performance is for a lot of people for many situations, so we use a distribution to describe performance.

An average would not explain outliers well, so percentiles (p50, p90, p99) are used. Higher percentiles are called **tail latencies**.

Tail latency amplification: High percentiles are important for backend services with multiple calls as a part of serving a single end-user request. Even if a small number have high latency, with multiple calls, the overall service slows down.

Vertical vs horizontal scaling
- Scaling up (vertical scaling): Moving to a more powerful machine.
- Scaling out (horizontal scaling): Distributing load across multiple machines.

Elastic vs Manual
- Elastic: Services can automatically add or remove resources.
- Manual: Must be done by hand.

**Latency** is the duration of a request waiting to be handled, while **response time** is what a client sees.

## Maintainability
The engineers should be able to **maintain** the current behavior and **adapt** the system to new use cases productively.

- Operability: Make it easy for teams to keep the system running.
    - Should monitor the system health and be easy to trace problems.
    - Good visibility, automation, and documentation.
- Simplicity: Easy to onboard.
    - Opposite of big ball of mud. Best to avoid accidental complexity.
- Evolvability: Easy to change to system in the future.
    - IMO, this is part of the first two.

