# 1. Client-Server & Request-Response Model

This is the same thing you read in the very first step and also saw in the diagram:

**Client-Server:** In SIP, endpoints (phones) temporarily become either a Client (UAC) or a Server (UAS).

**Request-Response:** To start any task, you must first send a Request (INVITE, BYE, etc.), and in return, a Response (200 OK, 486 Busy, etc.) comes back. Without a Request, no Response can come.

---

# 2. All Messaging is US-ASCII Based (Text-Based Protocol)

This is a huge plus point of SIP. Traditional telecom protocols (like ISDN or H.323) are "Binary-based," meaning humans can't read them directly—only machines understand them.

**The advantage of SIP:** SIP is a Text-Based (US-ASCII) protocol, just like HTTP (the Web Browser protocol). This means when you capture SIP packets on Wireshark or Asterisk CLI, you won't need any software; you can read with your own eyes clearly in plain English that it says `From: Ali` and `To: Bob`. This makes troubleshooting very easy.

---

# 3. Message Structure: Postmortem of All Three Parts

Every SIP message (whether Request or Response) is made up of these three parts:

## 📄 Line 1: Request-line (Or Status-line)

This is the first line of the message that tells what the purpose of the message is.

**Example:** `INVITE sip:1002@192.168.10.55:5060 SIP/2.0`

This clearly states: "Bro, I am an INVITE request, I am going to extension 1002, and my protocol version is SIP 2.0."

## 📋 Part 2: Request-Header

This carries important information (Metadata) about the call. It contains many lines, such as:

- **Via:** (Which route the call came through)
- **From:** (Who is making the call)
- **To:** (Who is receiving the call)
- **Call-ID:** (Unique identity of this entire Dialog)
- **CSeq:** (Transaction sequence number)

## 📦 Part 3: Request-Body (Why Optional?)

You caught a very valid point that "sometimes there is nothing in request body but sometimes it has a lot of things."

The Request body is exactly like a "Parcel or Box" that is attached at the very end of the SIP message (after leaving one blank line after the Header).

### ❌ When is it empty (Nothing)?

When we only need to send a signal and don't need to set up any technical media.

**Example:** BYE Request or CANCEL Request. When you are ending a call, you only need to tell the other person "End the call." There are no audio/video parameters to exchange, which is why the Request-Body inside a BYE message is completely empty. Its job is done just by the headers.

### 📦 When does it have "A lot of things"?

When a call needs to be started or modified!

**Example:** INVITE Request or 200 OK Response. In this case, the complete SDP (Session Description Protocol) data is hidden inside the Request-Body. Inside that SDP it is written: "My IP is this, my RTP ports are these, I support these codecs." These are many technical lines, which is why at this time the body is full.

---

# 4. Rejection, Redirection, & Progress (Optional)

These are the same things we learned in the diagram:

- **Accepted:** 200 OK (Call was answered).
- **Redirected:** 3xx codes (The person forwarded somewhere else).
- **Rejected:** 4xx/5xx/6xx codes (Busy, Not Found, etc.).
- **Progress is optional:** 1xx series (like 100 Trying or 180 Ringing). These are optional because if the server decides immediately (e.g., if the number is blocked, it will directly give 403 Forbidden), then there is no need for ringing to play in between.

---

💡 **Core Takeaway:** A SIP message is like a letter (chitti). The Request-line is the main address on the envelope, the Header is the sender's and receiver's address, and the Request-Body is the actual goods (SDP) placed inside the envelope, which is only sent when needed (like during Call Setup).
