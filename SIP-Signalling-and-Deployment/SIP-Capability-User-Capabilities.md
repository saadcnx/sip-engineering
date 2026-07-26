# SIP Capability: User Capabilities

## What Are User Capabilities?

In the world of Telecom and VoIP, every endpoint (IP Phone, Laptop Softphone, Mobile App) has its own limitations and specifications. Some phones only support simple audio calls, some can do HD video calls, and some even support screen sharing.

Similarly, within audio, there are different **Codecs** (formats for compressing audio), such as:

- **G.711 (PCMA/PCMU):** Standard quality audio (low CPU usage, high bandwidth).
- **G.722:** HD Quality audio.
- **Opus:** Super flexible audio (automatically adjusts quality if the internet is slow).

The job of the **User Capabilities** feature is to check which features and codecs are common between both endpoints, so the call can run on those. If the two devices don't match, the call simply won't connect (which we call a **Codec Mismatch** in telecom).

## How Does This Work on the Backend? (The SDP Negotiation)

For this task, SIP takes help from a very important partner protocol called **SDP (Session Description Protocol)**. SDP information is always hidden inside SIP's `INVITE` and `200 OK` messages.

Let's understand this with a short dialogue:

- **Phone A (sends INVITE):** "Bro, I want to connect a call to Phone B. My capabilities are that I can do both Audio and Video. And for audio, I have the G.722 (HD) and G.711 codecs."
- **SIP Server / Phone B (checks):** Phone B checks what it has. Assume Phone B is an old desk phone that doesn't support video and only has the G.711 codec.
- **Phone B (sends 200 OK Response):** "Bro, I can't do video, I'll only do Audio. And for audio, G.711 is common between us both, so let's start talking on that."

## Simple Word Summary

**User Capabilities** means **"Compatibility Check."** Before the call connects, it facilitates a compromise (negotiation) between the hardware and software features (Audio, Video, Codecs) of both sides so that both devices can communicate without any errors.
