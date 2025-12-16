# ACKZERO

ACKZERO is a simple, independent **digital acknowledgement** service.  
It creates a **verifiable proof that a specific message was issued** and made available at a precise time, **without requiring the recipient to sign up**.

Target market: **Europe + United Kingdom**  
Primary use cases: cancellations, disputes, HR notices, freelancers, B2C/B2B communications  
Contact: **jeason.bacoul@gmail.com**

---

## What ACKZERO is

ACKZERO produces a neutral, tamper-evident proof showing:

- **When** a message was issued (trusted timestamp)
- **Which exact message** was issued (cryptographic hash)
- **Which recipient** it was intended for (hashed identifier)
- **How to verify it independently** (public verification link or code)

It is designed to be **simpler than registered electronic delivery** and **stronger than “I sent an email”**.

---

## What ACKZERO is NOT

ACKZERO does **not** prove:

- That the recipient read the message
- That the recipient accepted or replied
- The recipient’s legal identity beyond the identifier provided
- Legal equivalence to regulated registered-delivery services (varies by country)

ACKZERO proves **issuance and availability of proof**, not guaranteed receipt.

---

## Why ACKZERO exists

Email headers, screenshots, and local timestamps are:

- Easy to dispute
- Difficult to verify independently
- Dependent on providers and user interfaces

ACKZERO provides:

- An **independent public verification endpoint**
- A **portable proof object** (JSON)
- A **cryptographic fingerprint** of message + recipient reference
- A **timestamped record** that can be checked later by anyone

---

## Typical use cases

- Contract or subscription cancellation
- Formal notice or dispute escalation
- Freelance scope, delivery, or payment notices
- HR procedural communications
- B2B commercial notifications

---

## How ACKZERO works (v0.1)

1. You write a message and specify a recipient identifier (email, reference, etc.).
2. ACKZERO generates a cryptographic proof and verification link.
3. You send your message normally and include the verification link or code.
4. Anyone can later verify that the message existed at that time and has not changed.

The recipient never needs an account.

---

## Proof model

ACKZERO is **hash-first** and **content-minimal**.

Recommended canonicalization:
- UTF-8 encoding
- Line endings normalized to `\n`
- Trim trailing spaces

Minimal proof structure (v0.1):

```json
{
  "spec": "ackzero.v0.1",
  "proof_id": "ACK-7F3A9",
  "created_at": "2025-12-16T14:22:00Z",
  "recipient_hint": "sha256:…",
  "subject_hash": "sha256:…",
  "message_hash": "sha256:…",
  "issuer": "ackzero",
  "verify": "https://ackzero.io/verify?proof=ACK-7F3A9",
  "integrity": {
    "proof_hash": "sha256:…"
  }
## Hashed elements

ACKZERO relies exclusively on cryptographic hashes to guarantee integrity while minimizing exposure of personal or sensitive data.

The following elements are hashed using **SHA-256** after canonicalization (UTF-8, normalized line breaks, trimmed whitespace):

- **message_hash**  
  Hash of the full message body exactly as written by the issuer.  
  This guarantees that the message content cannot be altered after proof creation.

- **subject_hash** (optional)  
  Hash of the message subject or title, if provided.  
  Useful for legal or contractual notices where the subject carries meaning.

- **recipient_hint**  
  Hash of a canonical recipient identifier (typically a lower-cased email address or reference ID).  
  This proves *who the message was intended for* without exposing the recipient publicly.

These hashes are committed into a single proof object.

---

## Proof object (v0.1)

```json
{
  "spec": "ackzero.v0.1",
  "proof_id": "ACK-7F3A9",
  "created_at": "2025-12-16T14:22:00Z",
  "recipient_hint": "sha256:…",
  "subject_hash": "sha256:…",
  "message_hash": "sha256:…",
  "issuer": "ackzero",
  "verify": "https://ackzero.io/verify?proof=ACK-7F3A9",
  "integrity": {
    "proof_hash": "sha256:…"
  }
- **proof_id**  
  Short, human-readable identifier generated at proof creation time.  
  Used as the primary reference for verification, sharing, and inclusion inside messages or documents.  
  Example format: `ACK-7F3A9`.

- **created_at**  
  Trusted UTC timestamp indicating when the proof was generated.  
  This timestamp anchors the existence of the message at a precise moment in time.

- **recipient_hint**  
  SHA-256 hash of a canonical recipient identifier (for example: lower-cased email address).  
  Allows later confirmation that the proof was intended for a specific recipient without revealing their identity publicly.

- **subject_hash**  
  SHA-256 hash of the subject or title associated with the message.  
  Optional, but recommended for legal or contractual communications.

- **message_hash**  
  SHA-256 hash of the full message body, exactly as issued.  
  Any modification of the message content will result in a different hash and invalidate equivalence.

- **issuer**  
  Identifier of the issuing service.  
  For v0.1, this value is always `ackzero`.

- **verify**  
  Public verification URL allowing anyone to check the existence and integrity of the proof without authentication.

- **integrity.proof_hash**  
  SHA-256 hash of the full proof object.  
  Ensures the proof itself has not been altered since creation.

---

## What this proof guarantees

The proof guarantees that:

- A specific message **existed**
- At a **precise timestamp**
- Intended for a **specific (hashed) recipient**
- With **unchanged content**

The proof does **not** guarantee that the message was received, opened, or read.

---

## Public verification

Verification answers only factual questions:

- Does this proof exist?
- When was it created?
- Are the hashes intact?
- Has the proof been modified?

No private data is ever revealed during verification.

---

## How it is used in practice

1. A user writes a message (email, letter, notice).
2. ACKZERO generates a proof and returns a `proof_id`.
3. The user includes the verification link or proof ID in the message.
4. At any later time, either party can verify the proof publicly.

This creates a neutral, independent anchor of issuance.

---

## Legal positioning

ACKZERO provides **technical proof of issuance**, not legal delivery certification.

It is designed to:
- Strengthen disputes
- Support good-faith communication
- Provide objective timestamps and integrity guarantees

Legal effect depends on jurisdiction and context.

---

## Scope (v0.1)

- No user accounts required
- No message storage
- Hash-only architecture
- Stateless verification
- Designed for individuals, freelancers, and small organizations

Future versions may extend capabilities without breaking existing proofs.
