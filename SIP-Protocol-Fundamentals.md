# SIP: A Protocol for Creating, Modifying, and Terminating Sessions
 
**Definition:** *SIP is a protocol for creating, modifying, and terminating sessions with one or more participants.*
 
This is the most standard and core definition of SIP. RFC 3261 (the official SIP standard document) defines it exactly this way.
 
Let's break this definition down into simple terms and understand it within the VoIP/Telecom context.
 
Think of SIP as working like an **"Event Organizer"** or a **"Matchmaker."** Its job is solely to connect people, manage their call settings, and end the connection when the conversation is over.
 
It performs three basic tasks:
 
## 1. Creating Sessions (Connecting the Call)
 
When you dial someone's number from your phone, SIP's first job begins — **Creating a Session**.
 
- **What does it do?** It establishes a connection between the two endpoints (like Phone A and Phone B).
- **How does it do it?** As we saw earlier, it sends an `INVITE` request. This request doesn't just say "Pick up the call," it also carries **SDP (Session Description Protocol)** data along with it. Inside the SDP, the phone says: "This is my IP address, I can receive audio on this port, and I support these audio formats (codecs like G.711 or G.729)."
- **Result:** Both phones agree with each other, and a session is created.
## 2. Modifying Sessions (Making Changes During a Call)
 
The call is in progress, and both parties are talking. But if something needs to change during the call, that's called **Modifying a Session**.
 
**Practical Examples:**
 
- You put the call on **Hold**.
- Midway, you convert the audio call into a **Video Call**.
- While moving around, you switch from **Wi-Fi to Mobile Data** (your IP address changes).
**SIP's Role:** In such a situation, SIP becomes active again and sends a `re-INVITE` (a new INVITE inside the existing call). It tells the other phone: "Boss, the session settings have changed; now the audio is on hold" or "Here's the new IP address, send media to this one."
 
## 3. Terminating Sessions (Ending the Call)
 
When the conversation is over and one party hangs up, the session is **Terminated**.
 
- **What does it do?** It signals both endpoints to free up their resources (bandwidth, ports) because the call has ended.
- **SIP's Role:** It sends a `BYE` request (or a `CANCEL` if the call was canceled even before being picked up). The other side responds with `200 OK`, and the line is cleared on both ends.
## One or More Participants? (How Many People?)
 
The final part of the definition states: *"with one or more participants."* This means SIP is flexible:
 
- **One-to-One Call:** When you call a single friend (2 participants).
- **Multi-party / Conference Call:** When you make a conference call where 3, 4, or more people are talking together. Through a SIP server (like Asterisk/PBX), the sessions of all participants can be managed and modified simultaneously.
## ⚠️ One Crucial Point (That People Often Misunderstand)
 
SIP itself **does not transfer** the call's audio or video. SIP's job is only to **Create, Modify, and Terminate** the session (i.e., Signaling). Once the call is connected, a separate protocol handles the audio transfer, called **RTP (Real-time Transport Protocol)**.
 
SIP merely builds the road; the traffic runs on RTP.
