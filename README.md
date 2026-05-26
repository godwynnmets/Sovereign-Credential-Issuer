# Sovereign Credential Issuer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Deployed-brightgreen)](https://godwynnmets.github.io/Sovereign-Credential-Issuer/)
[![OPN Chain](https://img.shields.io/badge/OPN%20Chain-Testnet%20984-blue)](https://testnet.iopn.tech)

**Issue verifiable, soulbound credentials on OPN Chain.** Built on IOPn's sovereign, immutable, human-centric blockchain. Powered by NeoID · REP · NeoPoints · Genesis Badge.

---

## 🎯 Features

✅ **Issue Soulbound Credentials** — Non-transferable ERC-721 tokens on OPN Chain  
✅ **Reputation System** — Earn REP points and unlock tier badges (Common → Rare → Epic → Legendary → Mythic)  
✅ **NeoID Integration** — Self-sovereign identity verification via IOPn ecosystem  
✅ **Mobile-Optimized** — Responsive dApp with session persistence  
✅ **Web3 Ready** — MetaMask/injected provider support  
✅ **Open Source** — MIT License, fork and deploy freely  

---

## 🚀 Quick Start

### 1. **Access the dApp**
Visit: **[godwynnmets.github.io/Sovereign-Credential-Issuer](https://godwynnmets.github.io/Sovereign-Credential-Issuer/)**

### 2. **Connect Wallet**
- Click "Connect Wallet"
- MetaMask will open
- Approve network switch to OPN Chain Testnet (Chain ID: 984)
- Click "Add OPN Chain to MetaMask" if needed

### 3. **Issue a Credential**
- Fill in recipient wallet, name, type, organization, description
- Click "Issue Credential on OPN Chain"
- Confirm in MetaMask (testnet, so no real gas)
- Credential issued as soulbound NFT

### 4. **Verify**
- Go to "Verify" tab
- Enter Token ID or wallet address
- View credential metadata on-chain

### 5. **Track REP**
- Visit "⋂exus" tab to see reputation points
- Earn 25 REP per credential (50 if Genesis badge holder)
- Progress through tiers: Common → Rare → Epic → Legendary → Mythic

---

## 📋 Core Contract

**SovereignCredentialIssuer (ERC-721 Soulbound)**

| Function | Purpose |
|----------|----------|
| `issueCredential()` | Mint credential to wallet + award REP |
| `verifyCredential()` | Check credential validity & metadata |
| `getREPBalance()` | Query holder's reputation points |
| `getNeoPoints()` | Query holder's NeoPoints balance |
| `revokeCredential()` | Admin revocation (with reason) |
| `registerIssuer()` | Whitelist credential issuer |
| `registerGenesisHolder()` | Register badge holder (2x REP) |

**Contract Address (Testnet):** `0x7F3a2E9d1C84bB6e0D5F8A3c2B9e1D7F4A6C8E2d`  
**Network:** OPN Chain Testnet (Chain ID: 984)  
**Explorer:** [testnet.iopn.tech](https://testnet.iopn.tech)  
**ABI:** [abi.json](./abi.json)

---

## 📁 Project Files

```
sovereign-credential-issuer/
├── index.html          ← Interactive dApp (HTML/CSS/JS + ethers.js)
├── abi.json           ← Contract ABI (function signatures & events)
├── README.md          ← This file
├── deploy-guide.md    ← Step-by-step deployment instructions
├── LICENSE            ← MIT License
└── .github/
    └── workflows/     ← GitHub Actions (auto-deploy Pages)
```

---

## 🎮 dApp Tabs

### **Issue**
- Form to issue new credentials
- Recipient wallet, name, type, organization, description
- Optional NeoID hash and expiry date
- Recent transactions feed
- Badge strip showing features (Soulbound · ERC-721)

### **Registry**
- View all issued credentials
- Filter by holder/type
- Revoke credentials (admin only)
- Count of issued records

### **Verify**
- Query by token ID or wallet address
- Real-time on-chain verification
- NeoID integration status
- Credential validity indicator

### **⋂exus** (Reputation)
- REP points dashboard
- Tier progression tracker (Common → Rare → Epic → Legendary → Mythic)
- Contributor profile (badges, transactions, gas contributed)
- $OPN tokenomics summary

### **Contract**
- RPC configuration for OPN Chain
- Solidity source code excerpt
- Add OPN to MetaMask
- Copy contract ABI

### **Docs**
- Deployment instructions
- Key functions reference
- IOPn ecosystem links

---

## 🔧 Credential Types

Pre-configured in the dApp:
- Employee Certificate
- Customer Verification
- Service Completion
- Training Certificate
- Loyalty Badge
- NeoID Verified
- Vehicle Service Record
- Parts Warranty Certificate
- Fleet Management Credential

**Custom types** — edit the `<select>` in `index.html` to add more.

---

## 🌐 Network Configuration

| Property | Value |
|----------|-------|
| **Chain Name** | OPN Chain Testnet |
| **Chain ID** | 984 (0x3D8 hex) |
| **RPC 1** | https://testnet-rpc.iopn.tech |
| **RPC 2** | https://testnet-rpc2.iopn.tech |
| **Explorer** | https://testnet.iopn.tech |
| **Faucet** | https://faucet.iopn.tech |
| **Token** | OPN |
| **Block Time** | ~2 seconds |

---

## 💡 How It Works

1. **Connect** your MetaMask wallet to OPN Chain Testnet
2. **Issue** a credential by submitting the form → mints soulbound ERC-721 NFT
3. **Earn** REP points: 25 per credential (50 if Genesis badge holder)
4. **Verify** credentials by token ID or holder address
5. **Progress** through reputation tiers to unlock badges

**Soulbound:** Credentials cannot be transferred, only burned/revoked by issuer.

---

## 🚀 Deployment

### **Frontend (GitHub Pages)**
Auto-deployed on every push to `main`:
```bash
git add index.html
git commit -m "Update dApp"
git push origin main
```
Live in ~30 seconds at: https://godwynnmets.github.io/Sovereign-Credential-Issuer/

### **Smart Contract (Backend)**
See [**deploy-guide.md**](./deploy-guide.md) for:
- Environment setup
- Wallet funding
- Contract compilation
- Deployment to OPN testnet
- Issuer registration
- Testing & verification

---

## 🔐 Security

- **Soulbound:** Non-transferable after minting
- **Access Control:** Only registered issuers can mint
- **Session Storage:** Wallet persists via browser sessionStorage
- **No Private Keys:** Never stored or transmitted
- **Audit Status:** ⚠️ Not audited — use with caution in production

---

## 🎨 Tech Stack

- **Frontend:** HTML5 + CSS3 + Vanilla JavaScript
- **Web3:** ethers.js v6
- **Blockchain:** Solidity ^0.8.20
- **Standard:** ERC-721 (NFT) + Access Control
- **Hosting:** GitHub Pages
- **Network:** OPN Chain Testnet (Chain ID: 984)

---

## 📚 Key Resources

- **IOPn Documentation:** https://iopn.gitbook.io/iopn
- **OPN Hub:** https://hub.iopn.tech
- **Testnet Faucet:** https://faucet.iopn.tech
- **Block Explorer:** https://testnet.iopn.tech
- **Discord Community:** https://discord.gg/iopn
- **Deployment Guide:** [deploy-guide.md](./deploy-guide.md)

---

## 🤝 Contributing

1. **Fork** the repo
2. **Create a branch:** `git checkout -b feature/your-feature`
3. **Make changes** to `index.html` or documentation
4. **Test locally** in your browser
5. **Commit:** `git commit -m "Add feature"`
6. **Push:** `git push origin feature/your-feature`
7. **Open Pull Request** with description

---

## 📄 License

MIT License © 2026 Godwin Metsagharun

See [LICENSE](./LICENSE) file for details.

---

## 👤 Author

**Godwin Metsagharun**  
Organization: Elizade Nigeria Limited  
GitHub: [@godwynnmets](https://github.com/godwynnmets)

---

## 🙏 Credits

- **Blockchain:** IOPn (NeoID · REP · NeoPoints · Genesis Badge)
- **Network:** OPN Chain Testnet (Chain ID: 984)
- **Standard:** ERC-721 Soulbound + OpenZeppelin
- **Hosting:** GitHub Pages

---

## 🐛 Issues & Support

- **Report Issues:** https://github.com/GodwynnMets/Sovereign-Credential-Issuer/issues
- **Discussions:** https://github.com/GodwynnMets/Sovereign-Credential-Issuer/discussions
- **Discord:** https://discord.gg/iopn

---

**Built on OPN Chain · Chain ID: 984**  
_Sovereign · Immutable · Human-Centric_