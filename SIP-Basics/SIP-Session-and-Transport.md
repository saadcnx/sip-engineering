# SIP Communication Methods: Unicast, Multicast & Mesh

According to SIP protocols, members can communicate with each other in three ways. Let's understand all three points in a very simple IT and network engineering context.

## 1. Unicast (One-to-One)

This is the most common and straightforward method.

- **Concept:** When a single point (sender) talks directly to another single point (receiver).
- **SIP Example:** Phone A's IP address is `192.168.10.20` and Phone B's is `192.168.10.30`. When Phone A makes a call, the SIP signaling and later the RTP media packets travel directly between these two IPs, creating a unique target. The rest of the devices on the network have nothing to do with this traffic.

## 2. Multicast (One-to-Many)

This is used when resources are scarce and targets are many.

- **Concept:** The sender sends only a single packet, but it is sent to a specific **Multicast Group Address** (like `224.0.1.75`, which is reserved for SIP multicast). The network's switches/routers duplicate that packet and deliver it to all the members who have joined that group.
- **SIP Example (Intercom / Paging):** Imagine an office with 50 agents. The manager needs to make a live announcement to everyone at once. If the manager's phone creates 50 separate unicast streams, the server and network will crash. Instead, the SIP session initiates on a multicast address. The manager speaks once, and the voice comes out of the speakers of all 50 phones simultaneously.

## 3. Via a Mesh of Unicast Relations (Or a Combination)

This point is very interesting and is used in decentralized multi-party conferencing.

### Mesh of Unicast Relations (Fully Decentralized)

- **Concept:** Here, there is no central media server (like an IP-PBX or MCU). Every participant creates a separate direct Unicast connection with all the other participants.
- **SIP Example (3-Way Call on a Phone):** Imagine Phone A, Phone B, and Phone C are conferencing together:
  - Phone A will create one unicast session with Phone B and another unicast session with Phone C.
  - Phone B will also separately connect with Phone C.
  - **Result?** A "Mesh" (web) is formed. Each phone itself mixes the audio. (This is fine on a small scale, but for 10-15 people, putting that much load on a phone becomes difficult).

### Combination of These (Hybrid Model)

- **Concept:** In real-world enterprise networks, a mix of these two (unicast and multicast) is often used.
- **SIP Example:** A large company's conference call is in progress. 5 people from different branches are connected via the internet to the central Asterisk/PBX server on Unicast (some are remote, some local). However, the same call's streaming is being broadcast to 200 employees sitting inside the head office via Multicast on their desk phones to save the local LAN's bandwidth.

## 💡 Transport Shortcut

To carry SIP signaling at the transport layer, **UDP** (fast and connectionless, standard port 5060) or **TCP** (reliable and connection-oriented) is used, and for security, **TLS** (port 5061) is run. But whether it's UDP or TCP, the routing method is one of these three (Unicast, Multicast, or Mesh).
