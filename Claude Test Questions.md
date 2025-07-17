
##  System Design & Trade-offs

*You're designing a global social media platform expecting 100M+ users. What scaling approach would you choose and why? Consider the trade-offs between vertical vs horizontal scaling.*

- Horizontal Scaling - wegen Replication bei 100M+ Usern, Mehr Load, Fault Tolernace auf dieser Scale ist sehr wichtig

*A startup's monolithic application is hitting performance limits. What's your step-by-step approach to scale it out while maintaining availability?*

- on-premises computing with cloud bursting
- scale out the monolith (either in the cloud or on-premises)

## Consistency & Replication Strategy

*You're building a financial trading system where consistency is critical, but you also need global low-latency access. How would you design the replication strategy?*

- Replication across multiple locations 
  (Geographically Distributed Primary-Copy with Sharding)
- Each local cluster is the primary replica of the (Primary copy per region)
- Cross-region asynchronous replication (Fast Writes, and Strong Consistency)

*A collaborative document editing service (like Google Docs) needs to handle concurrent edits from multiple users. What consistency model and replication approach would you recommend?*

<img width="1195" height="619" alt="image" src="https://github.com/user-attachments/assets/c88bf15a-8100-4984-9a90-eda1e933096b" />

- Consistency Model (Different Consistency Views):
- Client-Centric-Consistency: From the prespective of the user the data feels consistent
  - Read-Your-Writes: If you write something, reading that data always returns your most recent write.
  - Write-Follows-Reads: A client that reads version X and then updates the same data item, will only update replicas that have at least version X.
  - Monotonic-Reads: A read will never return older values than previously returned to the same client.
  - Monotonic-Writes: If you write after another write, the writes should always be commited in the correct order.
 
  => If all Client-Centric-Consistency-Models
 
- Data-Centric-Consistency: From the perspective of replicas
- Replication Approach:

## Data Distribution & Sharding

*You're designing a messaging system like WhatsApp. How would you shard user conversations to ensure scalability while avoiding cross-shard queries?*

- Sharding users and chats independently:
  - Range-based
- Sharding based on logical attributes: Users on a shard, Chats on another shard 
- Key

- Sharding: 

*An e-commerce platform is experiencing hot spots where certain product categories get much more traffic. What sharding strategy would you implement?*
Sharding Strategies:
- Range-based sharding: 
- Key-based sharding:
- Directory-based sharding:
- Geographic sharding:
- Natural sharding (if possible):

Key-based sharding, Product category can be split into the products, and the products can be distributed based on hashing algorithms


*A social media platform notices that posts from celebrity accounts generate massive traffic spikes while regular user posts have minimal engagement. What sharding strategy would you implement?*

- Key-Based Sharding, equal -> widely distributed
- Directory-based Sharding based on Metrics of the Server
- Implement Shuffle Sharding

## CAP Theorem & PACELC in Practice

*Your system currently prioritizes consistency over availability. Business requirements change to demand 99.99% uptime globally. How would you redesign the system architecture?*

- Sacrifice Consistency for Availability during a network partition -> Still remain eventual consistency
- 

*During a network partition, your distributed database must choose between availability and consistency. Walk through your decision-making process for different types of applications (banking vs social media).*

- Banking: Demands Consistency (sensible data - remain a global consistent state). Altough availability is important on a day to day basis, when a network partition occures or any other kind of failure, the bank can sacrifice consistency for availability.
- Social Media: Demands Availability (not so sensible data - data can easily be stale). Social Media can easily be eventual consistent and still serve requests 
and remain available
  

## Stateful vs Stateless Components

*You're migrating a legacy application with heavy session state to a cloud-native architecture. What's your strategy for separating stateful and stateless components?*

- 

*A gaming platform needs to scale player session management across multiple regions. How would you architect this to be both scalable and performant?*


## Cloud-Native Scaling

*Your serverless application is experiencing cold start issues during traffic spikes. What architectural patterns would you implement to maintain performance?*

*A system built on cloud services is hitting provider limits during peak usage. What multi-cloud strategy would you implement?*

## Failure Handling & Resilience

*Your distributed system needs to handle the failure of entire data centers. How would you design replica placement and failover mechanisms?*

*A microservices architecture is experiencing cascading failures. What patterns would you implement to increase system resilience?*

## Performance vs Consistency Trade-offs

*An analytics dashboard needs to display near real-time metrics but can tolerate some data staleness. What consistency model and caching strategy would you choose?*

*A ride-sharing app needs to match drivers with passengers quickly but also maintain data consistency for billing. How would you balance these requirements?*
