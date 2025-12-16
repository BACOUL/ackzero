# ACKZERO

ACKZERO is a simple, independent **proof of message availability** service.

It provides **cryptographic evidence that a specific message was made available to a recipient at a precise time**, without requiring the recipient to sign up or interact.

**Target**: Europe + United Kingdom  
**Use cases**: cancellations, disputes, HR notices, freelancers, B2C/B2B communications  
**Contact**: contact@ackzero.io

---

## What ACKZERO does

ACKZERO proves that:

- A **specific message existed**
- It was **made available** at a **trusted UTC timestamp**
- It was intended for a **specific recipient** (hashed identifier)
- The message **has not been modified**
- Anyone can **verify this independently** later

This proof is **publicly verifiable** and **tamper-evident**.

---

## What ACKZERO does NOT prove

ACKZERO does **not** prove that:

- The recipient read or accepted the message
- The recipient replied
- The recipient’s legal identity beyond the provided identifier
- Legal equivalence to regulated registered-delivery services

ACKZERO proves **availability and integrity**, not guaranteed receipt.

---

## Why ACKZERO exists

Emails, screenshots, and local timestamps are:

- Easy to dispute
- Dependent on providers and interfaces
- Hard to verify independently

ACKZERO provides:

- A **neutral third-party proof**
- A **cryptographic fingerprint** of message + recipient reference
- A **public verification endpoint**
- A **portable JSON receipt**

No message content is ever stored.

---

## How it works (v0.1)

1. You write a message and choose a recipient identifier (e.g. email).
2. You generate hashes (message, subject, recipient).
3. ACKZERO creates a proof and returns:
   - a **claim link**
   - a **public receipt**
4. You send your message normally and include the claim link.

The recipient never needs an account.

---

## Proof model

ACKZERO is **hash-only** and **privacy-first**.

Only cryptographic hashes are stored:

- **recipient hash** (e.g. lower-cased email)
- **subject hash** (optional)
- **message hash**
- **metadata hash** (optional)

Canonicalization (recommended):
- UTF-8
- Line endings normalized to `\n`
- Trim trailing spaces

---

## Public verification

Each proof exposes:

- A **public claim page** (`/p/:token`)  
  → logs that the message was made available

- A **signed JSON receipt** (`/v/:id`)  
  → includes timestamps, hashes, status, and HMAC signature

Verification answers only factual questions:
- Does this proof exist?
- When was it created?
- Was it made available?
- Has anything changed?

No private data is revealed.

---

## Typical use cases

- Contract or subscription cancellation
- Formal notice or dispute escalation
- Freelance scope, delivery, or payment notices
- HR procedural communications
- Commercial B2B notifications

---

## Legal positioning

ACKZERO is **not a regulated delivery service**.

It provides **independent cryptographic proof of message availability**.

In disputes, it strengthens evidence by providing:
- objective timestamps
- integrity guarantees
- neutral verification

Legal effect depends on jurisdiction and context.

---

## Scope (v0.1)

- No user accounts
- No message storage
- Hash-only architecture
- Public verification
- Signed receipts (HMAC-SHA256)
- Optional open tracking (claim / pixel)

Future versions may extend capabilities without breaking existing proofs.
