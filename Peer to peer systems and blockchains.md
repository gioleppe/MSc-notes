## Peer to peer systems and blockchains

---

University of Pisa, Computer Science MSc, AY 20/21.

Lecturer: **Professor Laura Ricci**.

Notes taken by Tommaso Colella.

\newpage

---

### Lecture 1

Peer to peer started as a file sharing mean. Peers have a great "churn" problem, because of their on/off behaviour. A server is needed in order to bootstrap the P2P network. Peers are both providers and consumers. A peer to peer system is made of autonomous entities, it can auto-organise, and works in a complete or partial decentralized way. Another definition of P2P network focuses on its goal of sharing node resources, and being able to adapt to continuous churn.

#### Blockchain

It has various definitions:

1. A shared database stored in multiple copies on computers throughout the world, maintained without the need for a central authority
2. replicated and consistent, immutable, append only data storage system resistant to tampering
3. a write-only, decentralized, state machine that is maintained by untrusted actors, secured by economic incentive. You cannot delete data, nor shut down or censor the blockchain. It supports defined operations agreed upon by participants that may not know each other. The best interest for each actor involved is to play by the rules.

**Bitcoin**: by Satoshi Nakamoto, October 2008.

---

### Lecture 2

**Ethereum**: it's main innovation are smart contracts. The language in which smart contracts are written is T-complete. This is quite cool since Bitcoin's smart contract language (scripts) is not T-complete, whereas the ethereum one can be exploited to write any computable function. 

The smart contract is executed by all the nodes: they reach a consensus as agreement on the results of the computation.

You have to pay some "gas" in order to avoid denial of service, you have to buy gas to your programs in order to run them on the nodes. 

Blockchains are being classified on some of their properties (who can read, execute and validate transactions and blocks):

- Public vs Private 
- Permissionionless vs Permissioned

You don't need a blockchain when all parties are known and trusted, use databases instead.

If parties are known and trusted but you also need immutability, do not use a blockchain.

The success of a P2P application greatly depends from the creation of a "critical mass of users".

#### Unstructured overlays

**Semi-decentralized** systems such as Napster, one of the first P2P applications. The Napster servers had peers connecting to the to donwload file descriptors, then the effective download was Peer to Peer.

The main strength with semi decentralized systems is resource sharing, while its main weakness is that a centralization point still exists.

**Fully decentralized systems** such as Gnutella, there's no cenral index, queries are sent on the network. Gnutella was the first overlay network example. Gnutella was self organizing.

What is a **Peer to Peer overlay**? a logic network defined at application level connecting peers laid over the IP infrastructure. It's built on top of an existing network and provides services not available in the underlying network. Most P2P overlays are build over TCP/IP.

---

### Lecture 3

Recap on P2P overlays.

One of the topic of research is how to map the logical overlay to the underlying physical one wrt P2P overlays.

P2P overlays exploit the services provided by the TCP/IP stack

- **Unstructured overlays**: the topology doesn't follow any specific rule
- **Structured overlays** such as distributed hash tables (these follow a set of rules)
- **Hybrid overlays**: Super peers

#### Unstructured overlays

To find information inside an unstructured overlay, you need to use a look-up algorithm. These are easy protocols, highly resilient to churn, but the lookup cost is high (linear in the number of nodes in the network) and the scalability is low.

Let's give a look to Gnutella, an example of unstructured overlay:

- there's no index information
- connections between peers are defined at random

The main problems lie with bootstrapping the network and finding content without a central index.

The bootstrap problem is common in all P2P systems. Usually there's a sort of repository of peer descriptors, such as Gnutella's WebCache, which stores the IP addresses of a list of "stable" peers. The cache is dynamically and automatically updated. The joining peer has an internal cache storing the IP addresses of peers contacted in current and previous sessions, that is updated regularly as well.

Gnutella uses the Ping Pong Protocol to discover the network, and employs a TTL to limit flooding.

Searching the Gnutella network works via a message flooding known as "gossiping". The query is sent to neighbours, they forward them to their neighbours and so on until the TTL zeroes. Cycles are detected by pairing a unique identifier with each message. When content is found, the reply to the lookup gets routed backwards to the peer who issued the query, then the actual file is transferred by means of a standard HTTP connection.

Sometimes, in these kind of networks, it is possibile to have false negatives: a content is present in the network but because of TTL you may not find it

Which are the main methods to search content in an unstructured overlay?

- Breadth first (such as the one used with flooding)
- Expanding ring/Iterative deepening: a sequence of flooding with increasing TTL
- Random walk (drunkard's walk): it is described by a markov chain, the system has no memory of previous states. each neighbor could be chosen on different criteria and there are many variants of this.

**K-Random walk**: the querying node sends out k query messages to an equal number of randomly chosen neighbours, then each step follows each own path by choosing one neighbor to forward it. TTL is used to stop the search. Each path is a walker. K-Random walk is a popular substitute for flooding, it reduces the number of messages but search latency increases. Another possible stopping mechanism is to check back with the issuing node if the information has been found.

Self organized systems such as the unstructured overlays are well known for their distribution of control, local interactions, information and decisions, emergence of global structures, and failure resilience. 

For instance, looking at the Gnutella backbone, a network of server-like nodes emerges from the interactions in the Gnutalla system.

#### Structured overlays

The choice of neighbors is defined according to some given criteria, and the resulting overlay network is structured. The goal is to guarantee scalability with key-based look ups, and guaranteeing that the look up of an information always has a given complexity (for instance $O(log(N))$)

#### Hierarchical overlays

There are both peers and super-peers. Peers connect to Super-Peers, which know the Peers' resourced and index them.

The flooding mechanismis restricted to Super-Peers and resources are then directly exchanged between the peers.

The main pro is the lower lookup cost and the improved scalability, but this kind of network is clearly less resistant to churn.

Super-Peers are chosen autonomously by the system, based on their capacities and availability. They periodically exchange information on peers' resources.

Peers upload their resource description to a Super-Peer, query them for information, and are involved in resource transfer.

#### Content distribution networks (CDN)

Let's suppose a server publishes new content, such as a new videogame, operating system, or song: since a single centralized server is a bottleneck when serving content, especially for video/audio streaming applications, a P2P content distribution is adopted. The initial file request are served by a centralized server, while further requests are served by peers which have already received and replicated the files.

**Bittorrent is basically a CDN**

Retrieving content in a pure P2P syste can be made by either:

- Searching, on the value of a set of attributes of the content, "Google style", such as gnutella does, but this has poor scalability and overhead due to comparing whole objects.
- Addressing: associating a unique identifier to the content and exploiting it to search for the content itself. The main advantage is efficient object detection, while disadvantages are ID computation by hashing and maintaining the addressing structure.

#### Distributed hash tables

They've been devised as a way to compromise between centralized server and flooding approaches. The idea is simply to split hash tables into several parts and distribute them to several servers. Initially this strategy was employed for web caching, the technique was later extended to DHT in P2P systems.

**Rehashing problem**: if a server crashes you have to rehash all the keys, this is clearly impossible for P2P applications, so the classical hash function doesn't work. The solution is **consistent hashing**: an hashing scheme that doesn't depend directly on the number of servers. It guarantees that adding more nodes/removing nodes implies moving only a minority of data items.

By using consistent hashing functions, keys are distributed quite evenly on the ring, but nodes may be different, some may be more or less powerful, so the idea is to assign more positions to the more powerful servers (load balacing wrt DHT).

Content addressing vs. Location addressing

The main idea with location addressing is to fingerprint the content (for example using an hash function) in order to recognize it. IPFS uses location addressing.

---

### Lecture 4

#### Content Addressing (continued)

How to actually implement content addressing? The hash function is not enough. A routing algorithm is required.

We want a maximum of $O(log(n))$ steps to reach the content, the routing should be efficient.

We also want to implement policies to support a voluntary node leave and a node failure. Of course a voluntary leave is not as catastrophic as a node failure, since the leaving node could redistribute its address space to the neighbor nodes, while in case of node failure, we need to introduce some redundancy in order to be able to sustain such an event.

Different DHT proposals have different network topologies.

#### DHT API

It is very simple, usually has just:

- PUT(key value) for content insertion
- GET(key) for content search

The DHT approach doesn't support complex queries, which are instead supported by a centralized approach or a pure P2P flooding.

Some real applications using DHT approaches are:

- IPFS
- Bittorrent
- Ethereum

#### The Chord DHT

The main idea is to base the system on a few, very powerful concepts:

- Applying consistent hashing concepts
- Routing is logarithmic with very high probability, and the routing table has a logarithmic size with very high probability.
- The network is self organising and self adapting, in case of a node's leave.

Chord applies the Consistent Hashing concept.

How does look up work? A node implements a minimal Routing Table, each node remembers only te next node on the ring, and this is the only knowledge of a node about other nodes of the ring. Queries are forwarded to each node's successor in the ring. 

The main disadvantage is that the routing is linear and is subject to single node failure.

We want to reduce the number of steps: the way to do so is to let a node store links for z neighbors, we want to find a logarithmic mesh of the nodes of the ring (more links towards close neighbors, less links towards far neighbors)

Each node maintains some data structures to support routing:

1. The finger table
2. a link to its successor and to its predecessor
3. a set of pair (key, value)

So, how is the routing algorithm made in Chord?

- Each node propagates a query with key k to the farthes finger preceding k.
- The propagation of the key goes on untile the node n such that $((n < k) \and successor(n) \geq k)$ in $mod(2^n)$ arithmetic. In this case successor(n) owns the key.

#### Handling Churn in Chord

The main reason why Chord has never been used in real applications is because of its strict topology rules, that make it hard to maintain the network.