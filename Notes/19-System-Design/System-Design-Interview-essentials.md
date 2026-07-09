<div align="center">

# System Design Essentials

![SystemDesign](https://img.shields.io/badge/System%20Design-Architecture-orange?style=for-the-badge)
![Scalability](https://img.shields.io/badge/Scalability-Distributed%20Systems-blue?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to understand system design and answer interview questions with confidence**

</div>

---

## Table of Contents

1. [What is System Design](#what-is-system-design)
2. [Functional vs Non-Functional Requirements](#functional-vs-non-functional-requirements)
3. [Vertical vs Horizontal Scaling](#vertical-vs-horizontal-scaling)
4. [Load Balancing](#load-balancing)
5. [Caching](#caching)
6. [Content Delivery Networks](#content-delivery-networks)
7. [Database Scaling](#database-scaling)
8. [SQL vs NoSQL in System Design](#sql-vs-nosql-in-system-design)
9. [Database Replication](#database-replication)
10. [Sharding](#sharding)
11. [Consistent Hashing](#consistent-hashing)
12. [Message Queues](#message-queues)
13. [Microservices vs Monolith](#microservices-vs-monolith)
14. [API Gateway](#api-gateway)
15. [Rate Limiting](#rate-limiting)
16. [CAP Theorem](#cap-theorem)
17. [Consistency Models](#consistency-models)
18. [Availability and Redundancy](#availability-and-redundancy)
19. [Designing for Failure](#designing-for-failure)
20. [How to Approach a System Design Interview](#how-to-approach-a-system-design-interview)
21. [Common Interview Questions](#common-interview-questions-spoken-style-answers)
22. [Quick Cheat Sheet](#quick-cheat-sheet)

---

## What is System Design

System design is the process of planning the architecture of a software system, deciding how its components fit together to handle real world requirements like scale, speed, and reliability. It's less about writing code and more about making thoughtful trade-offs between competing priorities.

**Spoken answer:** I would describe system design as zooming out from writing individual functions and instead thinking about how an entire application is structured, how data flows through it, and how it behaves when thousands or millions of people use it at once. It's really a series of trade-off decisions rather than one single correct answer.

---

## Functional vs Non-Functional Requirements

**Spoken answer:** Functional requirements describe what the system should do, like letting a user post a photo or send a message. Non-functional requirements describe how well it should do it, things like how fast it responds, how many users it can handle at once, and how it behaves during a failure. In interviews, I always clarify both before jumping into a design, since non-functional requirements often shape the architecture more than the features themselves.

---

## Vertical vs Horizontal Scaling

| Vertical Scaling | Horizontal Scaling |
|---|---|
| Add more power to a single server | Add more servers |
| Simple, no code changes needed | Needs load balancing and distributed logic |
| Has a hard upper limit | Scales almost indefinitely |
| Single point of failure | More resilient, failure of one server is survivable |

**Spoken answer:** Vertical scaling means upgrading a single machine with more CPU or memory, which is simple but eventually hits a hardware ceiling. Horizontal scaling means adding more machines and distributing the load across them, which scales much further but adds complexity, since now the system needs to coordinate across multiple servers.

---

## Load Balancing

**Spoken answer:** A load balancer sits in front of multiple servers and distributes incoming traffic across them, so no single server gets overwhelmed. It also improves reliability, since if one server goes down, the load balancer simply stops sending traffic to it and routes requests to the remaining healthy servers instead. Common strategies include round robin, least connections, and routing based on server response time.

---

## Caching

**Spoken answer:** Caching stores a copy of frequently accessed data somewhere faster to reach than the original source, like keeping it in memory instead of querying a database every time. This reduces load on the database and speeds up response times significantly. The trade-off is that cached data can become stale, so I need a clear strategy for when and how the cache gets updated or invalidated.

| Caching Strategy | Description |
|---|---|
| Cache aside | App checks cache first, loads from database on a miss, then stores it in cache |
| Write through | Data is written to the cache and database at the same time |
| Write behind | Data is written to the cache first, then asynchronously saved to the database |
| TTL expiration | Cached data automatically expires after a set time |

---

## Content Delivery Networks

**Spoken answer:** A content delivery network, or CDN, stores copies of static content like images, videos, and JavaScript files on servers spread across different geographic locations. When a user requests that content, it's served from the location closest to them, which reduces latency significantly compared to always fetching it from one central server far away.

---

## Database Scaling

**Spoken answer:** As traffic grows, a single database server eventually cannot keep up with the volume of reads and writes. The common approaches are adding read replicas to handle more read traffic, caching frequently accessed queries, and eventually splitting the data itself across multiple servers through sharding if a single database can no longer hold or serve all the data efficiently.

---

## SQL vs NoSQL in System Design

| Factor | SQL | NoSQL |
|---|---|---|
| Schema | Fixed, structured | Flexible, dynamic |
| Relationships | Strong, uses joins | Usually denormalized |
| Consistency | Strong by default | Often eventual consistency |
| Scaling | Mostly vertical, sharding is complex | Built for horizontal scaling |
| Good for | Financial data, structured relationships | High write throughput, flexible or huge datasets |

**Spoken answer:** I lean toward SQL when data has clear relationships and strong consistency really matters, like financial transactions. I lean toward NoSQL when the schema needs to be flexible, or when I need to scale writes horizontally across many servers, like storing activity logs or session data for a huge user base.

---

## Database Replication

**Spoken answer:** Replication keeps copies of the same data on multiple database servers. Usually there's one primary server that handles writes, and one or more replicas that handle read traffic, which spreads out the load and improves availability. If the primary fails, one of the replicas can be promoted to take over, though there's often a short delay before that failover completes.

---

## Sharding

**Spoken answer:** Sharding splits a large database into smaller pieces called shards, each holding a portion of the total data, usually spread across multiple servers. For example, users could be split by region or by a range of user IDs, so no single server has to store or serve the entire dataset. The tricky part is choosing a good sharding key, since a bad choice can lead to uneven load, where one shard gets far more traffic than the others.

---

## Consistent Hashing

**Spoken answer:** Consistent hashing is a technique used to distribute data across servers in a way that minimizes how much data needs to move when a server is added or removed. Instead of a simple modulo based approach, which would reshuffle almost everything when the server count changes, consistent hashing only affects a small portion of the data, which makes scaling a distributed cache or database much smoother.

---

## Message Queues

**Spoken answer:** A message queue lets different parts of a system communicate asynchronously, where one service sends a message, and another service processes it whenever it's ready, instead of waiting for an immediate response. This decouples services from each other, smooths out sudden traffic spikes, and makes the system more resilient, since a temporarily slow or down consumer does not block the producer from continuing its work. Tools like RabbitMQ, Kafka, and SQS are common examples.

---

## Microservices vs Monolith

| Monolith | Microservices |
|---|---|
| One codebase, one deployment | Multiple independent services |
| Simpler to develop early on | More complex, needs strong infrastructure |
| Harder to scale specific parts independently | Each service can scale independently |
| A bug can affect the whole app | Failures can be isolated to one service |

**Spoken answer:** A monolith keeps the entire application as one codebase and one deployable unit, which is simpler to build and reason about early on. Microservices split the application into smaller, independently deployable services, which gives more flexibility to scale and update parts separately, but it also introduces real complexity around networking, data consistency, and monitoring across services.

---

## API Gateway

**Spoken answer:** An API gateway acts as a single entry point that sits in front of multiple backend services, handling things like routing requests to the right service, authentication, rate limiting, and logging, all in one place. This means individual services don't each need to reimplement those same cross-cutting concerns themselves.

---

## Rate Limiting

**Spoken answer:** Rate limiting controls how many requests a client can make within a certain time window, which protects the system from being overwhelmed by too much traffic, whether from a genuine spike or an abusive client. Common approaches include the token bucket and sliding window algorithms, which both track request counts over time and reject requests once a limit is exceeded.

---

## CAP Theorem

**Spoken answer:** The CAP theorem says that in a distributed system, I can only fully guarantee two out of three properties at the same time, consistency, availability, and partition tolerance. Since network partitions are unavoidable in any real distributed system, the actual choice usually comes down to favoring consistency or availability when a partition happens. A banking system often favors consistency, while a social media feed often favors availability.

---

## Consistency Models

| Model | Description |
|---|---|
| Strong consistency | Every read gets the most recent write immediately |
| Eventual consistency | Reads may return stale data temporarily, but all replicas converge eventually |
| Read your writes | A user always sees their own recent updates, even if others don't yet |

**Spoken answer:** Strong consistency guarantees that once a write is confirmed, every subsequent read reflects it immediately, which is important for something like an account balance. Eventual consistency allows a short delay before all replicas agree on the same value, which is acceptable for something like a social media like count, where a small delay doesn't cause real harm.

---

## Availability and Redundancy

**Spoken answer:** Availability means the system stays operational and responsive even when parts of it fail. This is usually achieved through redundancy, running multiple instances of critical components across different servers or even different data centers, so that the failure of one does not take down the whole system.

---

## Designing for Failure

**Spoken answer:** In distributed systems, failures are not rare edge cases, they are expected to happen regularly, whether it's a server crashing, a network call timing out, or a disk filling up. I design with that assumption in mind, using techniques like retries with backoff, circuit breakers to stop repeatedly calling a failing service, timeouts to avoid waiting forever, and redundancy so no single failure takes down the whole system.

---

## How to Approach a System Design Interview

1. Clarify requirements, both functional and non-functional
2. Estimate scale, like number of users, requests per second, and data size
3. Define the high level API or main use cases
4. Sketch a basic architecture with the major components
5. Dive deeper into one or two critical components
6. Discuss trade-offs, bottlenecks, and how to scale further
7. Talk about failure scenarios and how the system handles them

**Spoken answer:** I always start by asking clarifying questions rather than jumping straight into a diagram, since assumptions about scale or requirements completely change the right design. After that, I sketch a simple high level design first, and only then go deeper into the parts that matter most, rather than trying to design every component in perfect detail from the start.

---

## Common Interview Questions (Spoken-Style Answers)

**Q: What is the difference between vertical and horizontal scaling?**
Vertical scaling adds more resources, like CPU or memory, to a single existing server. Horizontal scaling adds more servers and spreads the load across them. Vertical scaling is simpler but has a hard limit, while horizontal scaling can grow much further but requires the system to be designed to work across multiple machines.

**Q: How would you design a system to reduce database load?**
I would add caching for frequently read data, introduce read replicas to spread out read traffic, and consider sharding if the dataset itself becomes too large for a single server to handle efficiently.

**Q: What is the CAP theorem and why does it matter?**
It states that a distributed system can only guarantee two of three properties at once, consistency, availability, and partition tolerance, when a network partition occurs. It matters because it forces an explicit decision about what the system should prioritize during a failure, which shapes a lot of the architecture.

**Q: What is the difference between a load balancer and an API gateway?**
A load balancer primarily distributes traffic across multiple instances of the same service to balance load. An API gateway is a broader entry point that can also handle routing to different services, authentication, and rate limiting, though the two concepts sometimes overlap in real systems.

**Q: When would you choose eventual consistency over strong consistency?**
I'd choose eventual consistency when a short delay in data propagation is acceptable in exchange for better availability and performance, like a view counter or a social media feed, where showing slightly stale data for a moment doesn't cause real harm.

**Q: What is a single point of failure and how do you avoid it?**
It's a component that, if it fails, brings down the entire system. I avoid it by adding redundancy, running multiple instances of critical components across different servers, and using load balancers or failover mechanisms so no single failure takes everything down.

**Q: How do message queues help with system scalability?**
They decouple the producer of a task from the consumer that processes it, allowing each to scale independently and absorb sudden traffic spikes, since messages can wait in the queue instead of overwhelming a service that can't keep up in real time.

---

## Quick Cheat Sheet

| Concept | Purpose |
|---|---|
| Load Balancer | Distribute traffic across multiple servers |
| Cache | Reduce load and latency for frequently accessed data |
| CDN | Serve static content from locations near the user |
| Read Replica | Spread out read traffic from the primary database |
| Sharding | Split large datasets across multiple servers |
| Message Queue | Enable asynchronous communication between services |
| API Gateway | Single entry point for routing, auth, and rate limiting |
| Rate Limiting | Protect the system from excessive traffic |
| Circuit Breaker | Prevent repeated calls to a failing service |
| Consistent Hashing | Minimize data movement when scaling distributed storage |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your system design interviews.

</div>