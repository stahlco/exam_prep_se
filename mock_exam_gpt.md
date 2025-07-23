## Questions Easy

Why does AWS recommend adding jitter to backoff strategies when retrying requests?

What is static stability and why is it important for high-availability systems?



## **Questions Hard**
You're designing a high-throughput service that calls a downstream payment gateway with unpredictable latency. What kind of retry strategy would you implement based on AWS guidance

You're building a service that aggregates user data from 200 microservices. Initially, the fan-out causes latency and scaling issues. How does shuffling shards reduce this load, and in what kind of workload does this technique become essential?

You need to run a daily cleanup job that deletes stale cache entries across multiple regions. Why is leader election + heartbeats a better choice than a cron job on one instance, and how would you handle failover in this architecture?

You're deploying a new version of a service that changes data schemas. How would you structure your deployment and rollout strategy to ensure rollback safety, especially in a multi-team environment where clients might still rely on older versions of the API?

Your API service is experiencing a surge in traffic due to a flash sale. Explain how load shedding helps achieve static stability, and how you would decide which requests to drop under pressure?

You need to migrate from a monolithic backend to multiple microservices without downtime. How does keeping a stable API at the load balancer layer support this evolution, and what patterns would AWS recommend to decouple old and new systems during this process?

A downstream ML model inference service has unpredictable latency spikes. Why should the caller control the timeout, and what risks arise if the callee tries to determine its own timeout?

You’re using a leader-based distributed store. Under network partition, some nodes still respond as leader. What are the dangers of leader stickiness, and how does AWS avoid this risk in critical services?




## **Questions**

1. **(4 pts)** A startup runs its application on a powerful single server but expects growing traffic. It wonders whether to scale up (vertically) or scale out (horizontally). Under what conditions is vertical scaling appropriate, and when should horizontal scaling be planned? Explain any caveats.

	
2. **(2 pts)** An online service experiences periodic load spikes. Define _scalability_ versus _elasticity_ in this context. Give an example of each (for example, doubling resources versus handling the transition)
    
3. **(3 pts)** A developer suggests breaking the monolithic app into microservices. How does separating stateful from stateless components in microservices help with scaling? Describe how microservices can ease vertical versus horizontal scaling.
	
    
4. **(2 pts)** Explain the concept of _scale-to-zero_ in cloud computing. Why do most services not truly scale to zero, and in what scenarios might something akin to scale-to-zero happen?

    
5. **(3 pts)** In a distributed database, what are the trade-offs between synchronous replication and asynchronous replication? In what scenario might you choose one over the other?

    
6. **(3 pts)** Compare _update-everywhere (multi-master)_ replication versus _primary-copy (single-master)_ replication in a distributed system. What are the advantages and disadvantages of each approach?
	

7. **(3 pts)** The CAP theorem states a trade-off under network partition. The PACELC model extends this concept. Explain the consistency/availability/latency trade-offs embodied by CAP and PACELC. For example, what trade-off remains even when there is no partition?
    
8. **(3 pts)** Describe two common sharding strategies for a database (such as range-based and hash-based sharding). What are their benefits and drawbacks?
    
9. **(2 pts)** A service call to a backend sometimes hangs, causing overall slowdown. What combination of timeouts, retries, and backoff strategy (including _jitter_) should be used by the client to handle such transient failures, and why?
    
10. **(4 pts)** A cluster of nodes must elect a leader to coordinate writes. Discuss the benefits and drawbacks of having a single leader. How might the system mitigate problems of a single leader, and what pattern is often used for leader election?
    
11. **(2 pts)** During a sudden traffic surge, a web service is in danger of overload (very high latency or failures). What is _load shedding_, and how can it help keep the service operational under extreme load?
    
12. **(2 pts)** A multi-tenant service wants to isolate workloads so that a surge of requests from one tenant doesn’t impact others. Explain how _shuffle sharding_ achieves workload isolation and limits the blast radius of failures.
    
13. **(3 pts)** A client may retry an API call when it times out. How should the API be designed so that retries do not cause duplicate side effects? Explain the concept of an _idempotent_ API operation and one practical way to implement it.
    
14. **(4 pts)** Consider a service that caches database results in-memory for performance. What problems can occur if the cache suddenly becomes unavailable or empty? Describe the “cache dependence” issue and a mitigation technique.
    
15. **(4 pts)** Many services use a durable queue to handle requests asynchronously. What risk arises if the producer generates messages faster than consumers can process them? Explain what happens to latency and recovery time after an outage if a large backlog builds up in the queue.
    
16. **(4 pts)** A system has a small control-plane service (manages configuration) and a much larger data-plane fleet (worker nodes). If every worker polls the control plane frequently, the control plane can get overwhelmed. Describe an architecture that avoids overloading the control plane by _reversing the flow of control_.
    
17. **(3 pts)** You are debugging a production service that has occasional high-latency outliers. Why is it important to instrument and monitor tail latencies (e.g. 99.9th percentile) in addition to average latency? What do high-percentile latencies indicate?
    
18. **(2 pts)** What is _dependency isolation_ in the context of service-to-service calls? Give an example of how limiting concurrency to a slow backend can help other parts of the service continue to work.
    
19. **(4 pts)** Define a _correlated failure_ in a distributed system. What is one strategy to minimize correlated failures in practice (for example, in replica placement or workload assignment)?
    
20. **(3 pts)** Many systems consider using fallback strategies (alternative methods) when a call fails. Explain why AWS recommends generally _avoiding fallback_ in distributed systems, and what alternative approach is preferred for handling a critical failure.
