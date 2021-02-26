## ICT Risk Assessment

---

University of Pisa, Computer Science MSc, AY 20/21.

Lecturer: **Professor Fabrizio Baiardi**.

Notes taken by Tommaso Colella.

\newpage

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

---

### Lecture 4

Rather than collecting data about the previous attacks on a system, let's attack it ourselves. This is the so called **adversary emulation**: it is an approach meant to mimic in an automated way the action of an attacker against the system. The ability to easily repeat the attack a large number of times can support a detailed evaluation of the system robustness and resilience.

Sometimes both the success probability and the impact are approximated with ranges such as {low, medium, high}.

We also need a **Risk-matrix** to compute the risk.

There are some problems related to Risk Matrixes though. They should satisfy these lemmas, in order to satisfy weak consistency:

- **Cox's First Lemma**: a red and a green cell cannot share an edge
- **Cox's Second Lemma**: no red cell can occurr in the bottom row or left column of the matrix

3X3 and 4X4 matrixes are always equally colored when applying Cox's lemmas, so they are not really useful.

Another critical problem is that changes and breakthroughs in technologies can invalidate an change the vulnerabilities.

#### Return on investment (ROI)

It's not meaningful to spend a huge amount of money to prevent an attack which has a very low impact (or very low success probability). The countermeasures should focus on attacks with large success probabilities and/or large impact. Even then, there are **Black swans**, attacks with a very big impact but a somewhat low probability (it's possible that we do not know how to efficiently measure a probability for these), that can really disrupt a system.

ROI is the difference between the overall risk before the countermeasures and the overall risk after the adoption of countermeasures. The difference arises because of a lower success probability and/or a lower impact of an attack.

The case where a vulnerability is removed or patched is a particular one.

There are two ways to evaluate the ROI: The simplest one is that the difference between before and after is positive (larger than zero), another approach is to use ratios (in which case the ratio must be >1 after the countermeasures).

#### Risk Based Approach recap

1. Asset Analysis
2. Vulnerability Analysis
3. Attack Analysis
4. Threat Analysis
5. Impact Analysis
6. Risk Evalutation
7. Risk Management (which countermeasures are to be adopted)

7 can be present or not (we might be interested in not adopting any countermeasures for low impact/success rate attacks)

The Risk Based Approach is the most modern one for ICT security.

#### Asset Analysis

We need to discover the assets that result in an impact if successfully attacked. This implies to discover which ICT resources an organization needs to work in an efficient way.

 The main steps are the following:

1. Discover the fundamental business process
2. Find out the critical ICT resources for these processes
3. Assess the impact for the organization if
   - A business process is stopped (availability)
   - The resource has to be rebuilt ex-novo (integrity)
   - The attacker discovers the information in the resource (confidentiality)

It's also important to estimate the actual value of a resource, which is usually not trivial. A possible approach is to consider the cost of rebuilding the resource if it disappears.

The first thing to do with asset analysis is to build an inventory of all the resources in the system to be protected (companies, even bigger ones, do not know what they need to protect). 

Other aspects to evaluate are:

- Externalities
- Free riding

#### Security Policy

It is a set of rules that an organization adopts both to minimize cyber risk and to define the goals of security.

- Defines the goal of security
- Defines the correct behavior of all the users
- Forbids dangerous behaviors and components

The security policy cannot violate the legislation that concerns ICT systems.

Security policies make use of the **Subject/Object abstraction**.

A subject entitled to invoke an operation of an object owns a **right** on this object. Rights may be directly or indirectly deduced from the security policy.

**Default allow**: defines forbidden behaviors and allows anything that it does not define (enumerating badness)

**Default deny**: defines legal behaviors and forbids anything it does not define (anything else)

**Default allow is very dangerous**, it should be avoided.

Mark Ranum - The Six Dumbest Ideas in Computer Security

1. Default permit
2. Enumerating badness
3. Penetrate & Patch
4. Hacking is cool
5. Educating Users
6. Action is better than inaction

#### Access Control Policies

- Discretionary access control
  - There's an owner for each object
  - The owner defines the policy (wrt subjects that can operate on the object and the rights for each subject)
- Mandatory access control
  - There is an owner but there are some system wide rules it has to satisfy (that cannot be violated)
  - It is implemented partitioning objects and subjects into classes. All the classes are partially ordered, and an owner can only grant permission to a subject only if that subject's class and the object's class satisfy a predefined condition

---

### Lecture 5 

#### Mandatory Access Control (cont'd)

- A subject in a class C may be enabled to
  - Read any file with a class lower than or equal to C
  - Write any file with a class equal to C
  - Append a record to a file with a class larger than C
  - The owner of the file can grant the rights provided that the three previous rules are satisfied

Mandatory access control is useful to prevent information leakage. Partial order comes from the military world.

#### Security policies

The **no write down** policy is used in order to avoid information leaking issues. Its main problem is that information may flow only at an higher level. To address this problem, a further operation is introduced to periodically desecretate information to the lower levels, but this operation is the ideal target for an attacker.

**Bell-LaPadula Policy**: "no read up, no write down"

When you're interested into integrity instead of confidentiality, the security policy should adopt a **no write up** approach. In this case a subject in a class C may be enabled to write any file with a class lower than or equal to C, and read any file with a class larger than or equal to C. This policy is called **Bida Integrity Policy**.

In some cases integrity is much more important than confidentiality.

**Watermark policy**: every subject has a maximum level, but is not fixed, it is the highest one of the objects it has worked on. The level increases as the subject reads critial information. The increase is monotonical, no decrease is possible. The policy is time dependent, and was introduced to minimize the flowing of information at higher levels.

**No interference property**: a system satisfies the property if the labels associated with each object do not change after the removal of a subject with different (higher or lower) level that accessed those resources.

**Clark-Wilson policy**

**Chinese Wall policy**: objects are partitioned into classes, as soon as a subject invokes an operation on an object 

- It cannot invoke operations on objects in distinct classes
- it can invoke operations on objects in the class

This is made to avoid conflict of interest. The policy is time dependent and can be integrated with both DAC and a MAC.

Real policies could be made up of various multiple ones, and there could be two levels for subjects as well: one for integrity and one for confidentiality.

#### Trusted Computing Base

includes any component that is involved in the implementation of the security policy. These components are highly critical since if there's a defect in the TCP, that defect/bug is a vulnerability.

Any system needs to trust all the TCB components. Assurance of these components is very important.

The smaller the TCB, the better for a series of reasons:

- less code means less bugs (statistically)
- less code means that correctness can be proven by applying formal methods in a much simpler way.

#### Vulnerability Analysis

What is a **vulnerability**? (recap)

A defect in one system component or in the way the component is used.

By exploiting the bug, a threat agent can fire an unexpected behavior of the component.

Several taxonomies have been proposed for vulnerabilities.

A Vulnerability could be located in various places, such as:

- Actions that are executed (procedural)
- People executing the action (organization)
- Hardware or software tools (ICT tools that are used)

About vulnerability in tools, there's a further taxonomy classification:

- Specification
  - You may use a library with more functions than the required ones. If someone succeeds in invoking some of the "useless" functions, anomalous behaviors may arise. This kind of vulnerability could be introduced with code reuse, since there could be some vulnerabilities in the code that is reused.
- Implementation 
  - There could be missing control on the user input, the root cause is the user's ability to provide malformed input to the code. These vulnerabilities are strongly dependant upon the native control in the language type system and in the run time support.
- Strutural
  - These vulnerabilities arise when a component works in isolation, but doesn't work correctly when composed in a system. This way trust may be violated, since some components may delegate security checks to other ones.

There's also another type of classification based on the attacker's point of view, either who can implement the attack:

- Those who own a local account $\implies$ Local vulnerability
- Those who can interact with the machine $\implies$ Remote vulnerability 

Or what can be achieved by the attack.

#### Searching for vulnerabilities

Since most vulnerabilities and exploits for standard components are well known, the search should focus on not standard components, structural vulnerabilities due to the composition of standard components with non standard ones.

Vulnerabilities in standard components should be the last ones to search for.

In order to search for vulnerabilities, a vulnerability scanner is usually employed. The vulnerability scanner is a tool that returns a set of vulnerabilities for each computer node in a network. It fingerprints the scanned system, then it accesses a database that maps each OS and application into a set of public vulnerabilities.

Vulnerablity scanning is the easiest implementation of a vulnerability analysis.

**Fingerprinting** is the main mechanism to identify the OS and it is implemented by sending malformed IP packets and see the reply. Each OS and application has its own reaction and response to a wrong packet that violates TCP/IP specifications. Several packets may be required to solve any ambiguity among distinct OSes/components.

This technique is called **active** fingerprinting, one coul also use **passive** fingerprinting, capturing packets flowing in the networks. Passive fingerprinting is much slower but doesn't produce any noise.

Applications are actively fingerprinted by analyzing open ports on the node. This kind of active fingerprinting can be confused by using a non-standard port to run an application.

A big problem with vulnerability scanners is that it could produce both false positives: a vulnerability could have been patched, the vulnerability could not be present anymore. The only way to distinguish false and true positives is to actually implement an attack that exploits the vulnerability (breach and simulation tools are used in order to do this), but this is not always possible on production systems.

Security is not a boolean world, you could always have some false positives (type I errors) and false negatives (type II errors) the accuracy is given by: $accuracy = \frac{number\ of\ true\ positives + number\ of\ true\ negatives}{number\ of\ true\ positives + false\ positives + false\ negatives + true\ negatives}$

In some cases, the number of false positives and false negatives is so large that no meaningful information can actually be found.

---

### Lecture 6

How to find vulnerabilities in non standard components? 

If we don't have any source code available, we must use some sort of black box.

A **Web scanner** is a tool used to search for vulnerabilitiesin web application (it focuses on well known vulnerabilities). It works by first crawling web pages, then it considers all the pages in isolation and emulates the way an attacker might act on that specific page (for example injecting some code into forms, or queries to check for SQL injection attacks).

**Tainting analysis**: it is a preliminary static analysis of the source code, useful to discover which instructions receive an input. It is a worst case approach: it always returns a larger set than the actual one, since it is impossible to check at static time if an input will taint a given instruction.

#### Fuzzing and fuzzer

Fuzzing is a search technique that can be applied even if the source code of a module is not available. According to Google and Microsoft, it can discover more than 80% of vulnerabilities.

The basic idea is to send malformed input to the module, if the module crashes, then the input is not controlled and a vulnerabilityis possible. 

The fuzzer automates this strategy by testing a huge amount of inputs in parallel.

**Mutation based fuzzing**: you take a good input and add anomalies to it. This requires little or no set up time. Anomalies may be generated at random or by following some kind of euristhic.

**Generation based fuzzing**: test cases are generated from some description of the format. Anomalies are added to each possible spot in the inputs. Can take a while to set up but usually provides better results than random fuzzing.

White box fuzzing is clearly more effective than black box fuzzing, since you can see and verify the code paths traversed by every malformed input. White box fuzzing allows to use a technique called **drilling**, which involves an optimized search of malformed inputs.

**Evolutionary fuzzing**: you try to generate inputs based on the program's response. You can generate test cases based on code coverage metrics, this technique is still in alpha stage though.

The main things about fuzzing are:

- Protocol knowledge is helpful
- Generational fuzzers are better than random fuzzers
- Using more fuzzers is better
- The longer you run a fuzzer, the more bugs you will find
- You guide the process, fix it when it breaks or fails to reach where you need it to go
- Code coverage can serve as a useful guide

Fuzzing can also be applied to IoT devices, in order to evaluate their reliability and vulnerability.

**Robustness of a module**: is the ability to prevent damage to the overall system even if its specifications are violated.

Violation of specifications is a generalization of fuzzing. 

The concept of robustness comes from biology. 

Robustness is a system property and it can be increased only by decreasing performance, efficient, ease of use, or some other system property. Robustness doesn't come for free.

A robustness measure is a continuous value in the range [0, 1), 1 is an asymptotic value. Total robustness is not reachable. Robustness depends upon the number of checks implemented in the program. The more checks, the more robustness tends to 1.

A compromise with the number of checks is required, since they reduce overall performance, since they're implemented through instructions such as any other instruction.

It's been experimentally confirmed that even trivial checks can improve the component robustness. Complex checks should only be adopted after the trivial ones. The most efficient checks are the ones related to data types.

We can be robust wrt intelligent attacks and/or random failures. We're interested to robustness wrt intelligent attacks.