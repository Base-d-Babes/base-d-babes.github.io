# Based_d Babes — The Archetypes

**Status:** ADR-0004 Compliant  
**Network:** Base (Chain ID: 8453)  
**Contract:** `0x5dCFeD9D2897d9EA587a30EcDA5a069461Ca46Dd`

---

## 🎯 Quick Start

### Local Development

**The mint interface MUST be served via HTTP, not opened directly as a file.**

MetaMask and other Web3 wallets only inject `window.ethereum` on `http://` or `https://` URLs, not `file://` URLs.

#### Option 1: Using the Helper Script (Windows)

```bash
# Double-click or run:
start-server.bat
```

Then visit: **http://localhost:9999/mint.html**

#### Option 2: Manual Python Server

```bash
cd F:\Base_d\Base.d-Claude
python -m http.server 9999
```

Then visit: **http://localhost:9999/mint.html**

#### Option 3: Node.js (if Python unavailable)

```bash
npx http-server -p 9999
```

---

## 📱 Mobile Wallet Testing

To test with mobile wallets (MetaMask Mobile, Rainbow, Coinbase Wallet):

1. Start local server (see above)
2. Ensure your phone is on the same Wi-Fi network
3. Visit: **http://192.168.40.79:9999/mint.html**
4. Use WalletConnect or in-app browser

---

## 🏗️ Architecture

```
index.html          → Static canon surface (no wallet logic)
mint.html           → Zora-aligned mint execution surface
start-server.bat    → Local development server launcher
```

### Governance Documents

- **RFC-0001** — Minting & Canon Governance
- **SPEC-0001** — Archetype Metadata Schema
- **ADR-0002** — Canonical Static Site Boundary
- **ADR-0003** — Canonical Minting Interface (superseded by ADR-0004)
- **ADR-0004** — Zora-Aligned Mint Execution Surface

---

## 🔐 Minting Architecture (ADR-0004)

### Zora Protocol Integration

**Minter Contract:** `0x04E2516A2c207E84a1839755675dfd8eF6302F0a`  
**Function:** `mint(address to, uint256 quantity, address collection, uint256 tokenId, address mintReferral)`

**Key Points:**
- ✅ Uses Zora sale strategy (not raw ERC-1155)
- ✅ No SDK dependencies
- ✅ Pure vanilla JavaScript + Web3 provider
- ✅ Free-tier compatible
- ✅ Full calldata transparency

### Mint Parameters

| Parameter | Value |
|-----------|-------|
| Price | 0.003 ETH per token |
| Max Supply | 50 tokens |
| Per-Wallet Limit | 5 tokens |
| Token ID | 1 (The Steward) |

---

## 🚀 Deployment

### GitHub Pages (Production)

```bash
git add index.html mint.html start-server.bat README.md
git commit -m "ADR-0004: Production deployment"
git push origin main
```

Live site: **https://base-d-babes.github.io/**

### Pre-Deployment Checklist

- [ ] Test locally with `start-server.bat`
- [ ] Connect MetaMask to Base network
- [ ] Verify wallet connection works
- [ ] Test mint flow with small amount
- [ ] Confirm supply tracking updates
- [ ] Check transaction on BaseScan

---

## 🧪 Testing

### Verification Steps

1. **Start Server:** Run `start-server.bat`
2. **Open Browser:** Navigate to `http://localhost:9999/mint.html`
3. **Connect Wallet:** Click "CONNECT WALLET"
4. **Verify:**
   - MetaMask popup appears
   - Base network selected/switched automatically
   - Wallet address displays in status bar
   - Quantity controls become active
   - Supply shows "X / 50"

### Common Issues

**Issue:** "No wallet detected"  
**Solution:** Ensure you're accessing via `http://localhost:9999`, NOT `file://`

**Issue:** "Wrong network"  
**Solution:** Interface auto-switches to Base (8453). Confirm in MetaMask.

**Issue:** Port 9999 in use  
**Solution:** Edit `start-server.bat` and change port number

---

## 📋 File Structure

```
F:\Base_d\Base.d-Claude\
├── index.html              # Static canon surface (ADR-0002)
├── mint.html               # Zora-aligned execution surface (ADR-0004)
├── start-server.bat        # Local development server
├── README.md               # This file
├── 1.json                  # Token metadata
├── contract.json           # Collection metadata
├── mint-base.js            # Deployment script reference
└── [governance docs]/      # RFCs, SPECs, ADRs
```

---

## 🔗 Links

- **Collection:** [OpenSea](https://opensea.io/assets/base/0x5dcfed9d2897d9ea587a30ecda5a069461ca46dd/1)
- **Contract:** [BaseScan](https://basescan.org/address/0x5dcfed9d2897d9ea587a30ecda5a069461ca46dd)
- **Token #1:** [BaseScan](https://basescan.org/token/0x5dcfed9d2897d9ea587a30ecda5a069461ca46dd?a=1)

---

## 📖 Canonical Language

> "Minting is conducted exclusively via the Zora Protocol sale strategy on Base. Primary minting occurs at: https://base-d-babes.github.io/mint.html"

---

## 🛡️ Security Notes

- No private keys in code
- No hardcoded secrets
- No localStorage/sessionStorage
- All transactions require wallet confirmation
- On-chain enforcement of all limits
- Client-side checks are advisory only

---

## 📚 For Developers

### Modifying Mint Logic

**ALL changes to mint execution MUST:**
1. Comply with ADR-0004
2. Use Zora sale strategy contract
3. Maintain calldata transparency
4. Avoid SDK dependencies
5. Receive Steward approval (RFC-0001)

**PROHIBITED:**
- Direct ERC-1155 `mint()` calls
- Bypassing Zora protocol layer
- Introducing paid dependencies
- Modifying canon surface (`index.html`)

---

**Last Updated:** 2026-01-05  
**Governance Status:** ✅ Fully Compliant (ADR-0004)
