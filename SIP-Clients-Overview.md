# SIP Clients

## 1. IP Phones (Hardware Desk Phones)

These are physical phones that look just like normal office telephones, but on their backend, instead of a telephone line (RJ-11), they use an Ethernet cable (RJ-45) or Wi-Fi.

**What happens on the backend?** Inside them, they have their own small computing hardware and an OS with a built-in SIP stack running. As soon as you connect them to the network, they grab an IP from the local DHCP and `REGISTER` with the Asterisk/PBX server. (Examples: Yealink, Grandstream, Polycom).

## 2. Softphones (Software-based Phones)

As the name implies—Software + Phone. If you don't have a physical phone, you simply install software on your PC, Laptop, or Mobile that turns your device into a SIP client.

**What happens on the backend?** It uses your PC's sound card (microphone and speaker). When you run the software on your PC, it uses the PC's network card to send SIP messages. (Examples: Zoiper, Linphone, MicroSIP, or X-Lite).

## 3. Cisco SIP IP Phones (The Request/Response Capability)

Cisco gets a special mention because Cisco is the industry standard in enterprise networking. Regarding Cisco phones, it's important to understand this line: *"can initiate SIP request and respond to requests."*

**What does this mean?** This is the exact same concept we learned at the very beginning—**UAC and UAS**. A Cisco phone is such a smart endpoint that when you make a call, it can initiate a new `INVITE` request (acting as UAC), and when a call comes in from the other side, it can accept it and respond with `200 OK` (acting as UAS). It doesn't depend on any central server to generate or respond to requests; this capability resides within the phone's own firmware.

## 4. SIP Conferencing Stations

In corporate meeting rooms or boardrooms, you've probably seen a triangle-shaped speaker-phone sitting in the middle of the table, commonly called a **"Conference Pod"** or **"Spider Phone."**

**What happens on the backend?** It's just like a normal IP phone, but its hardware is very high-end (360-degree microphones and powerful speakers). In the context of SIP, it's designed to handle multiple multimedia audio streams and set up a dynamic audio mixing session so that the entire room's voice goes through without any noise.

## 💡 Core Connect

Whether it's a handheld IP Phone, a Softphone running on a computer, or a boardroom Conferencing Station—in the eyes of the SIP server (Proxy/Registrar), all of them are simply **Endpoints (User Agents)**. Their job is all the same: tell the server their address, send requests, and receive responses.
