## ICT Risk Assessment

---

### Lecture 1

Systems will be attacked. If you believe otherwise you're simply wrong. Many attacks are only discovered after years.

Cloud $\rightarrow$ Fog $\rightarrow$ IoT 

With public cloud you may be using the same resources of someone that wants to attack you. The puclic cloud is a nightmare wrt security problems.

Security triad:

- Confidentiality
- Integrity
- Availability

**Vulnerability** is a first key concept for security. It can be an error, a bug either in a person, a component, a set of rules, that makes it possible to violate a security property. So a bug enables an attack. All vulnerabilities are bugs, but not all bugs are vulnerabilities.

**Threat agent** is a second key concept for security and is defined as a source of attacks.

**Intrusion** is a sequence of actions and attacks to illegally control an ICT system. A program can implement some actions (exploits).

**Unconditional and Conditional security**

**Risk analysis**

1. Asset analysis
2. Vulnerability analysis
3. Attack analysis
4. Threat analysis
5. Impact analysis
6. Risk management (Classifying risk, define acceptable risk, select and implement countermeasures)

---

### Lecture 2

**Asset analysis**

Which are the important resources that we are going to defend? Who is entitled to access those resources?

**Risk analysis and management** 

Not all attacks are worth preventing, and solutions are economy driver. There are very few complete and quantitative methodologies for this, and several are under development.

**Attack and intrusion**

**Intrusion** is the whole sequence of ations of the attacker to reach a goal

An **Attack** is a single action

**Local vs Remote attack**

A local attack can be executed only if the attacker has already an access/account on the node. (the attacker need a foothold on that specific node)

An attack is remote if it can be executed from another node even if the attacker has no local account

**Automated attack** needs no human action, it can be executed just by running an exploit. It's the most dangerous kind of attack since the time to execute it is neglectable, and an attacker with no know how or abilities can execute an exploit. An attack platform is a software tool to implement an intrusion without involving a human. There's a great difference between running and coding an exploit.

A **malware** is a software designed to attack a system and install some other software on an automated way. If some user cooperation is required in order to install the malware, the attack is a form of phishing. In this case the attack vector is a human. A **Payload** is a software module installed on a node by the attack vector at the end of the attack.

**Kill chain**: sequence of action you need to do in order to implement an intrusion 

1. Collection of information about a system (fingerprinting)
2. Discovery of system vulnerabilities (can be automated)
3. Search or build of a program (exploit) to implement the attack (even partially)
4. Implementation of the attack (Execution of the exploits + execution of human actions)
5. Install tools to control the system (in order to persist on that system)
6. Remove any attack trace on the system
7. Access, update, control a subset of the system information

In reality the steps of the chain are much more interleaved. 

**Command & control** theory about remotely controlling software deployed in an attack without generating too much "noise" (without being discovered). 

Cryptography CAN simplify Security but IS NOT security by itself.

Safety $\neq$ Security: safety refers to safe states in a system, while security depends upon the probability that an attacker succeeds in entering the unsafe state of that system.

The standard solution for safety is module redundancy (3 or 5), but if a module is affected by a vulnerability then the attacker has more opportunities to be succesfull in attacking the module.

**Red team exercise aka penetration testing**: you pay someone for attacking your system, but the approach is inconsistent since you cannot be sure that: 

- Your improvement is effective (Braess paradox)
- The read team has found all the possible attacks
- A red team failure has a large number of reasons...

**Stack overflow**

---

### Lecture 3

#### Structural Vulnerability

TCP/IP can be used as an example of structural vulnerability. TCP/IP's main goal is availability, there's some mechanism defined to discover which nodes are alive and reachable, but there's no mechanism available to guarantee or authenticate the source of the messages.

A node can send an Echo message to chech if another node is alive and reachable. The sender can specify a partial ip address and broadcast the message to check a set of nodes. There's no control on the fields of an IP packet a node sends.

Broadcast Echo messages can be used in order to trigger a **Distributed Denial of Service** or DDoS: a sender can fake its address in order to make other nodes in a network reply to target node, this way the node gets flooded by the echo messages sent by other nodes in the network.

IoT devices have been used in the past for this kind of attacks.

#### Security as an holistic property

- The security of a system is not implied by the one of each of its modules
- The overall system may be unsecure even when each module is secure
- In a virtual machine hierarchy the security of a machine may be destroyed by a vulnerability in an underlying machine

DDoS impact depends upon the number of zombie nodes whose address matches that in the message, and may be amplified by further messages. DDoS is a structural vulnerability.

#### Design approaches vs vulns

When designing and building a system we may adopt one of two approaches:

- Pretend there are no vulnerabilities in the components (penetrate & patch)
- Be aware that there are vulns and try to anticipate them even if we still do not know which vulnerabilities (proactive or predictive approach)

In the **penetrate & patch** approach there's a competition between discovering and exploiting vulnerabilities vs patching the system to remove them. A security patch is the change applied to an asset to corret the weakness described by a vulnerability. Patches change the module's behaviour, sometimes you have to remove some "good" behaviour in order to fix a vulnerability. Some systems cannot be patched because they're certified and a patch invalidates their certification. These systems are not patched very often.

Most vulnerabilities are not exploited, this is the main reason for conditional security. We should not remove ALL the vulnerabilities, since most vulnerabilities are there but are not worth writing an exploit for. It's important to understand if a vulnerability will really be exploited.

#### Life cycle of a vulnerability in a penetrate and patch world

1. The vulnerability is born
2. The vulnerability is discovered
3. Both the vulnerability and an exploit that takes advantage of the vulnerability are discovered
4. Both the vulnerability and a patch that removes the vulnerablity are discovered (a race with 3)
5. The vulnerability, the exploit, and the patch have been discovered.

Usually, when a patch is available, a vulnerability gets exploited much more, since almost everyone can write an exploit for the vulnerability. This until the patch gets applied, at which point the vulnerability dies.

A vulnerability can survive dormant in the code for years before it gets discovered.

#### Zero day exploit

It is an exploit for a vulnerability that has been discovered but not disclosed to all the users. Sometimes those who discover a vulnerability sell it to those interested in attacking the system (black market of vulnerabilities).

Sometimes a system is attacked even if a vulnerability is in the last status i.e. a patch is available. This is due to the fact that a lot of system owners do not apply a patch, even if it is available. There's an asymmetry between the owner and the software supplier.

In the best, case a patch is available before an attack is known.

Everytime someone buys a zero day, he's interested in preserving the life of the vulnerability in order to have it for longer (and not to loose money), so selling zero days makes the world less secure overall.

People are looking for vulnerabilities in popular modules, scarcely used modules have less known vulnerabilities but this doesn't mean they're actually free from them, this means that the number of disclosed vulnerabilities cannot be used to evaluate the quality of the module code.

#### Genetic difference

A system is more robust if it composes modules from distinct suppliers. The voint existence of vulnerabilities and a monopoly in the module supply results in several problems because:

- All the instances of a module are affected by the same vulnerability
- The same vendor tends to repeat a vulnerability

#### Defence in depth

Any system component can be affected by a vulnerability, a security expert: 

- Does not need to know any vulnerabilities
- Can design a system so that the discovery of a vulnerability in a component does not make the whole system useless
- Layered defence or defence in depth = redundancies and diversities in the controls
- Proactive approach vs penetrate and patch

We should be able to assess the risk of each vulnerability in each system