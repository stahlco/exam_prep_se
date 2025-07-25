Questions

	1.	(5 points) Design for Scalability and Elasticity (Microservices vs. Monolith):
You are building a new web service and choose a microservices architecture. Explain how you would design for scalability and elasticity. 
Compare vertical vs. horizontal scaling, and describe how you would handle components with infrequent but bursty demand (e.g., using a scale-to-zero approach). 

	2.	(5 points) Replication and Consistency in a Distributed Store:
Design a stateful distributed data store (for example, a user session or shopping cart store) that spans multiple data centers. 
Describe your replication strategy (e.g., primary/secondary or multi-primary, synchronous vs. asynchronous), the chosen consistency model, and how you would handle read/write quorum.
Discuss what happens during network partitions (CAP trade-offs) and how you would ensure data remains available and correct.

	3.	(5 points) Data Sharding and Partitioning:
You have a very large user database that must be distributed across several database servers. 
Explain how you would choose a shard key or partitioning scheme to balance load and allow efficient query routing. 
How would you handle hotspots or uneven growth in certain partitions? Illustrate with an example how you might re-shard or migrate partitions when load changes.

	4.	(5 points) Conflict Resolution with Vector Clocks:
Consider an eventually consistent key-value store where updates can be applied concurrently on different replicas.
Describe how vector clocks help detect and resolve conflicting updates. Provide a concrete scenario: two clients update the same key around the same time in different data centers.
Show how vector clocks would be attached to updates and how the system detects a conflict. What strategies would you use to resolve or merge those conflicts?

	5.	(5 points) Scaling Dimensions and Auto-Scaling:
Explain the differences between vertical scaling and horizontal scaling. Give an example scenario where each is appropriate.
In a cloud environment with auto-scaling, what metrics or signals would you monitor to trigger scaling actions? 
Discuss how you would achieve elasticity (automatic scale-out and scale-in) in response to workload changes while avoiding oscillations or overload.

	6.	(5 points) Scale-to-Zero and Event-Driven Scaling:
Some services see very little traffic most of the time, with occasional spikes (e.g. nightly batch jobs or infrequent user events). 
Explain how a scale-to-zero (serverless or cold-container) approach can save costs for such services.
What are the main trade-offs and challenges of scaling to zero? Discuss factors like startup latency (cold starts), state initialization, and how these affect system design.

	7.	(5 points) Timeouts, Retries, Backoff and Jitter:
Service A calls service B over the network. Sometimes B is slow or fails transiently.
Describe how A should use timeouts, retries with exponential backoff, and randomized jitter to improve resilience. 
Why is each technique important? What common pitfalls should you avoid (for example, retry storms)?

	8.	(5 points) Leader Election in a Cluster:
You have a distributed system of many nodes that need one leader at a time (for example, to coordinate a batch task).
Compare approaches for electing a leader (such as using a consensus algorithm, ZooKeeper/etcd, or a database lease).
What are the advantages and disadvantages of having a single leader? Explain why sharding the work is often used to mitigate a leader’s single point of failure and bottleneck.

	9.	(5 points) Load Shedding to Prevent Overload:
Your HTTP-based service suddenly experiences a traffic surge beyond its capacity. Explain what load shedding is and how you would apply it (for example, rate limits or rejecting excess requests) to protect the service. Describe at least two load-shedding strategies and how they help maintain low latency for accepted requests. What instrumentation or metrics would you use to detect overload and tune the load shedding?

	10.	(5 points) Shuffle Sharding for Fault Isolation:
In a multi-tenant service, suppose one tenant (customer) is hit by a large spike of requests (or a DDoS attack). Explain how shuffle sharding can isolate this tenant’s workload so other tenants are not impacted. Sketch a simplified example (e.g. 8 identical workers and 4 tenants) showing how you assign a random subset (“virtual shard”) to each tenant. How does this reduce the “blast radius” of failures?

	11.	(5 points) Idempotent APIs for Safe Retries:
Consider a non-idempotent operation, for example “CreateOrder”, that charges a customer. 
Describe how you would design an idempotent version of this API so that CreateOrder can be retried safely without duplicating work. 
What information would the client send, and how would the server use it to detect duplicate requests? Why are caller-provided idempotency tokens useful in this scenario?

	12.	(5 points) Fairness in Multi-Tenant Services:
A shared service hosts requests from multiple customers. One customer suddenly starts sending far more requests than usual. Explain how you would enforce fairness so that the overloaded customer doesn’t starve others. Describe the role of quotas or per-tenant limits and the difference between rejecting excess requests vs. letting them fail. How should the service communicate a “quota exceeded” error (e.g. HTTP 429 vs 503), and why?
