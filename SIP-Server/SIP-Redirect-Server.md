# SIP Redirect Server

## 1. Provides Client with Next Hop(s) Information

When a client (UAC) wants to connect to a target and sends its request to the Redirect Server, the Redirect Server does not forward that request ahead.

- **What does it do?** It simply checks in its Location Database where the target user is at that moment and retrieves the details of the new path (IP Address/URI).
- **Response Code:** It sends a specific response code back to the client—typically `302 Moved Temporarily`. Inside the header of this message (the Contact header), there is the IP address of the next server or device, which we call the **Next Hop**.

## 2. Client Contacts the Next Hop Server or UAS Directly

As soon as the original client (Phone A) receives that `302 Moved Temporarily` message from the Redirect Server, it learns the new address.

- **Next Step:** The client terminates its connection with that Redirect Server right there.
- **Direct Communication:** The client now directly sends a brand new `INVITE` request to that new IP address (Next Hop) itself—whether that's another SIP server or directly the target endpoint (UAS).

## Practical Diagram: Proxy vs Redirect Server

The difference between the two will become crystal clear from this flow:

### Proxy Server Model (What We Studied Earlier)

```
[Phone A] -------- 1. INVITE --------> [Proxy Server] -------- 2. INVITE --------> [Phone B]
[Phone A] <------- 4. 200 OK --------- [Proxy Server] <------- 3. 200 OK --------- [Phone B]
```

(The Proxy stands in the middle and handles all the message delivery itself.)

### Redirect Server Model

```
[Phone A] -------- 1. INVITE --------> [Redirect Server]
[Phone A] <--- 2. 302 Moved (Address) --- [Redirect Server] (Job Done!)

[Phone A] ----------------------- 3. New INVITE ------------------------------> [Phone B]
[Phone A] <---------------------- 4. 200 OK ------------------------------------ [Phone B]
```

## Real-World Use Case (Where Is This Used?)

Imagine a large company with two offices: one in Islamabad and one in Karachi. A person in Islamabad calls a person in Karachi.

The central server (Redirect Server) sees that, "Man, this call should go towards the Karachi office's server." Instead of handling the call itself, it tells the Islamabad phone: "Bro, here's the IP of the Karachi server, contact it directly." This prevents load from falling on the central server.

## 📝 Short Summary

A **Redirect Server** is like an **Information Desk**. You ask it, "Where is such-and-such person?", it hands you their address, and you walk over to that person yourself.
