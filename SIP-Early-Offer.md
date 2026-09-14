# Early Offer (EO) – How It Works

Early Offer means sending SDP in the initial INVITE to negotiate media early.

## Steps

1. **Caller → Server/Callee:** Phone A sends INVITE with SDP.
   - Example: "I want to call; my codecs are G.711, Opus; my RTP port is 10004."

2. **Callee → Caller:** Phone B answers with 200 OK containing SDP.
   - Example: "G.711 selected; my RTP port is 20008."

3. **ACK:** Phone A sends ACK without SDP, because media is already finalized.

**RTP Flow:** Audio starts immediately after the call connects.

## Why Use Early Offer?

- **Early Media / Pre-Connect Audio:** Needed for custom ringtones, announcements, or queue music (e.g., 183 Session Progress) because the audio channel is already negotiated.
- **Cisco (CUCM) & Enterprise Gateways:** Preferred by PSTN/GSM gateways and Cisco Unified Communications Manager so the gateway knows which codec and bandwidth to reserve.
- **SIP Trunking:** SIP trunk providers often insist on Early Offer to avoid transcoding issues.

## One-Line Summary

Early Offer means sending your SDP (codecs/ports) in the initial INVITE, making call setup fast and ensuring early media/ringback tones work correctly.

## Early Offer Example
<img width="787" height="515" alt="image" src="https://github.com/user-attachments/assets/6897e849-45a2-4d55-b9f4-671e9ba796b8" />
credit - Technical Venture
