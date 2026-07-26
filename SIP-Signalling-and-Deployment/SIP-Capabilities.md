# SIP Feature Blueprint: A Deeper Dive into the 5 Pillars

## 1. Location (Address Resolution, Name Mapping, Call Redirection)

We previously learned that the server knows where a person is located. But on the backend, it's actually performing these three tasks:

- **Address Resolution:** Just as DNS resolves a domain name (`google.com`) into an IP address, the SIP server similarly resolves a user's extension or URI (e.g., `sip:1001@company.com`) into their actual IP and port (`192.168.10.55:5060`).
- **Name Mapping:** This maps an extension to a person's real name, so that when a call arrives, the screen doesn't just show a number but also displays a Caller ID (e.g., "Ali DevOps").
- **Call Redirection:** If a user isn't at their seat and has set up Call Forwarding, the SIP server redirects (reroutes) the call to another extension or mobile number.

## 2. Media Capabilities via SDP (Audio/Video, RTP Ports, Codecs)

This is a very crucial technical part. SIP itself only handles signaling (messages), but through **SDP (Session Description Protocol)**, it determines these three things:

- **Audio/Video Calls:** First, it's decided whether only voice will go or if video will be on as well.
- **RTP Ports:** This is extremely important. For audio/video to flow, both devices agree between themselves: "Bro, I will receive audio packets on port number 12004, you send them here." These ports are called **RTP (Real-time Transport Protocol)** ports.
- **Codec Capabilities:** Both devices exchange lists of their preferred codecs (like G.711, Opus, or H.264 for video) and select the one that is common between them.

## 3. Availability (Specific Messages for Unavailability)

We discussed that if the user is not free, response codes are returned. In SIP, there is a specific message/code for everything so the caller knows what the issue is:

- If the person is on another call → sends `486 Busy Here` (You hear a busy tone).
- If the person has switched off their phone or has no network → `480 Temporarily Unavailable` comes back.
- If you've dialed a wrong number that doesn't exist at all → a `404 Not Found` message is sent.

## 4. Session Management (Mid-call Changes, Transfer & Hold)

The changes that occur after the call is connected are called **Mid-call Changes**. For this, SIP sends new messages (like `re-INVITE` or `UPDATE`):

- **Changing Codecs:** Imagine a call is in progress and suddenly your internet slows down; SIP can send a mid-call message to switch to a new codec (with lower bandwidth) so the call doesn't drop.
- **Adding Endpoints:** Adding a third person into the call during the conversation (creating a Conference).
- **Transfer & Hold:** Transferring a call forward to someone via a `REFER` message, or pausing the media and putting it on hold.

## 5. Other (SIP Gateways & Conferencing)

- **SIP Gateways (Call Control):** If you want to call a normal mobile number (Zong, Jazz, PTCL) from an IP phone, the internet traffic must be converted to the normal telephone network (PSTN). This job is done by a **SIP Gateway**. It converts traditional call signaling into SIP, and SIP into traditional, and handles the entire call control.
- **Supports Conferencing:** SIP has a built-in capability to handle multi-party sessions, whether through a central server (PBX) or via mesh networking.

## 💡 Summary

This note is essentially SIP's complete **Feature Blueprint**. SIP finds the path (Location), agrees on the language for conversation (SDP), communicates the status (Availability), changes settings during the call (Session Management), and connects to the outside world (Gateways).
