# Delayed Offer (DO)

- Caller sends INVITE **without SDP** (empty body).
- Callee responds with **200 OK** containing its SDP (codecs, RTP port).
- Caller selects matching codec and sends its SDP in the **ACK**.

**Key Difference:**  
Early Offer (EO) → SDP in INVITE  
Delayed Offer (DO) → SDP in ACK

## Flow Comparison

| Early Offer (EO) | Delayed Offer (DO) |
|------------------|---------------------|
| INVITE (SDP)     | INVITE (no SDP)     |
| 200 OK (SDP)     | 200 OK (SDP)        |
| ACK              | ACK (SDP)           |

## Why Use Delayed Offer?

- **Avoid codec mismatch:** Get callee capabilities first.
- **3PCC:** For call centers, auto-attendants, recording servers.
- **Inter-trunk compatibility:** Resolve codec mismatch between different networks.

**One-Line Summary:**  
DO sends no SDP in INVITE; callee offers in 200 OK, caller finalizes in ACK.

<img width="760" height="503" alt="image" src="https://github.com/user-attachments/assets/2be6eca5-2655-45c0-b21c-4f8d2f2d795a" />
credit - Technical Venture
