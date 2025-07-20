<!-- markdownlint-disable MD033 -->
# Zero-Key Vault
### Privacy-first, client-side relays for EVM & Bitcoin  
> **Send crypto without servers, without custody, without a trace.**  

---

## 📌 TL;DR
Open `zero-key-vault-evm.html` (EVM) or `zero-key-vault-btc.html` (Bitcoin) in any modern browser, connect a wallet, and **atomically relay funds through a one-time address**—breaking on-chain links while.

---

## 🚀 Quick-Start (Non-Technical)
| Step | Action |
|---|---|
| 1 | **Download** the latest release or clone this repo. |
| 2 | **Double-click** `index.html` (EVM) or `btc.html` (Bitcoin). |
| 3 | **Connect Wallet** (MetaMask, Trust, WalletConnect). |
| 4 | Paste **destination address** & **amount**. |
| 5 | **Send Privately** → two signed transactions broadcast automatically. |

---

## 🛡️ Privacy Architecture
| Layer | Mechanism |
|---|---|
| **Client-Side Execution** | All cryptography, ABI calls, and transaction signing happen in the browser; no data leaves the user’s machine except the final signed transactions. |
| **One-Time Relay** | A fresh, ephemeral key-pair is generated per transfer. The on-chain footprint becomes: `User → Temp → Destination (+ Tip)` |
| **No External APIs** | Public RPC endpoints (Infura, Blockstream) are used **read-only**; no server ever holds private keys. |

---

## 📦 Repository Layout
zero-key-vault/
├── index.html        # EVM 10-chain vault
├── btc.html          # Bitcoin vault
├── README.md         # this file

---

## ✅ Supported Networks

| Chain | Chain-ID | RPC Endpoint (read-only) |
|---|---|---|
| Ethereum | `1` | `https://eth.llamarpc.com` |
| BNB Smart Chain | `56` | `https://bsc-dataseed.binance.org` |
| Polygon | `137` | `https://polygon-rpc.com` |
| Avalanche | `43114` | `https://api.avax.network/ext/bc/C/rpc` |
| Fantom | `250` | `https://rpc.ftm.tools` |
| Arbitrum | `42161` | `https://arb1.arbitrum.io/rpc` |
| Optimism | `10` | `https://mainnet.optimism.io` |
| Gnosis | `100` | `https://rpc.gnosischain.com` |
| Cronos | `25` | `https://evm.cronos.org` |
| Aurora | `1313161554` | `https://mainnet.aurora.dev` |
| Bitcoin | — | Blockstream REST API |

---

## 🧠 Technical Deep-Dive

### 1. Transaction Flow (EVM)
```text
┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│   Sender    │──▶│   Temp      │──▶│ Destination │
│  (User)     │   │   Wallet    │   │   Wallet    │
└─────────────┘   └─────────────┘   └─────────────┘


tx1 is signed by the user’s wallet.
tx2 is signed by the ephemeral wallet created in-browser.
Gas & tip are bundled; no additional fees.
2. Bitcoin Flow
Uses bitcoinjs-lib (browser build) + Blockstream REST endpoints.
UTXOs are fetched → transaction built & signed → pushed via /tx.
3. Client-Side Features

Feature	Implementation
Dead-Man Switch	localStorage stores encrypted payload; setInterval tracks last activity.
Geo-Lock	HTML5 Geolocation coarse check (lat/lng ±3°).
AI Gas-Prediction	TensorFlow.js model predicts 30-min gas; fallback to current price.
Rotating Tip	keccak256(salt + UTC-day) produces daily address.
Fiat Off-Ramp	Ramp.Network iframe (no custody).
Steganography	LSB encoding hides seed phrase inside PNG canvas.

Steps to download and use
| **PC / Laptop (Windows / macOS / Linux)**                              | **Mobile (iOS / Android)**                                                                        |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| 1. Click **“Code” → “Download ZIP”** on the repo.                      | 1. Tap **“Code” → “Download ZIP”** on the repo.                                                   |
| 2. **Right-click** the ZIP → **Extract All**.                          | 2. **Open Files app** → **Extract** the ZIP.                                                      |
| 3. **Double-click** `index.html` or \`btc.html\*\*.                    | 3. **Tap** `index.html` or `btc.html`.                                                            |
| 4. Browser opens → click **“Connect Wallet”** (MetaMask, Frame, etc.). | 4. Browser or wallet opens → tap **“Connect Wallet”** (MetaMask Mobile, Trust, WalletConnect QR). |
| 5. Fill address & amount → **Send Privately**.                         | 5. Fill address & amount → **Send Privately**.                                                    |
