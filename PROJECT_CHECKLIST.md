# ACKZERO — Project Checklist (v0.1 → v1.0)

> Goal: build a **simple, independent digital acknowledgment of sending & availability**  
> Scope: Europe + UK  
> Principle: no account required (v0.1), proof-first, minimal UX

---

## 1. Core Concept (MUST)
- [ ] Clear definition: *proof of sending & availability* (not proof of reading)
- [ ] Explicit non-goals documented (not certified email, not legal advice)
- [ ] Separation from TimeProofs (brand, repo, site, API)
- [ ] Terminology fixed and consistent (ACK, Proof, Availability, Receipt)

---

## 2. Legal & Regulatory Sanity (EU/UK)
- [ ] Clarify legal positioning (evidence support, not legal certification)
- [ ] Check compatibility with:
  - [ ] EU civil procedure (free evidence / commencement de preuve)
  - [ ] UK civil evidence principles
- [ ] GDPR compliance:
  - [ ] No content storage (hash-only)
  - [ ] Minimal metadata
  - [ ] Explicit data retention policy
- [ ] Disclaimer section (site + README)

---

## 3. Proof Model (CRITICAL)
- [ ] Define ACKZERO proof format (JSON)
- [ ] Fields locked:
  - [ ] proof_id
  - [ ] created_at (UTC)
  - [ ] sender_fingerprint
  - [ ] recipient_identifier_hash (email / ref)
  - [ ] message_hash
  - [ ] availability_url
  - [ ] proof_hash (self-integrity)
- [ ] Deterministic hashing rules documented
- [ ] Proof verifiable without ACKZERO UI (API + spec)

---

## 4. User Flow (v0.1 – No Account)
- [ ] Step 1: user writes message (or uploads text/PDF)
- [ ] Step 2: ACKZERO generates:
  - [ ] proof_id
  - [ ] verification link
  - [ ] reference code
- [ ] Step 3: user sends message via their own email
- [ ] Step 4: recipient can access availability page (optional)
- [ ] Step 5: third party can verify proof independently

---

## 5. Abuse & Edge Cases
- [ ] Anti-fake claims documented (what ACKZERO proves / does not prove)
- [ ] Handling “recipient claims not received”
- [ ] Handling “recipient never opened”
- [ ] Timestamp authority clarity (UTC + server signed)
- [ ] Rate limiting & basic abuse protection

---

## 6. API (Minimal)
- [ ] POST /create-proof
- [ ] GET /verify/{proof_id}
- [ ] Proof JSON downloadable
- [ ] No auth required (v0.1)
- [ ] OpenAPI spec published

---

## 7. Verification Page
- [ ] Public verification URL
- [ ] Human-readable summary:
  - [ ] What is proven
  - [ ] What is NOT proven
- [ ] Machine-readable proof (JSON)
- [ ] Timestamp + hash clearly visible

---

## 8. Website (Single Page v0.1)
- [ ] Clear problem statement (email ≠ proof)
- [ ] Concrete examples:
  - [ ] Contract termination
  - [ ] HR / disputes
  - [ ] Freelance / invoices
- [ ] 30-second demo
- [ ] “Why not email?” section
- [ ] “Why not registered mail?” section
- [ ] Legal disclaimer
- [ ] Contact email visible

---

## 9. Naming & Branding
- [ ] ACKZERO name locked
- [ ] Domain configured (ackzero.io)
- [ ] Neutral, serious tone (legal-friendly)
- [ ] No crypto / blockchain language

---

## 10. GitHub & Documentation
- [ ] MIT License
- [ ] README.md:
  - [ ] What it is
  - [ ] What it is not
  - [ ] How it works
  - [ ] Legal positioning
- [ ] Proof format spec
- [ ] Changelog v0.1

---

## 11. Monetization (Post v0.1)
- [ ] Free anonymous proofs (limited)
- [ ] Pro usage (bulk / API key)
- [ ] B2B / Enterprise discussion only
- [ ] No pricing page in v0.1

---

## 12. Success Criteria v0.1
- [ ] Proof can be generated in < 60s
- [ ] Proof verifiable by third party
- [ ] No account required
- [ ] No personal data stored
- [ ] Clear legal understanding by users

---

## 13. Explicit Non-Critical (Can Wait)
- [ ] Dashboard
- [ ] User accounts
- [ ] Mobile app
- [ ] Advanced analytics
- [ ] Full legal certification

---

## 14. Final Question Gate (Before Launch)
- [ ] Is the proof understandable by a non-technical person?
- [ ] Can it be explained in one sentence?
- [ ] Would I personally use it for a dispute?

---

**Status:** ☐ Draft ☐ In Progress ☐ v0.1 Ready
