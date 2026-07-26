# SIP Proxy Server

## 1. Receives Requests & Forwards on Client's Behalf

This means that no client on the network (whether it's a Cisco IP Phone or a Softphone on a PC) talks directly to another client for signaling. Everything happens through the Proxy.

- **Real-world Analogy:** Imagine you're sitting in an old-school VIP office where you need an operator to talk to anyone. You pick up the phone and say, "Operator, connect me to the manager." The operator takes your request, finds the manager, and forwards your call ahead.
- **What happens in SIP?** Phone A doesn't send an `INVITE` directly to Phone B. Phone A sends its request to the Proxy. The Proxy looks at that request, applies a little bit of its own intelligence to it, and then, on behalf of Phone A, forwards that request ahead towards Phone B or the SIP Gateway.

## 2. The Big Three: Authentication, Authorization, Routing

A Proxy Server isn't just a "postman" who delivers the letter ahead; it holds huge responsibilities for security and routing:

### 🔒 Authentication (Who Are You?)

Whenever any IP phone comes onto the network or tries to make a call, the Proxy doesn't immediately trust it.

- **Backend Process:** Phone A sent an `INVITE`. Instead of forwarding it ahead, the Proxy sends back a challenge: `401 Unauthorized`. This means: "First, tell me your password (secret key)."
- The phone creates an encrypted hash of its password and sends it again. The Proxy checks it, and only when it's satisfied that this is our own valid employee does it allow the call to proceed.

### 🛡️ Authorization (Do You Have Permission for This?)

Authentication meant that you are a user of the network. Authorization means: are you allowed to do this specific task?

- **Backend Process:** Imagine an agent sitting at a local extension dials an International Number (USA/UK). The Proxy will check in its database what the class-of-service is for this extension. If they don't have permission, the Proxy, instead of forwarding the call ahead, immediately responds with `403 Forbidden`: "Bro, you don't have permission to make this call."

### 🗺️ Routing (Showing the Path)

This is the Proxy's main operational job.

- **Backend Process:** When Phone A dials 1002, the Proxy checks where 1002 is located. It performs a lookup in the Location Database, retrieves its IP address, and routes the call to the correct network segment or subnet.
- If the number isn't local (like a mobile number), the Proxy knows that this call shouldn't be routed towards local extensions but towards the SIP Gateway instead.

## 💡 Short Summary

The **Proxy Server** is both the Security Gate and the GPS of the SIP network. It checks whether the user is genuine (Authentication), whether they have the right to make the call (Authorization), and then delivers their request to the correct target (Routing & Forwarding).
