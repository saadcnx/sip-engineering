# SIP Transactions

## 🧩 What Is a Transaction? (The Definition)

In SIP, a single transaction is formed when a request begins and the entire loop of messages is completed up to its final destiny.

Three things are involved in this:

- **The Request:** Which starts the transaction (e.g., `INVITE`, `BYE`, `CANCEL`).
- **Provisional Responses (1xx):** The temporary progress messages in between (e.g., `100 Trying`, `180 Ringing`). These are optional.
- **A Final Response (2xx to 6xx):** Which officially ends/closes the transaction.

> ⚠️ **Rule:** Once a final response (`200 OK`, `404`, `486`, etc.) arrives, that specific transaction dies (gets closed). After that, whatever new message comes will form a separate transaction.

## ⚡ Real-World Examples

Let's look at three examples diagrammatically so the concept becomes absolutely clear.

### Example 1: INVITE to 200 OK (The Invite Transaction)

```
[ Client (UAC) ]                  [ Server (UAS) ]
        |                                |
        |------- 1. INVITE ------------->|   <-- Transaction START!
        |<------ 2. 180 Ringing ---------|   (Provisional - Optional)
        |<------ 3. 200 OK --------------|   <-- Transaction CLOSED (End)!
        |
```

**Analysis:** The `INVITE` request started the transaction, `180 Ringing` came in between, and `200 OK` (Final Response) completed and closed this transaction.

### Example 2: ACK Itself Is Also a Transaction

Here's a very fine and professional network engineering point that people often get wrong.

According to the SIP standard (RFC 3261), when the INVITE is successful and a `200 OK` arrives, the previous transaction has already been closed. Now, the acknowledgment that the caller sends back:

```
[ Client (UAC) ]                  [ Server (UAS) ]
        |                                |
        |------- 1. ACK ---------------->|   <-- Separate Transaction!
        |
```

**Analysis:** Because `ACK` is a standalone request (and no response code comes back for it when it's in the standard flow), at the protocol level, it's considered a separate transaction—referred to as a branch of the Non-INVITE Transaction (or it handles the behavior directly in a transaction-less manner).

### Example 3: BYE and 200 OK (The Bye Transaction)

When the call ends, a new request-response loop runs:

```
[ Client (UAC) ]                  [ Server (UAS) ]
        |                                |
        |------- 1. BYE ---------------->|   <-- New Transaction START!
        |<------ 2. 200 OK --------------|   <-- Transaction CLOSED!
        |
```

**Analysis:** `BYE` made the request to drop the call, and the server said `200 OK` (Final Response), closing this transaction as well.



<img width="762" height="429" alt="image" src="https://github.com/user-attachments/assets/153c599d-5c84-43ec-91d1-2ffa249d118c" />

## From (Invite to 200 OK) this is 1 transaction
## ACK is another transaction
## BYE to 200 OK this is 3rd transaction

credit Technical Venture
