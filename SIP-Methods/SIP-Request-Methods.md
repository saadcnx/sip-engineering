# SIP Methods 

## 1. INVITE
- Initiates or modifies a session.
- Sends SDP (codecs, RTP ports).
- Re-INVITE used for hold or media change.

## 2. ACK
- Confirms receipt of final response (200 OK) to INVITE.
- Only used with INVITE.

## 3. BYE
- Terminates an active call (established dialog).
- Sent by either party on hangup.

## 4. CANCEL
- Cancels a pending call (ringing, not yet answered).
- Triggers 487 Request Terminated.

## 5. OPTIONS
- Queries capabilities/health.
- Response: 200 OK with SDP.
- Used for keep-alive (e.g., Asterisk qualify).

## 6. REGISTER
- Updates user location (IP, port, URI) with Registrar.
- Sent on boot or re-registration.

## Quick Summary

| Method   | Purpose                     | When Used                     |
|----------|-----------------------------|-------------------------------|
| INVITE   | Initiate/modify call        | Dialing or hold               |
| ACK      | Confirm call setup          | After 200 OK to INVITE        |
| BYE      | Terminate active call       | Hangup during call            |
| CANCEL   | Terminate pending call      | Hangup while ringing          |
| OPTIONS  | Check health/capabilities   | Background pinging/keep-alive |
| REGISTER | Update location database    | Phone boot or re-register     |
