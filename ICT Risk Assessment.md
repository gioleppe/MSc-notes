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

**Buffer overflow**

