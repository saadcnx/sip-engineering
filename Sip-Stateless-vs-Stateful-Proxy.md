# Stateless Proxy vs Stateful Proxy 

A Proxy Server's job is not just to forward packets. It also decides how long the server keeps a transaction in its RAM/memory.

## Transaction Stateless Proxy

Works like a **"Blind Postman."**

- **How it works:** When a Request (INVITE) or Response (200 OK) arrives, it looks at the message, finds the route, and forwards it immediately without saving anything.
- **No State Maintained:** No record of who sent what earlier. Every packet is treated as brand new.
- **Pros:** Very light and fast. Uses low RAM and CPU, so it can handle millions of requests per second.
- **Cons:** Cannot perform advanced routing, re-transmissions, call-forking (ringing 3 phones at once), or digest authentication.

## Transaction Stateful Proxy

Works like a **"Smart Traffic Controller"** that maintains memory at the transaction level.

- **How it works:** When a request arrives, the proxy holds the state in RAM until the transaction ends.
- **Transaction State Period:** Starts when the request arrives, and stays in memory until a Final Response (2XX, 3XX, 4XX, 5XX, or 6XX) is received.
- **Key Point:** *"Transaction Stateful has no knowledge of a session Update Request (UPDATE), a Transfer Request (REFER) or of a Termination Request (BYE)."*
  - This means it only remembers individual transactions, not the whole Dialog (Call Session).
  - Once the first transaction (INVITE → 200 OK) ends, the proxy removes it from memory.
  - Later UPDATE, REFER, or BYE requests are treated as brand new, separate transactions because the proxy does **not** track Dialog State (it is only Transaction Stateful, not Call/Dialog Stateful).

## Quick Comparison Table

| Feature | Transaction Stateless | Transaction Stateful |
|---|---|---|
| Memory / RAM Usage | Zero memory tracking | Memory maintained until final response |
| Re-transmissions | Cannot handle (just forwards) | Handles internal re-transmissions itself |
| Parallel Forking | Not supported | Supported (ring multiple extensions at once) |
| Mid-call Requests (BYE/REFER) | Forwards normally | Processes as a new transaction |
