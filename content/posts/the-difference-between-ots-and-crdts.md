---
title: The difference between operational transformations (OTs) and CRDTs
date: 2022-05-09
tags: [algorithms, crdt, operational, transformations]
---

How do you ensure systems remain consistent even when a partial network failure happens between them? Seems impossible, right? Commonly, systems would delegate a leader and changes would be sent to the leader first. The leader would propogate changes to their replicas, where you will need to rely on network latency in order to ensure the information is propogated to all replicas. In the event of a network partition, your system may end up with a split brain with inconsistent data across the partition. CRDTs aim to ensure updates are consistently propogated to all nodes without the delegation of a leader, which avoids a split brain problem.

CRDTs avoid causing split brains by using a star or ring topology<!--QC1-->. Every node in a CRDT system communicates with every other node - so if there is a network partition between S1 and S2, but not between S1 and S3, eventually the right value will be propagated to all nodes. When a node receives information from another node, it needs to apply a merge operation which is commutative<!--QC2--> (i.e. the order in which the merge is applied does not change as long as the terms don't change) and must be the same operation that is used by all other nodes to resolve conflicts.

Although this sounds like a dream, CRDTs do present their own problems. For one, it is not ideal for real-time document collaboration, like Google Docs for example. The reason for this is because we would have to design a way to map the characters such that they are ID'd by their position in the doc. It so happens that this is a common method which lends itself to a commutative merge operation which can be used by either client. However, this approach is prone to interleaving<!--QC3-->, which is where two clients who have started typing from the same position, will result in both of their inputs interleaved with each other:

```
Client 1: Hello World
Client 2: Hello Earth

Output: Hello EWoarltdh
```

There are alternatives to CRDTs which do lend themselves better to real-time document collaboration: for example, operational transformations (OTs).

OTs work by taking the changes from each client, applying a merge operation in a central location and then committing the transformations back to the clients. This takes the burden of conflict resolution away from the clients and manages them centrally<!--QC4-->. The only problem is that centrally managing these operations brings us back to a single point of failure and a higher probability of data loss<!--QC5-->.

As with everything in tech, there's always a trade off in the approach you take. It's important to know the pros and cons of each solution and decide on what "cons" you'd rather adopt for your use case.

**To read more about CRDTs and OTs, here are a few useful references:**

* [(Video) CRDTs: The Hard Parts][1]
* [(Blog) How do CRDTs solve distributed data consistency challenges?][2]
* [(Paper) Implementing counters with CRDTs][3]

<!-- References -->
[1]: <https://martin.kleppmann.com/2020/07/06/crdt-hard-parts-hydra.html> (Martin Kleppmann talk on CRDTs)
[2]: <https://ably.com/blog/crdts-distributed-data-consistency-challenges#what-are-operational-transforms> (Ably blog on CRDTs)
[3]: <https://www.cs.utexas.edu/~rossbach/cs380p-fall2019/papers/Counters.html> (Implementing counters with CRDTs)

<!-- Questions and comments - refer to IDs with QC prefix

1. Confirm that star topology is the correct terminology here
2. Confirm that declarative is the right terminology here
3. Include a nicer diagram to explain interleaving
4. Do the operations still have to be commutative in OTs? Re-watch Martin Kleppmann's video again.
5. Confirm these are actually the drawbacks of OT by wathcing Kleppman's video
-->