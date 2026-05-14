
## What is the Internet
global system of interconnected computer networks that use the Internet protocol suite (TCP/IP) to communicate between networks and devices. It is a **network of networks.**
#### It's purpose and goals

-  **Integrating many separately administered networks into one common system.**
-  Continue despite network or gateway failure
-  Support multiple types of services and networks
-  Distributed management of resources
	-  No single central authority should need to manage every part of the Internet.
-  Cost effective
-  Easy host attachment, easy to connect new devices
-  Resources should be accountable
## Components of the Internet
**1) Host / End systems**
- PCs
- workstations
- servers
- smartphones
- smart toasters and fridges

These run network apps like
- web browsers
- email clients
- video streaming apps
- SSH clients

**2) Communication Links**
These are the physical or wireless channels that move data.
- fiber
- copper cable
- radio
- satellite
###### Links can vary by 
- **bandwidth**: how much data can be sent per second
- **latency**: how long it takes data to travel

**3) Routers**
Routers forward **packets**, which are chunks of data.

**4) Networks**
The Internet is made of many types of networks, like local networks, company networks, and regional network providers. These networks  connect together to form the larger internet.

## Communication Basics

Requirements:
- some kind of medium (air, wire, fibre)
- source and destination
- protocol (shared  message type/language)
- message

## Switched Network

In a switched network, devices do not all need direct links to each other. Instead, they connect through switching devices.

![](../../../pasted_images/Pasted%20image%2020260512221406.png)

This means multiple devices or data flows share the same network infrastructure.
> How can multiple conversations share the same medium without getting mixed up?
#### Multiplexing

Multiplexing means combining multiple data flows onto a shared medium. Many senders share the same link or medium.

#### Demultiplexing

The receiver separates the combined data back into the correct original streams.

**Simple example:**

Four phone calls share one physical link. Multiplexing combines them onto the link. Demultiplexing separates them back into four separate calls at the other end.


# Two ways to send data
## Circuit switching

Based on creating a **dedicated path** between source and destination before communication begins.
###### Call analogy with Alice and Bob.
Before Alice talks to Bob, the network establishes a fixed path through the switches. That path stays reserved for the connection and other users can't use the reserved capacity during the call.

![](../../../pasted_images/Pasted%20image%2020260512222258.png)
#### Properties

**Dedicated path**
- A circuit is reserved between source and destination.

**Path chosen during setup**
- The route is determined when the connection is established.

**Single stream per path**
- Each circuit carries one stream of information.

**Predictable performance**
- Because capacity is reserved, performance is more guaranteed

### Circuit Switching Multiplexing

Since many users may need to share the same physical link, circuit switching still needs multiplexing.

###### Frequency Division Multiplexing, FDM
- the frequency range is divided into narrow bands
- each call gets its own frequency band
- each call can transmit at the maximum rate of that narrow band

![](../../../pasted_images/Pasted%20image%2020260512223203.png)
 
###### Time Division Multiplexing, TDM
- time is divided into slots
- each call gets specific time slots

Think of users taking turns very quickly.

![](../../../pasted_images/Pasted%20image%2020260512223353.png)

###### Code Division Multiplexing

different representations of data
###### Orthogonal Multiplexing

combination of techniques


## Pros

1. Guaranteed Performance
	a) Once the circuit is established, resources are reserved. 
2. Immediate Data Transmission After Setup
	a)  Once the call begins, data can be transmitted without needing to make a routing decision
## Cons

1. Wastes Bandwidth for Bursty Traffic
	a) when data is sent in bursts with idle periods in between(loading a webpage, sending messages) reserved capacity sits unused during idle periods.
2. Connection Setup Time Is Overhead
	a)  Before sending data, the circuit must be established. Inefficient for short or frequent communications.
3. Poor Fault Tolerance 
	a)  If part of the dedicated path fails, the connection can break.


## Packet Switching

Data is divided into small chunks called **packets**. Each packet is sent individually through the network.

Each **packet** itself contains a header and payload. 

Packets are **independently routed** from source to destination, meaning they don't all follow the same path. They are forwarded separately with routers.

Packet switching can't **guarantee exact performance** for every packet. Instead, it gives good average or statistical performance. (which is good enough)

#### Pros

**Demand is bursty**

Instead of reserving capacity for one user, the network can let many users share the medium dynamically. When one user is idle, another user can use the capacity.

**Starting new conversations is frequent**

Packet switching avoids the need to establish a dedicated circuit for every conversation. This is useful because Internet communication often involves many short interactions.

**Improves Utilization**

because network capacity is shared dynamically.

## Circuit Switching vs Packet Switching

| Concept         | Circuit Switching                         | Packet Switching                               |
| --------------- | ----------------------------------------- | ---------------------------------------------- |
| Data path       | Dedicated path                            | Packets routed individually                    |
| Setup           | Requires connection setup                 | No dedicated circuit setup                     |
| Resource usage  | Resources reserved                        | Resources shared dynamically                   |
| Performance     | Guaranteed once established               | Statistical/best-effort performance            |
| Bursty traffic  | Inefficient                               | Efficient                                      |
| Fault tolerance | Poorer if path fails                      | Better because packets may use alternate paths |
| Best for        | Continuous streams with strict guarantees | Bursty data and many conversations             |
#### Intuition
 **Circuit Switching**

Circuit switching is like reserving an entire road lane for one car trip. Even if the car stops or drives slowly, no one else can use that lane. This gives predictable performance but wastes capacity.

**Packet Switching**

Packet switching is like many cars sharing roads. Each car has a destination and can be routed independently. There may be congestion, but the road is used more efficiently overall.