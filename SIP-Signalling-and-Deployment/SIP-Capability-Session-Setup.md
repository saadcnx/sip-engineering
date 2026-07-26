# SIP Capability: Session Setup

Now we've arrived at the climax of this entire process: **Session Setup**.

## What Happened in the First Three Steps?

- **User Location:** We found out where the person is sitting (IP Address).
- **User Availability:** We found out whether the person is free or busy (Status).
- **User Capabilities:** We found out which codecs and media types are common between both parties (Compatibility).

When these three things give the "Green Signal," that's when **Session Setup** begins!

## What Is Session Setup?

The simple meaning of Session Setup is **"Making the phone ring, and once the other party picks up, solidifying the media path between the two."**

So far, the only talk was about "where to call and what the format will be." In this step, the actual call gets placed.

## How Does This Work in the Practical Flow? (The Handshake)

When you dial someone and they pick up the call, a proper Handshake takes place within SIP. We observe this in three stages:

### Stage 1: Ringing (The Bell Rings)

- **INVITE:** The caller's phone sends an `INVITE` to the target phone via the SIP server.
- **`180 Ringing`:** When the target phone learns a call is incoming and it is available, it sends back a response: "Bro, the bell is ringing on my end, tell the caller to wait." (The caller's phone starts playing the ring-back tone "Toot-toot").

### Stage 2: Acceptance (Picking up the Call)

- **`200 OK`:** When the person on the other side picks up the phone, their phone sends a success message with the code `200 OK`. This is the most beautiful message in SIP because it means: "Deal confirmed! The person has picked up the phone."

### Stage 3: Acknowledgment (Solidifying the Path)

- **ACK:** When the caller's phone receives the `200 OK`, it sends back one final confirmation called an `ACK` (Acknowledgment).
- **Session Created!** As soon as the `ACK` reaches the server and the other phone, SIP's session setup is complete. Now SIP's job is finished, and for the actual voice (Audio) to flow, **RTP (Real-time Transport Protocol)** becomes active.

## Simple Word Summary

**Session Setup** is the final bridge that connects two separate phones together. When Location, Availability, and Capabilities all match, the process of `INVITE` → `Ringing` → `200 OK` → `ACK` runs and makes the call go live.
