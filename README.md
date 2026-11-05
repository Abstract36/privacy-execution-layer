# Privacy Execution Layer v3.0

<p align="center">
  <strong>🔐 ZK-SNARK Privacy Protocol on Solana</strong>
  <br><br>
  <a href="#quick-start">Quick Start</a> •
  <a href="docs/">Documentation</a> •
  <a href="SECURITY.md">Security</a> •
  <a href="CONTRIBUTING.md">Contributing</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Archived-lightgrey" alt="Archived">
  <img src="https://img.shields.io/badge/Build-does%20not%20compile-red" alt="Does not compile">
  <img src="https://img.shields.io/badge/License-MIT-blue" alt="MIT License">
</p>

---

> ## ⚠️ Archived on 2026-11-05 — the code does not compile
>
> Read the rest of this document as a design sketch, not as a description of
> working software. Measured before archiving:
>
> - **The program does not build.** `declare_id!` is called with
>   `privPoo1AAAA…`, a placeholder that is not a valid Solana public key — it
>   decodes to 33 bytes instead of 32. That failure cascades: `ID` is never
>   defined, so the `#[program]` macro fails in both crates. Separately,
>   `#[derive(Default)]` is applied to a struct holding `[u8; 8192]`, which Rust
>   does not implement `Default` for.
> - **CI never passed.** Nineteen runs, zero successes, across the repository's
>   whole history.
> - **There are no tests.** `anchor test` runs `ts-mocha` over `tests/**/*.ts`,
>   and no `tests/` directory exists.
> - **The toolchain requirements contradict each other.** `anchor-cli 0.29.0`
>   pinned by `--locked` needs Rust older than 1.80; the committed `Cargo.lock`
>   needs Rust 1.85 or newer.
>
> The feature table below marks items complete. Those marks describe what was
> designed, not what runs. Nothing here has ever executed on a Solana cluster.
>
> **Not audited. Never use with real funds.**

## Overview

Non-custodial privacy protocol enabling **unlinkable transactions** through zero-knowledge proofs.

### Core Invariants *(Cannot be changed)*

1. **Absolute Unlinkability** — Cannot link deposits to withdrawals
2. **Single-Spend Guarantee** — Each nullifier used only once
3. **Zero Trusted Parties** — No admin keys, no custody
4. **Protocol > Implementation** — Works without team/UI

## Quick Start

```bash
# Clone
git clone https://github.com/privacy-execution-layer/protocol
cd protocol

# Install
npm install

# Build
anchor build

# Test
./scripts/test_all.sh

# Deploy to devnet
./scripts/deploy_devnet.sh
```

## Features

| Feature | Phase | Status |
|---------|-------|--------|
| Deposit/Withdraw | 1 | ✅ |
| ZK Proof Verification | 1 | ✅ |
| Developer Fee (0.3%) | 1 | ✅ |
| Encrypted Payloads | 2 | ✅ |
| Time Windows (24h) | 2 | ✅ |
| Cross-Pool Nullifiers | 2 | ✅ |
| Relayer Network | 3 | 🔜 |
| Dashboard | 4 | 🔜 |

## Project Structure

```
├── programs/private-pool/   # Solana program (Rust)
├── circuits/                # ZK circuits (Circom)
├── scripts/                 # Automation (14 scripts)
├── docs/                    # Documentation
├── .github/                 # Workflows & templates
└── announcements/           # Generated posts
```

## Fee Structure

| Withdrawal | Fee (0.3%) |
|------------|------------|
| 0.1 SOL | 0.0003 SOL |
| 1 SOL | 0.003 SOL |
| 10 SOL | 0.03 SOL |
| 100 SOL | 0.3 SOL |

## Documentation

- [Protocol Doctrine](docs/PROTOCOL_DOCTRINE.md)
- [Threat Model](docs/THREAT_MODEL_v0.md)
- [Core Invariants](docs/CORE_INVARIANTS.md)
- [Technical Memo](docs/TECHNICAL_MEMO.md)

## How to Participate

| Action | How |
|--------|-----|
| Ask a question | [Open Discussion Issue](.github/ISSUE_TEMPLATE/discussion.yml) |
| Report a bug | [Open Bug Report](.github/ISSUE_TEMPLATE/bug_report.yml) |
| Suggest feature | [Open Feature Request](.github/ISSUE_TEMPLATE/feature_request.yml) |
| Contribute code | See [CONTRIBUTING.md](CONTRIBUTING.md) |
| Report vulnerability | See [SECURITY.md](SECURITY.md) |

## Security

| Severity | Bounty |
|----------|--------|
| Critical | Up to $1,000,000 |
| High | Up to $250,000 |
| Medium | Up to $50,000 |
| Low | Up to $10,000 |

⚠️ **DO NOT** create public issues for vulnerabilities.  
Use [GitHub Security Advisories](../../security/advisories).

## Governance

All decisions via [GitHub Issues](../../issues):
- 👍 Vote for
- 👎 Vote against
- Discussion → Proposal → Implementation

See [GOVERNANCE.md](GOVERNANCE.md).

## Publication Commands

```bash
# Deploy to IPFS + create GitHub release
./scripts/technical_announcement.sh

# Generate announcement posts
./scripts/generate_announcements.sh
```

---

<p align="center">
  <strong>This project exists only as code.</strong><br>
  No Discord. No Telegram. No Twitter.<br>
  All discussions via GitHub Issues.
</p>

---

## License

[MIT](LICENSE)
