
## Packet switching and Routers

When a packet reaches a router, the router checks the packet’s header and looks up the destination in a **forwarding table**. The forwarding table tells the router which **next hop** to send the packet to.

Packet is sent to the router that is believed to be closest to the destination

## Protocols

> **A set of rules for communication**

A Protocol defines:
- The roles of communicating entities
- The format of messages
- The order of messages
- The actions taken when messages are sent or received
- The actions taken when other events happen

#### Request-Response Protocols

Flow: 
1. The client sends a request.
2. The server sends a response.
```
Client  -> Request  -> Server
Client  <- Response <- Server
```

 Usually well-defined rules for whose turn it is. For more complex protocols, it may be more complex because:
 - Server is slow to respond 
 - Size of request or response can vary

#### Finite state machines (FSM)

A finite state machine describes:
- The possible **states** a system can be in
- The **events** that cause state changes
- The **actions** taken when events happen
- The transitions between states

**Example: Simplified web server state machine**

```
Wait
Receive request
Send response
```

The server starts in a waiting state. When it receives a request, it sends a response, then goes back to waiting.
![](../../../pasted_images/Pasted%20image%2020260514133152.png)

>**FSMs are useful because protocols need precise behavior. A machine needs to know exactly what to do depending on its current state and the event it receives.**

## The Internet protocol stack

The Internet is organized into layers, called the **protocol stack**. Each layer has a different responsibility. The point of layering is to separate concerns, so each layer solves one part of the communication problem.

```
Application    // operating system
Transport
Network
Link           // hardware
Physical
```

When a client sends data to a server, the data moves **down the stack** on the sender side

Then it travels through the physical medium and eventually moves **up the stack** on the receiver side:
#### Application layer

The **application layer** is closest to the user/application.
```
// Examples

HTTP / Web
	Email
File transfer
Multimedia
```

#### Transport layer
The **transport layer** handles communication between processes on machines.

This includes:
```
- Identifying the process on the machine
- Maybe identifying a resource within the process, such as a browser tab
- Ensuring data arrives in order, if required
- Recovering lost data, if required
```

Some examples are TCP and UDP

The transport layer uses things like **port numbers**. The network layer may get data to the correct machine, but the transport layer helps get it to the correct process on that machine.

> Analogy: making sure the message reaches the correct person, not just the correct building.

#### Network layer

The **network layer** is responsible for routing data through routers to the destination machine.

This protocol usually uses **IP Addresses**

#### Link layer 

The **link layer** moves data between adjacent machines on a direct connection. It routes frames to adjacent machines.

Example:
- Ethernet

The important address here is the **MAC address**.

The network layer thinks globally: “How do I reach the destination machine across networks?”

The link layer thinks locally: “How do I get this frame to the next directly connected device?”

#### Physical layer

The **physical layer** handles the actual transmission over the physical medium. encodes data appropriately for the physical medium.

This layer deals with the actual signals moving through Wi-Fi, copper cables, fiber, or other media.

#### Encapsulation

Each layer wraps the data from the layer above with its own header. This means the naming changes as data moves down the stack:
```
Application data = message
Transport data   = segment
Network data     = datagram
Link data        = frame
```
The structure looks like this:

```
Message: M
Segment: Ht M
Datagram: Hn Ht M
Frame: Hl Hn Ht M
```

Where:
- `M` = original message
- `Ht` = transport header
- `Hn` = network header
- `Hl` = link header

![](../../../pasted_images/Pasted%20image%2020260514143939.png)
#### Cheat Sheet
![](../../../pasted_images/Pasted%20image%2020260514143748.png)

The easiest way to remember the whole lecture:

```
Application: What does the app want to say?
Transport: Which process should receive it, and does it need reliability/order?Network: Which machine should receive it across the Internet?
Link: Which directly connected device should receive it next?
Physical: How do we physically transmit the bits?
```

And for encapsulation:

```
App creates messageTransport wraps it into segmentNetwork wraps it into datagramLink wraps it into framePhysical sends the bits
```