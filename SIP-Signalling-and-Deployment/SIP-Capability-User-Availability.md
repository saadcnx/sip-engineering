# SIP Capability: User Availability

## What Is User Availability?

Imagine you dialed someone. The SIP server has already figured out where that person is sitting—at `192.168.10.55` (**User Location**). But is it guaranteed that they'll actually pick up the call?

- Maybe they're already busy on another call (DND / Busy).
- Maybe they've enabled "Do Not Disturb" on their phone.
- Maybe their system is offline or they're in a meeting.

SIP's **User Availability** capability ensures that before forwarding the call, it checks whether the target endpoint is actually capable of receiving a call at that moment.

## How Does This Work on the Backend?

The biggest example of this is the SIP `OPTIONS` request or the status codes received during call setup. It's observed in two ways:

### 1. Before the Call (Pre-call Checking / Presence)

You've probably noticed on office phones or softphones (like Teams or Zoiper) that small icons appear next to names:

- 🟢 Green (Available)
- 🔴 Red (Busy / On a Call)
- 🟡 Yellow (Away / Idle)
- ⚫ Grey (Offline)

All of this happens through SIP's **Availability / Presence** features. Devices continuously share status with each other or through the server to show who is currently available.

### 2. During the Call Setup (Real-time Response Codes)

When you make a call (send an `INVITE`), if the other party isn't available, the SIP server or target endpoint sends back some standard Response Codes that indicate availability:

- `486 Busy Here` → Means the user is currently busy on another call (Not Available).
- `600 Busy Everywhere` → The user is busy on all of their devices.
- `480 Temporarily Unavailable` → The user is currently unreachable (perhaps disconnected from the network).

## Simple Word Summary

**User Location** told us where the person is sitting (IP Address), and **User Availability** checks whether that person is even in the mood or condition to talk at this moment (Busy/Free).
