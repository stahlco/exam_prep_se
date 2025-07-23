Absolutely — here are the same scenario-based exam questions rewritten without the “Answer must consider” hints, just like a real exam.

⸻

🧠 Realistic AWS Builders Library-Style Exam Questions

⸻

Q1. The Retry Storm

Your team deploys a new feature to your distributed order processing service. Within minutes, your monitoring system lights up: latency increases, timeouts spike, and downstream services begin returning 500 errors. You roll back, and the system stabilizes. Postmortem analysis shows that retry attempts multiplied exponentially across services.

What changes should you prioritize to prevent this failure pattern from recurring?

⸻

Q2. The Poison Queue Problem

Your image processing service reads from an SQS queue. One malformed image causes repeated failures. The consumer keeps retrying and fails on that one message, preventing other images from being processed. The queue backlog grows to 10 million messages.

What architectural improvements would help you ensure system resilience in this scenario?

⸻

Q3. Global Outage from Fallback

A critical microservice fails in one region, triggering a fallback mechanism to redirect traffic to another region. However, the fallback path was stale, untested, and caused cascading failures in the new region due to configuration drift and overload.

How could you improve the system to support safer failover in the future?

⸻

Q4. Flaky Cache, Flaky UX

Users report stale or inconsistent product prices. The pricing service uses a write-through cache backed by a DynamoDB table. A recent incident revealed partial failures where cache writes succeeded but DB writes did not.

How would you fix the system to provide both strong consistency and high availability?

⸻

Q5. Leader Chaos

Your distributed coordination service uses leader election with heartbeats and leases. After a brief network partition, two nodes claimed leadership. Both began making conflicting decisions that broke downstream services.

What should you change in your coordination protocol to avoid split-brain leadership?

⸻

Q6. The Noisy Tenant

One enterprise customer of your multi-tenant data platform starts sending 100x more traffic due to a misconfigured batch job. This affects latency and throughput for all other customers, even though autoscaling is active.

What architectural improvements would help mitigate this issue?

⸻

Q7. Overloaded Control Plane

Your edge fleet begins a coordinated rollout. Each node requests config updates from the control plane. A bug causes them to retry on 429s without backoff. The control plane collapses under load.

What controls would you add to harden the control plane and prevent cascading failure?

⸻

Q8. Outage in the Dark

A system outage takes 30 minutes to diagnose. Dashboards show rising latency, but no clear service is identified as the root cause. Your team relies mostly on logs for observability.

What monitoring and instrumentation changes would help you detect and diagnose faster?

⸻
