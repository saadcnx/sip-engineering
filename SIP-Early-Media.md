# Early Media

## Real-World Use Cases

- **Custom Network Announcements:** "Number unavailable" or "Insufficient balance."
- **Custom Ringback Tones (CRBT):** Music/tune before answer.
- **Call Center IVRs / Queue Music:** "Your call is important" or background music.

Callee hasn't answered (no 200 OK), but audio is already playing. This is Early Media.

## SIP Protocol Level

**183 Session Progress** plays the key role in early media.

## Key Technical Requirements

- **SDP Exchange First:** Caller and callee must know IP/ports/codecs beforehand. Early Offer or SDP inside 183 is mandatory.
- **180 Ringing vs 183 Session Progress:**
  - **180 Ringing:** Local ring generation (phone generates ringback).
  - **183 Session Progress:** Stop local ring; play RTP audio from network (announcement/music).
- **PRACK (Optional/Recommended):** Reliable delivery of 183 (RFC 3262) so it isn't dropped.

## One-Line Summary

Early Media = RTP audio/video before 200 OK via 183 Session Progress, so users hear announcements, custom ringback, or IVR prompts.
