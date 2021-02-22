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



