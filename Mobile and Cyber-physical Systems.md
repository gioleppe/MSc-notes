## Mobile and Cyber-physical Systems

---

University of Pisa, Computer Science MSc, AY 20/21.

Lecturer: **Professor Stefano Chessa**.

Notes taken by Tommaso Colella.

\newpage

### Lecture 1

This lesson was largely a course introduction, check out the recording.

----

### Lecture 2

By 2014 the number of mobile devices surpassed the number of humans on earth.

 A lot of devices will now operate autonomously, without human input, and leveraging their sensing abilities (achieved by using sensors). IoT devices have their own business logic, and they are deployed as independent physical objects. Many of these devices are already wearables and are full of sensors. A lot of these devices will be environmental ones, such as Smart cities sensors, Alexa, and so on. There are a lot of applications for these devices (Smart cities, health, robotics, ...), that said all these devices share a similar architecture with sensors and actuators. Consumer IoT market is exploding, and will become a huge economy in a few years. 

IoT is the last development for internet and computing. IoT devices are heterogeneous, there are both consumer and industrial devices. Internet connectivity is necessary in order to support the operations on the devices. Most of the devices are simple and are only sending sensor readings to the cloud, while others are more complex and need some more computational power (such as security cameras and so on).

Sensor/actuator technology is the "fourth generation" of the internet, with respect to end systems supported.

Each IoT device has sensors/actuators, a microcontroller, a wireless interface and some software (business logic). All data collected by sensors goes to the cloud where it is stored and processed for further usage. The cloud is also used is order to lock in (bind) users to a single vendor/manufacturer. Sensors and actuators are at the edge of the cloud. 

NoSQL databases are widely used in the IoT world because of their great horizontal scalability features and simpler design wrt SQL solutions. MongoDB is one of these NoSQL databases, it uses Documents inside, written in a json-like syntax and organized in Collections.

#### Relevant Issues in IoT

- Performance
- Energy efficiency
- Security
- Data analysis/processing 
  - Adaptability/personalization

- Communication middleware
  - How to bring together data producers with consumers
- Data representation
  - Data formats, standardisation
- interoperability

One of the main problems wrt performance is latency: roundtrip times could have an impact on critical applications such as alarms and security cameras. This problem can be solved by bringing the business logic into the IoT device itself, for example the camera, this way you can take some decisions without having to communicate with the cloud, and the latency problem gets solved. Bringing the logic to the end device also helps with relability, since there are less points of failure this way (communication may fail between nodes in a network).  Of course you need more computing power on the device in order to employ similar solutions. Vendors could also want the user to use their business model in the cloud, so this poses a threat on this kind of solutions, since vendors would have no service to sell this way. Vendors use data to their own advantage in order to improve their devices and lock in consumers to their own brand.

IoT & Artificial intelligence are cooperating. 

Curated knowledge: take the intelligence from where it is and mimic the way people think. Curated knowledge needs a reasoner in order to make inferences and huge databases. Some curated knowledge examples are propositional and predicate logic, productions rules and semantic networks. 

Analysing heterogeneous time series taken from sensors is almost impossible with curated knowledge: data is fast flowing, noisy, missing, redundant, and so on. For this reason it's an estabilished approach to analyse this data with machine learning. This way, humans are transitioning from "writing code" to "supplying data". There are several paradigms for machine learning: unsupervised, supervised, and reinforcement learning. The right approaches for data coming from sensors is to use supervised and reinforcement learning techniques. 

Classifiers obtained can be embedded into low-power devices. 

IoT $\rightarrow$ Fog $\rightarrow$ Cloud 

We can also let devices talk to near (similar devices) with a wireless sensor network (WSN). I can also push processing capabilities into each one of these devices.

At the edge of a typical enterprise networks there's a network of IoT-enabled devices that talk either to fog nodes or to cloud nodes. Fog nodes can be used to reduce pressure (amount of data, mainly) to the cloud nodes. The Core network stands between fog nodes and cloud nodes and enables communications between them. 

IoT can also be paired with blockchain, which can provide a single point of truth: it is shared and tamper-evident. The blockchain can be used to decentralize IoT storage into a distributed ledger. This can reduce maintenance costs and provides trust in data produced this way. The blockchain can be used as a shared ledger between companies in a supply chain in order to certify intermediate steps (smart contracts can be used).

---

### Lecture 3 - Interoperability

Often, finding a solution for an IoT problem is not that hard, you can design your solution bottom up, from the hardware layer to the application layer. This is called **vertical silo**, the problem is that the solution will only work on your devices and any change or update would require your intervention. Also, other vendors cannot interface with your solution.

There's a business model strategy behind vertical silo design: to entrap your clients with **vendor lock-in**. You prevent your customers from using the products of another manufacturer by forcing very high cost in order to migrate to another vendor. 

In the past the problem was only at hardware level, but now it is moving towards the application level (you cannot export/import you historical data from different vendors, for example).

The solution to the vertical silo/vendor lock-in problem is to introduce standards.

#### Wireless technologies & standards

Theres a sort of dichotomy between communications range and exchanged data rates. Important standards for IoT are **LORA** (which was built to address smart city applications), **Zigbee** (which can build very large networks and also supports point-to-point communications), **Bluetooth** (has a lot of different versions such as BLE ad BT5, and works in a lot of different context and applications, but cannot work with very large networks), **IEEE 802.11 standards (WiFi)** it's a family of standards, and has had a lot of iterations which improved each time.

**IEEE 802.15.4 standard** is a standard defining both physical and MAC layers. It is used as a foundation for **Zigbee**, which builds on top of it defining higher network layers and applications interface. Zigbee is an industrial consortium whereas the 802.15.4 standard is promoted by the IEEE. Zigbee supports multi-hop deployments.

**Bluetooth** has an higher data rate than ZigBee and lately it's becoming a competitor to it with **BLE (Bluetooth low energy)**. Bluetooth is mainly used for personal and multimedia communications.

**Cellular network** evolved to these days into 4G networks, which have very high bandwidths and very low latency. GSM and GPRS are still used for IoT.

 **5G** is just around the corner, though, and will change the way IoT stuff works (at still partially). 5G has better performance in all areas when compared to 4G, it is ultra-reliable, uses low-latency communications and supports massive machine type communications (which is basically IoT).

#### Why Standards?

The main motivation is a reduction of the costs for developing a technology. Standardisation happens when a tecnology becomes mature since the big revenues move somewhere else and there's no interest in investing in the development of the technology anymore. Without these tenets standardisation fails.

This produces a "coopetition" between vendors (cooperation/competition): they all help in developing the technology and updating the standard, competing on some other aspect of the business model.

When none of the proposed standards has become the "de facto" standard, the main problem becomes that of interoperability, since we've got a lot of different standards all deployed at the same time. Interoperability becomes a problem for standards as well, the same as with vertical silos.

The solution for the interoperability problem is to introduce **gateways**: such gateways implement the translation between different and incompatible protocols. The service gateway lets devices using different standards (speaking different languages) cooperate seamlessly by translating the protocols at application level. It maps a protocol's behaviour into another one's. 

There are different types of gateway:

- (A configuration) Same vendor and same protocol
- (B configuration) Different vendors and same protocol
- (C configuration) Different vendors and different protocols
- (C/II Configuration) Google Home, Alexa, works by enforcing the usage of the Google or Amazon assistants' APIs.
- (D Configuration) Different vendors and different protocols, distributed integration gateways

With type C configurations there are $n \times (n - 1)$ mappings from one protocol to another one that a gateway should be able to manage, since it is a bidirectional mapping, while on the other hand with a type D only $n$ mappings are needed in order to translate all protocols into the one of the distributed gateways. This makes the D configuration very good for interoperability.

#### Security in IoT

IoT devices are different: we may have constrained or unconstrained devices wrt to processing power or other resources. Devices being different, security-wise the IoT world is a nightmare.

Constraints in devices make it very difficult to actually secure them, some papers are saying that we're on the verge of a crisis point into IoT security: vendors focus on functionalities instead of security, devices are put into market as quickly and cheaply as possible, and many of these devices are completely unpatchable (the end users may have no mean of patching the devices). 

This is a great problem, especially wrt sensors, since an attacker can insert false data into the network. 

#### Cybercrime with IoT

It also happens at small scale, with ransomwares and small targeted attacks. Kits for similar attacks are available on the internet (black markets) for very cheap amounts of money, so everyone could in fact buy and use them.

IoT devices have security and privacy requirements. Most of the requirements are implemented into the gateway which is the most powerful device and has a central position, being able to secure all the IoT network. This is why **security requirements focus on the gateway**. 

Requirements may be difficult to achieve because of the aforementioned constraints of the devices. Also, requirements make several references to privacy, this is due to the fact that some of the IoT devices can be used to extract a lot of useful informations on their users/wearers.

---

### Lecture 4 - IoT protocol stacks

We will see two protocols, MQTT and Zigbee.

#### MQTT

It is based on the publish-subscribe model, it is used to apply the publish/subscribe model to IoT applications, and it has also extra features.

Since things must be connected to the internet in order to become "IoT devices", they must implement an internet protocol suite: such as IP at network layer, TCP/UDP at transport layer, and some protocol at application layer.

The standard stack using HTTP is too demanding for IoT devices and their limited capabilities, we also have some specific requirements that are not covered by the standard internet suite that must be addressed when deploying IoT devices. That's why we need a different protocol.

**MQTT** stands foo "message queueing telemetry transport", it is a very lightweight publish/susbscribe reliable messaging transport protocol. It has a very small code footprint, uses a low amount of bandwidth and has minimal packet overhead (this guarantees better performance when compared to HTTP).

MQTT is an OASIS standard, it's been around since the 90s, and build on top of TCP/IP, using **port 1883** (**8883 when using MQTT over SSL**, but SSL adds a significant overhead!)

- Uses a Client-Server architecture
- Implements a publish/subscribe paradigm
- It is simple on the client-side (and complex on the server-side), this is very important since IoT devices will operate as clients.
- It provides Quality of Service (QoS) data delivery
- It is data agnostic
- It is suitable for Mobile To Mobile (M2M) and IoT applications.

#### Recap on publish/subscribe paradigm

The main actors are publishers and subscribers, which are both clients, and they do not know each other. This is implemented by an event service (AKA broker), which is a server that knows both the publishers and the subscribers.

Publishers produce events (or any data that might be shared by means of events). They interact only with the broker.

Subscribers express the interest for an event, or a pattern of events, in order to get notified when such event occurs. They interact only with the broker as well.

Publishers and subscribers are fully decoupled in time, space, and synchronization.

The broker knows publishers and subscribers, receive messages from the publishers, filters and distributes them to the subscribers, and also manages the requests of subscription/unsubscription.

A publish/subscrive interaction can be implemented in many different ways, in the case of MQTT the broker is an independent server.

**Space decoupling**: publisher and subscriber do not need to know each other and do not share anything, they don't need to know each other's IP address and port, for example.

**Time decoupling**: publisher and subscriber do not need to run at the same time

**Synchronization decoupling**: operations on both publisher and subscriber are not halted during publish or receiving (no need to implement flow control).

**Scalability**: it is better than the usual client/server approach, but with this paradigm scalability is entirely up to the broker. the good thing is that the broker can be easily parallelized and it is event driven. In order to slae to a very large number of devices, some degree of broker parallelization may be needed.

The messages can be filtered by the broker according to various criteria:

1. **Based on a subject topic** (which is part of the message, clients subscribe for a specific topic and typically topics are just strings)
2. Based on the content (clients subscribe for a specific query, for example temp>30°, the broker filters the messages based on a specific query, this way data cannot be encrypted though!)
3. Based on type (events get filtered on both their content and their structure, the type refers to the type/class of the data. This requires tight integration of the middleware and the language, usually an O.O. one)

**MQTT only uses the first approach**.

In order to use the first approach, pub/sub need to agree on the topics beforehand. Also, publishers cannot assume that somebody is listening to the messages (messages may not be read by any subscribers).

Pubs/subs need to know the hostname/ip and port of the broker in order to connect to it.

In most applications the delivery of the messages is mostly in near-real-time, however the broker may also store messages for subscribers that are off-line, but the off-line subscribers need to have been connected with a persistent sessione and they should have already subscribed to the topic.

MQTT decouples the synchronisation:

- most client libraries work asynchronously (they are based on callbacks)
- synchronization is still possible if needed, by means of synchronous APIs

MQTT is easy to use on the client-side, since the complexity is on the broker-side. This is the main reason why it is well suited for low power devices. As already stated it is based on Subject-based filtering, there's a hierarchy of topics and needs a careful design that leaves space for future extensions.

There are three QoS levels for the messages: 0, 1, 2.

A client connects to a broker by sending a **CONNECT message**, that includes:

- A Client ID (unique string that identifies the client, it can also be empty, in the latter case the broker assigns a clientID, and does not keep a status for the client)
- an optional Client Session (False if the client requests a persistent session. The broker will store all subscriptions and missed messages for the client, as long as the messages are at QoS level 1 or 2. If there was a previous session it is resumed, and after the disconnection the broker and the client will store the state of the session. True otherwise, andin this case the broker cleans all the information of the client regarding previous sessions)
- an optional Username/Password (no encrypyion, unless security is used at transport layer)
- optional Will flags (if present, the broker will notify other clients in case of an ungraceful disconnection)
- optional KeepAlive (The client commits itself to sending a control packet to the broker with a keep alive interval, expressed in second in a 16-bits word. It allows the broker to detect whether the client is still active. KeepAlive = 0 turns off this mechanism)

The CONNECT message gets acknowledged by the broker via a CONNECTACK message, which confirms whether or not the connection was successful. The CONNECTACK also informs the client if there was a persistent session with that specific client, in the client asked for a persistent session.

After connecting, a client can publish messages. Each message contains a topic and a payload.

How is a **PUBLISH message** formed?

- packetId, with an integer, which is 0 if the QoS level is 0 (with QoS 0 you do not need to specify a packetId)
- topicName, which is a string possibily structured in a hierarchy such as "home/bedroom/temperature", delimited with "/"
- qos, either 1, 2, or 3
- payload (the actual message in any form
- retainFlag, which tells the broker if the message has to be stored as the last known value for the topic (this way a subscriber that connects later will get this message)
- dupFlag, which indicates that the message is a duplicate of a previous, unacked message, which is clearly meaningful when QoS is either 1 or 2.

When a broker receives a message, it immediately acknolewdge it, then it processes it (in order to identify its subscribers), then it delivers the message to its subscribers.

The publisher leaves the message to the broker, and doesn't know whether there are any subscribers and whether or when they will receive the message.

A **SUBSCRIBE message** contains:

- packetId
- topic1, which is a string that must match with publish messages
- qos1, which can either be 0, 1, or 2

topic and qos are repeated in a list for all topics to subscribe (so we would have <topic2, qos2>, <topic3, qos3>, and so on)

The broker acknowledges the Subscribe with a SUBACK message, which contains a packetId (the packedId of the ack'd message) and a number returnCode[s], one for every subscribed topic (with 128 indicating failure and 0, 1, or 2 indicating success with the corresponding maximum QoS granted, which can be lesser than the requested QoS.)

A client can unsubscribe a topic using an **UNSUBSCRIBE message**, which contains a packetId and the list of topics to unsubscribe from. Unsurprisingly, the message is ack'd with an UNSUBACK message, containing a packetId field, which is the same as that of the UNSUBSCRIBE message.

Some **wildcards** can be used with the hierarchies in the subscribe messages, for example:

- home/firstfloor/**+**/presence selects all presence sensors in all rooms in the first floor
- home/firstfloor/**#** selects all sensors in the first floor

With some versions of MQTT, you can also subscribe to topics reserved for internal statistics of MQTT, beginning with a "$" character. They are published by the broker itself and cannot be published by clients. Some examples are:

- $SYS/broker/clients/connected
- $SYS/broker/messages/sent
- $SYS/broker/uptime 

and so on.

There are no specific rules for the topics, so the hierarchy must be devised by the programmer, there are some best practices though:

- do not initiate a topic with a "/"
- do not use spaces
- keep topics short enough, as these are actually sent in the messages and add overhead to the communications
- use only UTF-8 ASCII characters
- sometimes it is useful to embed the clientID (or an unique identifier) in the topic, such as "sensor1/temperature". Of course only the client with the same clientId would be able to publish such a topic, but this is left to the programmer's design.
- use hierarchies of topics that are easily extendible
- prefer specific topics to generic topics, for example home/livingroom/temperature
- do not subscribe to all messages using #, since this could produce a very high workload, not easily supported by a client (and by the network itself). Accessing all messages could still be useful in order to store them in a DB, though.

#### QoS in MQTT

It is an agreement between the sender and the receiver of a message, in MQTT it is between the clients and the broker. There are three level of QoS as already stated: 0, 1, 2. QoS is used both between the publisher and the broker and between the broker and the subscriber.

**Qos level 0** sends a message only once, it is a "best effort" delivery. Messages are not ack'd by the receiver and when used betweeen publisher and broker, are not stored by the broker (only immediate forward policy is supported). it provides the same guarantee as the TCP protocol, that is, the delivery is guaranteed as long as the connection remains. If one of the two peers disconnects there's no guarantee anymore.

**QoS level 1** means the message is sent at leat once, messages are numbered ans stored by the broker until they are delivered to all subscribers with QoS level 1. Each message is delivered at least once to the subscribers with QoS 1, but a message may be delivered more than once. Subscribers send acknowledgements in the form of PUBACK packets.

**QoS level 2** means exactly once.It is the highest QoS level in MQTT, it is the slowest as well, it guarantees that each message is received exactly once by the recipient, using a double two way handshake. Requires using PUBREC and PUBREL packets.

QoS levels can different between publisher and broker and between broker and subscriber. Messages sent with QoS 1 or 2 are always stored for off-line clients.

The following are the best practices regarding QoS:

- use QoS level 0 when
  -  the connection is stable and reliable,
  -  a single message is not that important or it gets stale with time
  - messages are updated frequently and the old ones become stale
  - there's no need of a queue for offline receivers
- use QoS level 1 when you need all messages and subscribers can handle duplicates
- use QoS level 2 when you need all emssages and subscribers cannot handle duplicates. Level 2 has twice the overhead wrt level 1 (which has twice the overhead wrt level 0)

---

### Lecture 5

#### MQTT Persistent sessions

Persistent sessions keep the state between a client and the broker. If a subscriber disconnects, when it connects again doesn't need to subsribe again to the topics. The session is associated to the clientId defined with the CONNECT.

What is stored?

- all subscriptions
- all QoS 1 & 2 messages that are not confirmed yet
- all QoS 1 & 2 messages that arrived when the client was offline

A persistent session must be requested at CONNECT time. The cleanSession flag is involved, and the CONNACK message confirms wheter the session is persistent.

Also clients have to store state in a persistent session:

- all messages in a QoS 1 & 2 flow, not acked by the broker
- all received QoS 2 messages not confirmed by the broker

Messages of persistent sessions will be stored as long as the system allows it.

Persistent sessions should be avoided:

- for publishing-only clients that use only QoS 0, 
- if old messages are not important
- if you can afford to miss some data

#### Retained messages

A publisher has no guarantee that its messages are actually delivered to the subscribers, you can only guarantee the deliver to the broker, with QoS 1 or 2

When a client connects to the broker and susbscribes a topic, it does not know when it will get any message, it depends on when the publisher will publish messages, it can take a lot of time as well!

When a publisher sends a message with the retainFlag = True to the broker, the message is stored. If a new retained message of the same topic is published, the broker will keep the last one.

When a client subscribes the topic of the retained message the broker immediately sends the retained message for that topic. 

Retained messages are NOT persistent sessions, they are kept by the server even if they had already been delivered.

To delete a retained message, is sufficient to publish a retained empty message of the same topic.

Retained messages especially make sense for topics that get updated infrequently, for example devices which are either ON or OFF, this way all subscribers will easily know if the device is on, even if they connect at a later date.

#### Last will & testament

Last will & testament is used to notify other clients about the ungraceful disconnection of a client.

At CONNECT time, a client can request the broker a specific behaviour about its lasti will. The last will is a normal message with topic, retained flag, QoS, and payload. 

The last will is stored by the broker,and, when a client abruptly disconnects, it is sent to all subscribers of the topic specified in the last will message.

If the client instead sends a DISCONNECT packet, the stored last will is discarded.

The last will is sent if:

- There's an I/O network error
- The client doesn't send the KeepAlive message in time
- The client closes the connection without a DISCONNECT
- The broker coleses the connection with the client because of a protocol error

The last will is specified in the Connect message, in the following fields:

- lastWillTopic 
- lastWillQoS
- lastWillMessage
- lastWillRetain

The last will is often used along with retained messages: for example a crashing device with ON/OFF behavior, could send a last will with an OFF payload to all its subscribers.

#### Keep Alive (heartbeat)

It is a simple mechanism to assure that a client is still active.

The client sends periodic "I'm alive" messages to the broker, the frequency of these messages is declared in the CONNECT message. The keep alive message must be sent by the client before the expiration of the interval set with the CONNECT, otherwise the broker treats the client as if it abruptly disconnected (possibly sending out its last will).

The client sends PINGREQ messages, while the broker answers with PINGRESP.

#### MQTT Packet format

- Fixed header
- Variable header (packet identifier, present in all packets except CONNECT and CONNACK, and PUBLISH if $QoS = 0$. It contains other infrmation depending on the packet type as well, such as protocol name and version, plus a number of flags in the case of a CONNECT packet)
- Payload (contains additional information)

#### MQTT Competitors

The main issue with MQTT is that it relies on TCP, which is not particularly simple and lightweight, especially for low powered devices. Also, the broker is a single point of failure. 

An alternative to MQTT is using HTTP, but it has more problems than advantages, so overall it is not a great competitor.

Another option is to use Constrained Application Protocol (CoAP), which is designed for M2M (machine to machine) applications with constrained nodes and networks. CoAP is rapidly growing, and uses UDP underneath. CoAP does not need a bridge such as the broker in MQTT: nodes can communicate with each other (or with the cloud) directly (still, a bridge is somewhat supported if you want to).

- CoAP is based on a client/server paradigm, where sensors/actuators are servers and applications are clients.
- It uses a REST model: clients access resources by means of GET, POST, PUT, DELETE.
- It works similar to HTTP but builds on top of UDP/IP instead
- It embeds strong security mechanisms
- It uses URIs to describe network nodes

CoAP works with 8-bit controllers with small amount of ROM and RAM, and with contrained networks such as 6LoWPANs (with a typical throughput of 10(s)kbit/s)

CoAP's main strengths are:

- Native UDP
- Multicast support
- Security
- Async communications supported as well (as in MQTT)

Its main weaknesses are:

- The standard's maturity
- A not-so-sophisticated message reliability mechanism, somewhat similar to MQTT's QoS.

#### MQTT vs CoAP

- Both suitable for IoT applications
- MQTT particularly suitable for very low power devices
- pub/sub model of MQTT allows a full decoupling of producers and consumers.
- Security in CoAP has no match in MQTT.

#### The ZigBee standard

It is a standard for wireless sensor networks.

The main requirements are:

- The network needs to be completely autonomous, no human interventions.
- Very long battery life
- Low data rate
- Interoperability of ZigBee devices from different vendors

the main features are:

- Standard-based
- Low cost
- Devices can be used globally (worldwide)
- Reliable and self healing
- Supports large number of nodes
- Easy to deploy
- Very long battery life
- Secure

ZigBee is closely related to IEEE 802.15.4 Standard, it works on top of it at application layer and network layer, while  IEEE 802.15.4 works at MAC layer and Physical layer.

IEEE 802.15.4 is a specification of the physical and MAC layers for low-rate Wireless Personal Area Networks (PAN). It is infrastructure-less, supports short range, supports star and P2P technologies. It can coexist with Bluetooth.

ZigBee is built on top of IEEE 802.15.4, it specifices network and application layers.

The application layer comprises:

- The Application Framework (with a maximum of 240 APOs, Application Objects. Each APO is an user defined ZigBee application)
- The ZigBee device Object (ZDO), which provides services to let the APOs organize into a distributed application
- The Application Support sublayer (APS), which provides data and management services to the APOs and ZDO.

Layers in the ZigBee stack communicate by mean of primitives. The standard workflow is $request \to indication \to response \to confirm$

#### ZigBee network layer

There are three types of device:

- The network coordinator
- Routers
- End-devices

With ZigBee you can configure Star, Tree, or Mesh networks.

---

### Lecture 6

#### Network layer cont'd

The network layer works with a series of primitives, used to offer services to the application layer.

Before doing anything a device must be part of the network. It has two ways to do so: creating a new network (in this case the device becomes a ZigBee coordinator) or join an existing one (becoming a router or end-device). The role of the device is chosen at compile-time.

**NETWORK-FORMATION** is the primitive that a device acting as coordinator can invoke in order to create a new network. The network layer calls the underlying MAC layer, in order to look for the best available channel (the least noisy). After this, another call is carried out to the MAC layer, in order to check for other networks in the neighbourhood.

The MAC address of each device doesn't appear in the headers of ZigBee packets, this is made in order to save up space, because the devices are very low powered and the network has low throughput.

How to join a ZigBee network? There are two ways to do so:

- **Join through association**: initiated by a device wishing to join an existing network
- **Direct join**: requested by a router or by the coordinator to request a device to join its PAN

#### ZigBee application layer

It is comprised by:

- The Application Framework
- The ZigBee Device Object (ZDO)
- Application Support Sublayer (APS)

The Application Framework permits up to 240 APOs (Application Objects). Each APO can be used to get or set parameters: it acts as an endpoint.

The Application Support Sublayer is a sort of transport layer. It provides:

- Data service 
- Management

A ZigBee device can run multiple applications.

APS is divided into clusters identifying various aspects of each device. Cluster identifiers are used to tell which operations are available.

Application Profiles (and Profile IDs) are used for identifying applications

Device IDs: their main purpose is to make ZigBee more human-friendly.

**[skipped some stuff, check again later]**

