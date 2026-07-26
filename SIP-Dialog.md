# SIP Dialog

## 🎭 The Simple Concept of a Dialog (The Umbrella)

In SIP, a **Dialog** is a temporary relationship or umbrella that forms between two endpoints (peers). This relationship remains alive as long as your call is in progress.

As long as this Dialog is active, both devices know which specific call they're talking about, because on the backend, this Dialog has a unique identity called the **Dialog ID** (which is formed by combining the `Call-ID`, `From tag`, and `To tag`).

## 🔄 Lifecycle: Different Transactions Inside a Single Dialog

To solidify this concept, look at the sequence below. This entire scenario is **One Single Dialog**, but inside it, **Three Separate Transactions** will run:

```
======================= SIP DIALOG (THE ENTIRE CALL) =======================
|                                                                          |
|  [ Phone A ]                      [ Proxy/Server ]      [ Phone B ]     |
|       |                                  |                   |          |
|       |============ TRANSACTION 1: Call Setup =============|           |
|       |--- 1. INVITE ------------------->|                   |          |
|       |<-- 2. 180 Ringing ---------------|                   |          |
|       |<-- 3. 200 OK (Call picked up) ---|                   |          |
|       |--- 4. ACK ---------------------->|                   |          |
|       |====================================================|           |
|       |                                                                |
|       |             [ ... RTP Media: Conversation is happening ... ]   |
|       |                                                                |
|       |============ TRANSACTION 2: Mid-Call (Hold) ==========|           |
|       |--- 5. re-INVITE (Put on Hold) -->|                   |          |
|       |<-- 6. 200 OK (Done, call on hold)|                   |          |
|       |--- 7. ACK ---------------------->|                   |          |
|       |====================================================|           |
|       |                                                                |
|       |============ TRANSACTION 3: Termination ==============|           |
|       |--- 8. BYE (Drop the call) ------->|                   |          |
|       |<-- 9. 200 OK (Done, call ended) --|                   |          |
|       |====================================================|           |
|                                                                          |
===========================================================================
```

## 🧠 Break Down

- **When did the Dialog start?** When the first `INVITE` request went out and the other side accepted it (`200 OK`), a Dialog (relationship) was created between the two phones.
- **Transaction 1 (Setup):** Ran from `INVITE` up to `200 OK` and ended. (The Dialog is still running).
- **Transaction 2 (Modification):** While talking, the user pressed Hold. A new `re-INVITE` and its `200 OK` arrived. This was a new transaction that ran and ended. (The same Dialog is still ongoing).
- **Transaction 3 (Termination):** The conversation finished, a `BYE` went out, and `200 OK` came back. This was the third transaction. As soon as this transaction ended, the Dialog also officially died.

## 📊 Cement the Difference (Quick Table)

| Feature | Transaction | Dialog |
|---|---|---|
| Scope | Small (Short-lived) | Large (Long-lived) |
| What does it do? | Handles a single Request and its Response. | Remembers the entire call's state between two peers. |
| Example | `BYE` → `200 OK` | An entire 15-minute call (From Setup to Hangup). |

## 💡 Takeaway

A **Dialog** is essentially an entire train, and the various carriages running inside that train (stopping at stations, changing speed, applying brakes) are its separate **Transactions**.
