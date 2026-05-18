# Attesta — Frontend
**Verifiable Credential Interface & Proof Dashboard**

This repository contains the Next.js frontend for **Attesta**, a privacy-first on-chain verifiable credential registry built on Stellar. The interface allows institutions to issue credentials, users to manage and share cryptographic proofs of their credentials, and third parties to verify credential status — all without exposing any sensitive underlying data.

> **Monorepo siblings:**
> - Smart Contracts → [`attesta-contracts`](https://github.com/your-org/attesta-contracts)
> - Backend API → [`attesta-api`](https://github.com/your-org/attesta-api)

---

## 🚀 Features

- Institution dashboard for issuing and revoking verifiable credentials
- User credential wallet — view, manage, and share issued credentials
- Proof generator — creates cryptographic proofs for sharing with third parties
- Third-party verifier interface — verify credential proofs against on-chain commitments
- Access-controlled views based on wallet role (institution, user, verifier)
- Credential status feed — revocation and expiry alerts
- Freighter wallet integration for testnet interaction

---

## 🛠 Prerequisites

- **Node.js** v18 or higher — [Download](https://nodejs.org/)
- **pnpm** — Install via `npm install -g pnpm`
- **Freighter Wallet** browser extension — [Install](https://freighter.app/)
- A deployed instance of `attesta-contracts` (registry + issuer contract IDs required)
- A running instance of `attesta-api` (for off-chain indexing and proof aggregation)

---

## 📦 Installation

```bash
git clone https://github.com/your-org/attesta-web.git
cd attesta-web
pnpm install
```

---

## ⚙️ Environment Setup

Create `.env.local` in the project root:

```env
NEXT_PUBLIC_BASE_URL=https://attesta.app
NEXT_PUBLIC_STELLAR_NETWORK=testnet
NEXT_PUBLIC_HORIZON_PUBLIC_URL=https://horizon.stellar.org
NEXT_PUBLIC_HORIZON_TESTNET_URL=https://horizon-testnet.stellar.org

# Contract IDs (from attesta-contracts deployment)
NEXT_PUBLIC_REGISTRY_CONTRACT_ID=YOUR_DEPLOYED_REGISTRY_CONTRACT_ID
NEXT_PUBLIC_ISSUER_CONTRACT_ID=YOUR_DEPLOYED_ISSUER_CONTRACT_ID

# Backend API
NEXT_PUBLIC_API_URL=http://localhost:3001

# Community
NEXT_PUBLIC_DISCORD_URL=https://discord.gg/attesta
NEXT_PUBLIC_GITHUB_URL=https://github.com/your-org/attesta
```

---

## 🚀 Running the App

### Development

```bash
pnpm dev
```

App will be running at `http://localhost:3000`

### Production Build

```bash
pnpm build
pnpm start
```

---

## 👥 User Roles

The frontend adapts its interface based on the connected wallet's registered role in the contract:

| Role | Capabilities |
|---|---|
| **Institution** | Issue credentials, revoke credentials, manage signing keys |
| **User** | View issued credentials, generate proofs, share proof links |
| **Verifier** | Submit proofs for verification, view verification history |
| **Admin** | Register institutions, manage access control matrix |

On first connect, wallets without a registered role are prompted through an onboarding flow.

---

## 🧪 Testing

### Unit & Component Tests

```bash
pnpm test
```

### End-to-End Tests

Requires a running backend (`attesta-api`) and deployed contracts on testnet:

```bash
pnpm test:e2e
```

---

## 📁 Project Structure

```text
/
├── app/
│   ├── dashboard/        # Role-aware landing dashboard
│   ├── issue/            # Institution credential issuance flow
│   ├── wallet/           # User credential wallet
│   ├── verify/           # Third-party proof verification interface
│   └── onboarding/       # Wallet role registration flow
├── components/           # Reusable UI components
├── hooks/                # Custom React hooks (contract reads, wallet, proofs)
├── lib/                  # Stellar SDK helpers, contract clients, crypto utils
├── public/               # Static assets
└── .env.local            # Environment variables (not committed)
```

---

## 🔐 Privacy Notes

The frontend **never transmits raw credential data** to any server. All cryptographic proof generation happens client-side in the browser using the user's local credential data. Only commitment hashes and public keys are read from or written to the chain.

---

## 🐛 Troubleshooting

**`Failed to connect wallet`**
1. Confirm Freighter is installed and unlocked
2. Switch Freighter network to Testnet
3. Verify `NEXT_PUBLIC_STELLAR_NETWORK=testnet` in `.env.local`

**`Role not recognized` on connect**
1. Confirm the connected wallet address is registered in the registry contract
2. If a new institution, request registration from the contract admin
3. Check `NEXT_PUBLIC_REGISTRY_CONTRACT_ID` matches the deployed contract

**`Proof verification failed`**
1. Confirm the credential has not been revoked by the issuing institution
2. Verify the proof was generated against the correct credential commitment hash
3. Check that `attesta-api` is running and reachable at `NEXT_PUBLIC_API_URL`

**`Cannot fetch credential data`**
1. Confirm `attesta-api` is running: `curl http://localhost:3001/health`
2. Check that the contract IDs in `.env.local` match the deployed contracts

---

## 📚 Resources

- [Stellar Documentation](https://developers.stellar.org/docs/build/smart-contracts)
- [Soroban Docs](https://soroban.stellar.org/docs)
- [Attesta Contracts Repo](https://github.com/your-org/attesta-contracts)
- [Attesta API Repo](https://github.com/your-org/attesta-api)

---

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for coding standards, Git workflow, and the PR process.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

**Built with ❤️ on Stellar**
