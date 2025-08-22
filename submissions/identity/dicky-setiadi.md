# vApp Submission: Access Pass

## Verification
```yaml
github_username: "dicky-setiadi"
discord_id: "462058243057909760"
timestamp: "2025-08-22"
```

## Developer
- **Name**: Dicky Setiadi
- **GitHub**: @dicky-setiadi
- **Discord**: _dckys
- **Experience**: Junior Web Developer with JavaScript/Node.js. Comfortable building small full-stack apps and REST APIs.

## Project

### Name & Category
- **Project**: Access Pass for Communities
- **Category**: identity

### Description
A lightweight gate for communities (Discord/Telegram/private pages).
Users connect a wallet and present a Soundness Layer proof/attestation (e.g., human_verified, dev_contributor).
If valid, the server issues a short-lived token and reveals an invite/secret.
Goal: reduce spam/Sybil without collecting PII.

### SL Integration  
- The server verifies the user’s proof/attestation with Soundness (testnet).
- If valid, it issues a short-lived JWT to open the gated endpoint (e.g., invite/secret).
- Policy is simple and configurable (e.g., require `human_verified`).
- No on-chain writes required for the PoC.

## Technical

### Architecture
**Frontend**: React. Pages: /verify (connect wallet, submit proof), /success (secret/invite), /help.
**Backend**: Node.js (Express). Endpoints:
- GET /api/nonce – one-time nonce (5m expiry).
- POST /api/verify – verify signature + call Soundness; returns { token } if eligible.
- GET /api/secret – gated resource; requires Authorization: Bearer <token>.
**Security**: one-time nonce, short JWT TTL, strict CORS, basic rate limit, input validation.
**Observability**: request logs + verification audit log.

### Stack
- **Frontend**: React
- **Backend**: Node.js
- **Blockchain**: Soundness Layer
- **Storage**: Database (PostgreSQL)

### Features
1. Wallet connect + nonce/signature flow.
2. Eligibility check via Soundness proof/attestation.
3. Gated endpoint that returns invite/secret.
4. Configurable policy (ENV/JSON).

## Timeline

### PoC (2-4 weeks)
- [ ] Basic functionality: connect wallet → nonce/sign → verify → token → access secret
- [ ] SL integration: server verifies proof/attestation against policy
- [ ] Simple UI: minimal /verify & /success + README + curl examples
- [ ] Deploy PoC (web + API) on free tiers.

### MVP (4-8 weeks)  
- [ ] Policy config UI / multi-community presets.
- [ ] Redis rate limit (optional), monitoring/logging, CI/CD, deploy hardening.
- [ ] Better error states & small UX polish.

## Innovation
Config-only gate powered by zk-verified attestations—privacy-preserving, minimal UX friction, and deployable on free tiers for small communities.

## Contact
- Discord: _dckys
- GitHub: dicky-setiadi
- Email: dickysetiadi50@gmail.com

**Checklist before submitting:**
- [x] All fields completed
- [x] GitHub username matches PR author  
- [x] SL integration explained
- [x] Timeline is realistic
