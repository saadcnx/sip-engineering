# SIP Capability: Session Management

This is the final and fifth pillar of our SIP capabilities, and with this, the complete lifecycle of SIP is accomplished.

Let's understand this in absolutely simple terms.

## What Is Session Management?

What's happened so far?

- We located the person (**Location**).
- Checked whether they're free or not (**Availability**).
- Matched the codecs (**Capabilities**).
- Connected the call and started the voice (**Session Setup**).

But think about it—is our job finished once the call starts? Absolutely not! During a call, many things need to be done:

- If the boss calls, putting the first call on **Hold**.
- **Transferring** that call to another colleague.
- **Merging** three or four people to create a Conference.
- And when the conversation is over, **Terminating** (Hanging up) the call.

All these tasks fall under **Session Management**. Controlling the session while the call is in progress is its real purpose.

## How Does It Do This? (Practical Examples)

Session Management focuses on two main things: **Transfer** and **Termination**.

### 1. Call Transfer (Forwarding a Call)

Imagine a customer's call arrived at the receptionist's desk. The customer needs to speak with the technical department. What will the receptionist do? They will transfer the call.

For this, SIP uses specialized methods like the `REFER` method.

- The receptionist's phone sends a `REFER` request and says: "Bro, transfer this customer's call directly to the technical department at this IP address/extension."

### 2. Session Modification / Hold (Putting on Hold)

If you have to open the door while talking to someone and you press the Hold button:

- SIP sends a new `re-INVITE`, in which the audio stream is halted via SDP (a hold tone starts playing or it goes mute). When you come back and press unhold, it sends another `re-INVITE` to resume the media stream.

### 3. Session Termination (Ending the Call)

When the conversation is over and one party hangs up:

- The phone of the person ending the call sends a `BYE` request.
- The phone on the other side responds with a `200 OK`.
- With this, the SIP session ends, and the network ports and bandwidth that were reserved (for RTP streams) are freed back up.

## 📊 Quick Summary: The Complete Cycle of SIP's 5 Pillars

1. **User Location:** Figure out where the person is sitting (`REGISTER`).
2. **User Availability:** Check whether they're free or busy (Presence / Status codes).
3. **User Capabilities:** Check which codecs/features match (SDP).
4. **Session Setup:** Place the call, make it ring, and connect (`INVITE` → `200 OK` → `ACK`).
5. **Session Management:** Control the call during its duration (Hold, Transfer, or Terminate via `BYE`).
