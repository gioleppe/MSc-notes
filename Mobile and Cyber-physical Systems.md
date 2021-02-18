## Mobile and Cyber-physical Systems

---

### Lecture 1

This lesson was largely a course introduction, I couldn't be bothered to actually take notes on this.

----

### Lecture 2

By 2014 the number of mobile devices surpassed the number of humans on earth.

 A lot of devices will now operate autonomously, without human input, and leveraging their sensing abilities (achieved by using sensors). IoT devices have their own business logic, and they are deployed as independent physical objects. Many of these devices are already wearables and are full of sensors. A lot of these devices will be environmental ones, such as Smart cities sensors, Alexa, and so on. There are a lot of applications for these devices (Smart cities, health, robotics, ...), that said all these devices share a similar architecture with sensors and actuators. Consumer IoT market is exploding, and will become a huge economy in a few years. 

IoT is the last development for internet and computing. IoT devices are heterogeneous, there are both consumer and industrial devices. Internet connectivity is necessary in order to support the operations on the devices. Most of the devices are simple and are only sending sensor readings to the cloud, while others are more complex and need some more computational power (such as security cameras and so on).

Sensor/actuator technology is the "fourth generation" of the internet, with respect to end systems supported.

Each IoT device has sensors/actuators, a microcontroller, a wireless interface and some software (business logic). All data collected by sensors goes to the cloud where it is stored and processed for further usage. The cloud is also used is order to lock in (bind) users to a single vendor/manufacturer. Sensors and actuators are at the edge of the cloud. 

NoSQL databases are widely used in the IoT world because of their great horizontal scalability features and simpler design wrt SQL solutions. MongoDB is one of these NoSQL databases, it uses Documents inside, written in a json-like syntax and organized in Collections.

##### Relevant issues in IoT

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

