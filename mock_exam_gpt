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































## **Answers**

1. **(4 pts)** _Vertical (scale-up) scaling_ means using a more powerful machine. It is easiest to implement initially – especially for stateful components (e.g. a single database instance) – because it avoids many distributed-system issues . Vertical scaling is effective while your component (or microservice) can fit on one machine and handle the load. However, if demand continues to grow, you must plan to _scale out_ (horizontal) eventually. Horizontal scaling adds more machines or instances in parallel. The catch is that stateful parts become harder to replicate, so you typically separate out stateless parts (which can scale horizontally easily) and push stateful parts as far as possible vertically . In other words, use vertical scaling initially (for simplicity) but architect so you can add replicas horizontally later. Microservices naturally support this: each service can be scaled independently, allowing vertical scaling per service while planning for horizontal growth .
    
2. **(2 pts)** _Scalability_ is the ability of a system to handle increased load by adding resources. For example, if doubling CPU or instances leads to roughly doubling throughput in the new steady state, the system is scalable . _Elasticity_ refers to how smoothly a system can adapt to changing load (scaling actions) over time – including the transition effects. For instance, when load spikes, an elastic system can add instances quickly, and latency only grows moderately during that transition. In short, scalability is about the final capacity (e.g. “doubling resources doubles capacity”), while elasticity is about how the system behaves _during_ scaling (e.g. how latency or intermediate states are handled) .
    
3. **(3 pts)** Microservices work best when each service has a narrow scope. One key design is to keep stateful components separate from stateless ones . A stateless microservice can be scaled up easily (up to the capacity of one server) and can also be cloned (scaled out) independently of state. Stateful components (like databases) are kept minimal. This separation lets you treat stateful parts with vertical scaling as far as possible, while using horizontal scaling on stateless microservices . For example, a stateless front-end service can be run on multiple servers behind a load balancer. Each microservice contains less functionality (and data) than a monolith, so it can often rely on vertical scaling, but when demand is high each service can also be replicated. In summary, microservices allow each piece to be scaled independently – you can scale the lightweight stateless parts horizontally and handle the stateful parts with the best mix of vertical or limited replication .
    
4. **(2 pts)** _Scale-to-zero_ means reducing resources to zero when load is zero (common in serverless). In practice most systems don’t truly scale to zero because some infrastructure must always run (e.g. a load balancer or management service) . For example, big-data batch jobs can be shut down after they finish (but the job manager still exists) and serverless functions appear to scale to zero from the developer’s view. However, even serverless providers keep control-plane servers and often maintain a warm pool to avoid cold-start delays . In short, clients see “scale-to-zero” when no requests occur (they pay nothing), but the cloud provider always has some minimal infrastructure. The “exceptions” are batch or serverless jobs: a Lambda function can idle at zero user cost, but under the hood there is still a control plane and possibly a cold-start delay .
    
5. **(3 pts)** With **synchronous replication**, every write is immediately copied to all replicas before returning success. This ensures strong consistency and durability: once the write returns, you know all replicas have it. The trade-off is higher latency (every write waits for all nodes) and lower availability (if any replica is down, the write may fail). Synchronous replication is useful when consistency or durability is critical. **Asynchronous replication** lets the primary node return success before replicas catch up. Writes complete faster and the system stays more available if replicas lag, but a fast node crash can lose recent updates and replicas can see stale data. In other words, synchronous gives strong consistency at the cost of performance; asynchronous gives better write performance and availability but only eventual consistency. You might choose synchronous for a distributed ledger where every replica must record the update, and asynchronous for a geo-distributed cache where occasional staleness is acceptable in exchange for low write latency.
    
6. **(3 pts)** In an _update-everywhere (multi-master)_ system, all replicas can accept writes and propagate them to each other. This removes a single bottleneck and increases availability (clients can write to any node). However, it introduces conflicts: concurrent writes to different replicas may conflict and require conflict resolution or complex merging. It also means more replicas must communicate, complicating consistency. By contrast, _primary-copy (single-master)_ replication has one designated writer (the primary/master) and others replicate from it. This simplifies coordination (no write conflicts), and usually provides stronger consistency out of the box, but the primary is a single point of failure or a scalability limit. If the primary is slow or down, writes pause (although read replicas may still serve reads). In summary, update-everywhere is powerful for availability and locality but needs conflict resolution (often via vector clocks or CRDTs), whereas primary-copy is simpler and safer for consistency, at the cost of a potential leader bottleneck.
    
7. **(3 pts)** The CAP theorem says a distributed data system can only simultaneously guarantee **Consistency** or **Availability** when a network _Partition_ occurs. If a partition happens, you must choose: halt writes on some nodes to remain consistent, or accept writes on all nodes (losing consistency) to remain available. PACELC extends this by noting that even _without_ a partition (Else), there is still a trade-off between **Latency** and **Consistency**. In other words, when the network is working (no partition), you can still favor low-latency (eventual consistency) over strict consistency, or vice versa . For example, DynamoDB chooses availability during partitions and high responsiveness (low latency) during normal operation at the expense of strong consistency (it is eventually consistent) . In summary, CAP: on partition choose C or A; PACELC: if no partition, choose low Latency or strong Consistency (e.g. a system might forgo immediate consistency to get lower latency even when healthy) .
    
8. **(3 pts)** **Range-based sharding:** Data is partitioned by a contiguous key range (e.g. customer A–L on shard 1, M–Z on shard 2 ). This is great for range queries or scans (queries that naturally sort by the key range). However, it’s vulnerable to skew: if many keys land in one range or queries skew to one range, that shard becomes overloaded . **Hash (key-based) sharding:** Use a hash of the key to assign a shard. This evenly spreads data (and usually load) across shards . The downside is that range queries are hard (data is scattered unpredictably) . Other strategies include directory-based sharding (a lookup service maps keys to shards) or geographic sharding (by region) , each with their own trade-offs. For example, directory sharding can mitigate hotspots but adds complexity and a metadata service (single point of failure) .
    
9. **(2 pts)** The client should set a reasonable **timeout** for the remote call so that hung requests are aborted rather than waiting indefinitely . On timeout or transient failure, the client should **retry**, but not immediately in a tight loop. Use **exponential backoff with jitter**: wait a random interval that increases with each retry . The jitter (random variation) is critical to avoid all clients retrying in sync (which would create load spikes). Timeouts prevent waiting on dead calls , backoff avoids overwhelming the service during failure, and jitter spreads out retries .
    
10. **(4 pts)** Having a single leader (master) means all coordinated updates go through one node. The benefit is simplicity: consensus and serializing operations are easier since there’s a known authority, and reads or writes can be ordered through the leader . The drawbacks are a potential single point of failure and bottleneck: if the leader goes down or is slow, the system stalls. Also, maintaining a single leader can hurt availability in some designs (unless using a replicated proxy). To mitigate this, systems often implement automated leader election protocols (using tools like ZooKeeper, Raft/Paxos, or even simple heartbeats) so that if one leader dies, another can take over . They also use **leases** or timeouts to ensure one leader at a time. For example, after a leader fails health checks, replicas elect a new leader. In summary, a leader simplifies coordination but requires failover planning (e.g. election, redundancy) to avoid downtime .
    
11. **(2 pts)** _Load shedding_ means the service deliberately rejects or drops some excess requests when overloaded. Instead of queueing up or working slower on everything, an overloaded service “sheds” the least critical work (for example, returning HTTP 503 errors immediately) so it can serve the remaining requests at low latency . This keeps the service responsive for the requests it does accept, avoiding a state where latency spirals upward and throughput collapses. In effect, load shedding maintains high _goodput_ (successful requests) even as offered load rises, preventing a complete meltdown .
    
12. **(2 pts)** _Shuffle sharding_ assigns each tenant a random subset of the servers (“virtual shard”) rather than all tenants sharing all machines. For example, if there are 8 servers, each tenant might be mapped to 2 random servers. The result is that if one tenant floods its assigned servers, only that small subset (and thus those other tenants sharing those servers) are affected. This greatly reduces “blast radius”: in the example, at most one server in any other tenant’s shard is impacted . With enough servers and shard combinations, shuffle sharding ensures no two tenants fully overlap their shards, so an attack or failure targeting one tenant will affect only a small fraction of others .
    
13. **(3 pts)** An _idempotent_ API ensures that repeating the same request has the same effect as doing it once . This allows clients to safely retry failed calls without creating duplicate resources. For example, a “create item” API can be made idempotent by requiring the client to supply a unique request ID; the server checks if it has already processed that ID, and if so it returns the same result rather than creating a new item . In this way, if a network timeout caused the client to retry, the service will detect the duplicate request ID and avoid doing the operation twice. In summary, design the API so that clients assume non-error responses are durable and retries only repeat the outcome. Using client-provided unique IDs (or constructing them from request data) is a practical implementation of idempotency .
    
14. **(4 pts)** Caching can dramatically improve performance, but it introduces a dependence: if the cache “dies” or is empty (cold), the database suddenly receives all reads. This _cache dependence_ can lead to sudden overload of downstream systems . For example, if a fleet of servers lost their in-memory caches at once (cache flush or instance restart), they would all hit the database, potentially overwhelming it. Similarly, an otherwise stable service might scale down its database too much, assuming the cache handles most queries; if the cache fails, the database can’t keep up and the whole system may stall . One mitigation is **request coalescing** or **cache pre-warming**: when a cache miss occurs, only one request recomputes the value and others wait, rather than all of them querying the database. Another approach is to ensure caches warm up gradually (throttling client requests on a cold start). These techniques help avoid the “thundering herd” and smooth the load spike .
    
15. **(4 pts)** Queues provide durability, but if messages accumulate faster than they are processed, the backlog grows and latency skyrockets. When the system is processing normally, queueing gives low-latency responses (fast mode). But if consumers slow or stop (e.g. a service outage) while producers keep adding messages, the queue builds up . After the outage, the system must process the backlog. This can take much longer than the outage itself (e.g. an hour-long downtime might need >2× processing time to catch up) . During the backlog drain, end-to-end latency is very high and clients must wait. In effect, queue-based systems have two modes: fast (empty queue) and slow (large queue). A huge backlog means recovery from failure is slow (high latency and load on downstream systems) rather than having requests dropped immediately. Thus, an unbounded queue can worsen overall availability – it protects against lost data, but at the cost of long delays after failures .
    
16. **(4 pts)** One approach is to have the **control plane push updates** to the data plane, rather than each worker polling the control plane. For example, the control plane can write configuration to a shared store like S3; data-plane nodes poll that store on their own schedule . This way, the small control plane fleet isn’t bombarded by requests from thousands of workers. Another pattern is to reverse the connection: each data-plane node opens a persistent connection to one control-plane server (e.g. via a load balancer), and then the control plane pushes updates over that connection . In either case, the smaller service _dictates the pace_. By pushing updates or writing them to a scalable intermediary, the control plane stays in control and cannot be swamped by simultaneous requests from the large fleet . These designs ensure the control plane only does as much work as it can handle and slows down its push rate if needed.
    
17. **(3 pts)** Tracking tail latencies (e.g. 99.9th percentile) is critical because a few slow requests can hurt user experience and other services. A system might have a good average latency, but if 1 in 1,000 requests takes 10× longer, that indicates a problem (outliers, resource exhaustion, GC pauses, etc.). AWS emphasizes focusing on 99.9th/99.99th percentile instead of just average . High-percentile latencies often drive customer impact and propagate delays downstream in a microservice call chain. Monitoring these outliers helps diagnose issues that averages hide – for example, one overloaded node or bad request pattern. Reducing the tail latency improves overall user experience and even brings down the median latency as a side effect .
    
18. **(2 pts)** _Dependency isolation_ means limiting how much a slow or overloaded dependency can affect the service as a whole. For example, if one part of your service makes calls to a slow database, you can use a separate pool of threads or circuit-breaker for those calls. This way, threads waiting on the DB don’t block other incoming requests that don’t need the DB. In practice, you might set a maximum concurrency for each dependency (a bulkhead). If the database slows down, at most that many requests queue up or fail; the rest of the service (like handling cached data or simpler operations) continues unaffected . In short, by isolating slow dependencies (e.g. using separate threads or limiting calls), other API endpoints can keep working even if one backend is sluggish .
    
19. **(4 pts)** A _correlated failure_ is an event that causes many replicas or components to fail together (e.g. a power outage or bug affecting an entire rack or region) . Such correlation defeats the benefit of redundancy because failures are no longer independent. To minimize correlated failures, one strategy is to spread replicas or workload across truly independent domains. For example, deploy replicas in different Availability Zones or regions (different power grids or networks). Another approach is **shuffle sharding** (workload isolation): ensure no two replicas handle the exact same workloads, so a workload-specific bug only affects a small subset . In general, isolating resources (anti-affinity) and introducing randomness (e.g. shuffle sharding) reduces the chance that a single fault affects all copies .
    
20. **(3 pts)** Fallback strategies (using an alternate path or degraded feature) can seem prudent, but in distributed systems they often introduce hidden complexity. AWS argues that relying on fallbacks (like serving stale data or using a “whiteboard” mode) tends to cause user-visible problems and subtle bugs . Instead of complex fallbacks, services should focus on resilience through retries, failover, or redundancy. For example, rather than showing outdated cached data (a fallback), a service should retry or switch to a different replica, ensuring correctness. In practice, AWS prefers designs that handle failures by _retrying, failing over, or rejecting work_ rather than graceful degradation – because fallbacks can be dangerous and their breakages take long to surface . The recommended approach is to engineer for reliability (using timeouts, retries, and failovers) and treat fallback as a last resort, if at all .
    

  

## **✅ Topics Covered in the Exam**

  

### **🔹 From** 

### **01-Foundations.pdf**

- ✅ **Scalability vs. Elasticity** – Q2
    
- ✅ **Vertical vs. Horizontal Scaling** – Q1, Q3
    
- ✅ **Microservices & Stateless/Stateful Separation** – Q3
    
- ✅ **Scale-to-zero** – Q4
    
- ✅ **Load balancers, decoupling, and autoscaling (briefly)** – Q1, Q3
    
- ✅ **Serverless and natural sharding (indirectly)** – Q3, Q4
    

  

### **🔹 From** 

### **02-Scaling Stateful Services.pdf**

- ✅ **Replication Strategies (4 core types)** – Q5, Q6
    
- ✅ **CAP & PACELC models** – Q7
    
- ✅ **Data Consistency Models (briefly)** – Q5, Q6, Q7
    
- ✅ **Sharding Techniques (range, hash, etc.)** – Q8
    
- ✅ **Replica Placement Considerations** – Q19
    
- ✅ **Vector Clocks, Versioning, and Causality (implied)** – Q6, Q7
    
- ✅ **Append-only Logs / Write-once-read-many (lightly)** – Q14
    
- ✅ **Single Writer Approaches (indirectly via replication Qs)** – Q5
    
- ✅ **CRDTs – mentioned via idempotency/conflict avoidance** – Q13
    

  

### **🔹 From** 

### **AWS Builder’s Library**

- ✅ **Timeouts, Retries, and Jitter** – Q9
    
- ✅ **Leader Election in Distributed Systems** – Q10
    
- ✅ **Load Shedding** – Q11
    
- ✅ **Shuffle Sharding for Isolation** – Q12, Q19
    
- ✅ **Idempotent APIs** – Q13
    
- ✅ **Caching Challenges and Dependency** – Q14
    
- ✅ **Avoiding Queue Backlogs** – Q15
    
- ✅ **Control Inversion / Smaller Service in Control** – Q16
    
- ✅ **Instrumentation & Tail Latency** – Q17
    
- ✅ **Dependency Isolation / Bulkheads** – Q18
    
- ✅ **Correlated Failures** – Q19
    
- ✅ **Avoiding Fallback** – Q20
    
- ✅ **Fairness & Constant Work (implicitly via load shedding / retries)** – Q11, Q15
    

---

## **⚠️ Underrepresented or Missing Topics**

  

### **From PDFs:**

- ❌ **Client-centric consistency models** (e.g., Monotonic Reads, Read-Your-Writes) – _not directly tested_
    
- ❌ **Quorum Systems (strict, sloppy, R+W > N, etc.)** – _briefly implied but not tested directly_
    
- ❌ **CRDTs (in full detail)** – _not directly tested, only related concepts_
    
- ❌ **Vector clocks (as a technique)** – _not fully addressed as a standalone mechanism_
    
- ❌ **GFS & Bigtable architectural examples** – _mentioned but not explored as scenarios_
    
- ❌ **Append-only logs / event sourcing / IPFS** – _barely touched_
    
- ❌ **Chaining / Scattering for Replica Placement** – _no dedicated question_
    

  

### **From Builder’s Library:**

- ❌ **Fairness in Multi-Tenant Systems** – _only implicit via shuffle sharding_
    
- ❌ **Reliability and Constant Work** – _underrepresented as a distinct theme_
    
- ❌ **Operational Visibility Beyond Tail Latency (e.g., metrics, logs, events)** – _briefly in Q17_
    
- ❌ **Minimizing Correlated Failures through proactive design (beyond placement)** – _not deeply explored_
    
- ❌ **Dependency Isolation: bulkheads, timeouts, concurrency limits (only lightly touched in Q18)**
    

---

## **📌 Recommendations**

  

To **fully cover your scope**, I recommend:

1. A **follow-up practice set** focused on:
    
    - Quorum systems (strict/sloppy)
        
    - CRDTs and Vector Clocks
        
    - Real-world examples like GFS/Bigtable
        
    - Advanced failure handling and operational visibility
        
    - Fairness and throttling in multi-tenant systems
        
    
2. A few **diagram or architecture-based questions** (e.g., design a scalable log ingestion system with limited queue backlogs).
    

  
