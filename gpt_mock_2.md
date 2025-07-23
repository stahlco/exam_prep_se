Mock Exam: Distributed Systems & Scaling Stateful Services

Instructions

Answer the questions as precisely and pragmatically as possible. Justify your design decisions. Where applicable, briefly explain tradeoffs or alternatives.

⸻

Section 1: Replication & Consistency

1.1
You’re designing a globally distributed online banking system where money transfers must be consistent, but customers expect low latency when checking their balance.
How would you design the replication strategy and consistency model to support both operations?

⸻

1.2
A developer suggests using asynchronous update-everywhere replication for a shopping cart service. Evaluate this choice and suggest improvements or caveats.

⸻

1.3
How would you implement “Read Your Writes” semantics in a system with eventual consistency? Propose two technical solutions and discuss tradeoffs.

⸻

1.4
Explain how vector clocks help in retrofitting causality to an eventually consistent system. What are potential drawbacks in practice?

⸻

Section 2: Sharding & Replica Placement

2.1
You’re scaling a system storing IoT sensor data globally. Each device writes frequently, and data is rarely read back. What sharding and replica placement strategy would you choose? Justify.

⸻

2.2
Compare key-based and directory-based sharding for a social media platform storing user-generated content. Which would you use and why?

⸻

2.3
A sudden increase in load on one range of user IDs (range-based sharding) leads to a hotspot. Suggest two solutions to mitigate this issue without complete rearchitecture.

⸻

2.4
You’re deploying a distributed file store with strict durability guarantees across continents. Which replica placement strategy (global mapping, hashing, chaining, scattering) would you pick, and how would you ensure fault tolerance?

⸻

Section 3: Load, Failures & Recovery

3.1
You notice latency increases and reduced throughput under high load in your API service. Walk through how you would design load shedding logic to maintain service reliability.

⸻

3.2
Your system uses retries to improve reliability, but during failures you experience retry storms. How would you design retry and backoff mechanisms to avoid correlated retries and further failures?

⸻

3.3
In a message-driven system, the consumer is slow, and the queue backlog becomes insurmountable. What would you change in your system to prevent this from happening again?

⸻

3.4
How would you design a system to gracefully recover from overload without human intervention?

⸻

Section 4: Consistency & Idempotency

4.1
You are building a payment API where retries are possible. How would you implement idempotent request handling and what role do client tokens play?

⸻

4.2
Design a safe retry mechanism for a distributed database write API that might return ambiguous errors (e.g., timeout but operation may have succeeded).

⸻

4.3
A developer proposes using fallback services to handle outages. When might this be acceptable, and what risks must be considered? Propose safer alternatives.

⸻

Section 5: System Design Decisions

5.1
You’re tasked with designing a metadata service for video files in a global streaming platform. Metadata must be fast to read, rarely written, and always available. Propose a system design.

⸻

5.2
You’re designing an architecture to scale a legacy monolithic e-commerce app. Which components would you separate first, and how would you introduce stateful scalability?

⸻

5.3
You’ve been asked to build a high-throughput logging system. What caching, queueing, and replication strategies would you employ to ensure scalability and durability?

⸻

5.4
How would you instrument a distributed system to detect correlated failures early and respond automatically?

⸻

Section 6: Short Concepts (Rapid Fire)

Briefly explain (max 3 lines each):

6.1 What is a sloppy quorum and where might it be acceptable?
6.2 What does constant work mean and when is it useful?
6.3 What’s the difference between throughput and goodput?
6.4 Why might fallbacks make outages worse?
6.5 What is shuffle sharding and how does it improve fault isolation?
