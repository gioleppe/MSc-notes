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

One of the main problems wrt performance is latency: roundtrip times could have an impact on critical applications such as alarms and security cameras. This problem can be solved by bringing the business logic into the IoT device itself, for example the camera, this way you can take some decisions without having to communicate with the cloud, and the latency problem gets solved. Of course you need more computing power on the device in order to do so. Also, vendors could want the user to use their business model in the cloud,so this poses a threat on this kind of solutions, since vendors would have no service to sell this way. Vendors use data to their own advantage in order to improve their devices and lock in consumers to their own brand.

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

Theres a sort of dichotomy between communications range and exchanged data rates. Important standards for IoT are **LORA** (which was built to address smart city applications), **Zigbee** (which can build very large networks), **Bluetooth** (has a lot of different versions such as BLE ad BT5, and works in a lot of different context and applications, but cannot work with very large networks), **IEEE 802.11 standards (WiFi)** it's a family of standards, and has had a lot of iterations which improved each time.

**IEEE 802.15.4 standard** is a standard defining both physical and MAC layers. It is used as a foundation for **Zigbee**, which builds on top of it defining higher network layers and applications interface. Zigbee is an industrial consortium whereas the 802.15.4 standard is promoted by the IEEE. Zigbee supports multi-hop deployments.

**Bluetooth** has an higher data rate than ZigBee and lately it's becoming a competitor to it with **BLE (Bluetooth low energy)**. Bluetooth is mainly used for personal and multimedia communications.

**Cellular network** evolved to these days into 4G networks, which have very high bandwidths and very low latency. GSM and GPRS are still used for IoT.

 **5G** is just around the corner, though, and will change the way IoT stuff works (at still partially). 5G has better performance in all areas when compared to 4G, it is ultra-reliable, uses low-latency communications and supports massive machine type communications (which is basically IoT).

#### Why Standards?

The main motivation is a reduction of the costs for developing a technology. Standardisation happens when a tecnology becomes mature since the big revenues move somewhere else and there's no interest in investing in the development of the technology anymore. Without these tenets standardisation fails.

This produces a "coopetition" between vendors (cooperation/competition).

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