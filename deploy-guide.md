# Deployment Guide — Sovereign Credential Issuer

Issue verifiable, soulbound credentials on OPN Chain (Chain ID: 984). This guide walks through contract deployment and dApp setup.

---

## Prerequisites

- **Node.js** v16+
- **MetaMask** (or any EVM wallet)
- **OPN Testnet OPN tokens** (get from [faucet.iopn.tech](https://faucet.iopn.tech))
- **Git**

---

## 1. Clone & Install

```bash
git clone https://github.com/GodwynnMets/Sovereign-Credential-Issuer
cd Sovereign-Credential-Issuer
npm install
```

---

## 2. Configure Environment

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit `.env` with your details:

```env
# Deployer wallet private key (without 0x prefix)
DEPLOYER_PRIVATE_KEY=your_private_key_here

# OPN Chain RPC endpoints
OPN_RPC=https://testnet-rpc.iopn.tech
OPN_RPC_BACKUP=https://testnet-rpc2.iopn.tech

# Contract details
CONTRACT_NAME=SovereignCredentialIssuer
NETWORK=OPN_Chain_Testnet
CHAIN_ID=984
```

⚠️ **NEVER commit `.env`** to version control. Use environment variables in CI/CD.

---

## 3. Fund Your Wallet

1. Copy your deployer wallet address
2. Visit [faucet.iopn.tech](https://faucet.iopn.tech)
3. Paste address and request testnet OPN tokens
4. Wait ~10 seconds for confirmation

Check balance:
```bash
node scripts/check-balance.js
```

---

## 4. Compile Contract

```bash
# Compile Solidity to bytecode (no network needed)
node compile.js

# Expected output:
# ✓ SovereignCredentialIssuer.sol compiled
# ✓ ABI generated → abi.json
# ✓ Bytecode ready for deployment
```

---

## 5. Deploy to OPN Testnet

```bash
# Deploy and verify
npm run deploy:testnet

# Expected output:
# ✓ Deploying to OPN Chain Testnet (984)...
# ✓ Contract deployed: 0x7F3a2E9d1C84bB6e0D5F8A3c2B9e1D7F4A6C8E2d
# ✓ Deployment tx: 0x...
# ✓ Gas used: XXX
```

The contract address will be saved to `deployment.json`.

---

## 6. Add OPN Chain to MetaMask

**Manual Setup:**
- Network Name: `OPN Chain Testnet`
- RPC URL: `https://testnet-rpc.iopn.tech`
- Chain ID: `984`
- Currency: `OPN`
- Explorer: `https://testnet.iopn.tech`

**Or use the dApp button:** Click "Add OPN Chain to MetaMask" in the Contract tab.

---

## 7. Interact with Contract

```bash
# Open interactive CLI
npm run interact

# Commands:
# issue <wallet> <name> <type> <org> <description>
# verify <tokenId>
# getREP <wallet>
# getNeoPoints <wallet>
# revoke <tokenId> <reason>
```

**Example:**
```bash
issue 0x317074C86d87c378df1E4264FD855c13AA6192a0 "Chukwuemeka Adeyemi" "Employee Certificate" "Elizade Nigeria" "Completed onboarding — May 2026"
```

---

## 8. Deploy Frontend (GitHub Pages)

The `index.html` is auto-deployed to GitHub Pages.

**Settings → Pages:**
- Source: `Deploy from a branch`
- Branch: `main` / `root`

Live at: `https://godwynnmets.github.io/Sovereign-Credential-Issuer/`

To update:
```bash
git add index.html
git commit -m "v1.X — description"
git push origin main
```

Refresh in ~30 seconds. GitHub Pages will auto-deploy.

---

## Contract Architecture

### Key Functions

#### Issue Credential
```solidity
function issueCredential(
  address to,
  string credentialType,
  string organization,
  string description,
  string neoIdHash,
  uint256 validUntil,
  string tokenURI
) → uint256 tokenId
```

**Rewards:**
- Base holder: +25 REP
- Genesis badge holder: +50 REP (2x multiplier)
- All holders: +10 NeoPoints

**Soulbound:** Non-transferable after minting.

---

#### Verify Credential
```solidity
function verifyCredential(uint256 tokenId)
  → (bool isValid, string credentialType, string organization, address holder)
```

Returns full credential metadata. Used by dApp for verification.

---

#### REP & NeoPoints
```solidity
function getREPBalance(address holder) → uint256
function getNeoPoints(address holder) → uint256
function isGenesisHolder(address wallet) → bool
```

**Tier progression:**
- Common: 0+ REP
- Rare: 1,000 REP
- Epic: 5,000 REP
- Legendary: 10,000 REP
- Mythic: Select (admin)

---

#### Admin Functions
```solidity
function registerIssuer(address issuerAddr, string issuerName, string orgType)
function registerGenesisHolder(address addr)
function revokeCredential(uint256 tokenId, string reason)
```

Only callable by contract admin (deployer).

---

## Token Standard

**ERC-721 (Soulbound)**
- One credential per holder per type
- Non-transferable (reverts on transfer)
- Metadata stored on-chain (tokenURI)
- Compatible with block explorers

---

## Events

```solidity
event CredentialIssued(
  uint256 indexed tokenId,
  address indexed to,
  address indexed issuer,
  string credentialType,
  string organization
);

event CredentialRevoked(
  uint256 indexed tokenId,
  string reason
);
```

Subscribe to events via ethers.js:
```javascript
contract.on('CredentialIssued', (tokenId, to, issuer, type, org) => {
  console.log(`Credential #${tokenId} issued to ${to}`);
});
```

---

## Network Details

| Property | Value |
|----------|-------|
| **Chain Name** | OPN Chain Testnet |
| **Chain ID** | 984 (0x3D8) |
| **RPC 1** | https://testnet-rpc.iopn.tech |
| **RPC 2** | https://testnet-rpc2.iopn.tech |
| **Explorer** | https://testnet.iopn.tech |
| **Faucet** | https://faucet.iopn.tech |
| **Symbol** | OPN |
| **Block Time** | ~2 seconds |

---

## Troubleshooting

### "Insufficient balance"
```bash
# Check balance
node scripts/check-balance.js

# Request more from faucet
# https://faucet.iopn.tech
```

### "Contract already deployed"
```bash
# View existing deployment
cat deployment.json
```

### "MetaMask wrong network"
1. Open MetaMask
2. Switch to "OPN Chain Testnet"
3. Or click "Add OPN Chain" button in dApp

### "Verification failed"
- Token must exist
- Holder must be connected to same chain (OPN)
- Check block explorer: https://testnet.iopn.tech

---

## Environment Mainnet (Future)

When IOPn launches mainnet:

1. Update `deploy.js` network config
2. Redeploy to mainnet (real OPN tokens required)
3. Update dApp `index.html` contract address
4. Migrate genesis holders to mainnet

---

## Testing

```bash
# Local hardhat node (optional)
npm run hardhat:node

# Deploy to localhost
npm run deploy:localhost

# Run tests
npm test
```

---

## Security Audit

⚠️ **Not audited.** Use at your own risk in production.

For mainnet deployment, consider:
- Professional security audit
- Multi-sig admin wallet
- Time-lock governance
- Rate-limiting on issuance

---

## Support

- **Documentation:** https://iopn.gitbook.io/iopn
- **Discord:** https://discord.gg/iopn
- **GitHub Issues:** https://github.com/GodwynnMets/Sovereign-Credential-Issuer/issues

---

## License

MIT License — See LICENSE file

**Built on OPN Chain · Powered by IOPn**