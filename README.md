# StoreScope AI — Retail Intelligence Platform

> AI-powered shelf analytics for FMCG retail teams.  
> Built on **ARC Network** (Circle L1) — payments in USDC, proofs on-chain.

**Live demo:** https://storescope-ai.vercel.app  
**ARC Testnet:** Chain ID `5042002` · Explorer: https://testnet.arcscan.app

---

## What is StoreScope AI?

StoreScope AI turns shelf photos into structured business intelligence:

- **Upload** a retail shelf image
- **AI analyzes** brands, SKUs, facings, prices via OCR + Roboflow
- **Pay per task** in USDC on ARC Testnet ($0.025 total for 10 micro-tasks)
- **Get report** with shelf share, competitor visibility, stock risk, recommendations
- **Proof on-chain** — final report hash recorded on ARC

---

## ARC Network Integration

All payments flow through **ARC Testnet** (Circle-backed L1, USDC-native gas):

| Feature | ARC Usage |
|---|---|
| AI Analysis (10 tasks) | 10 micro-USDC transactions, $0.025 total |
| Layout Mint | Pay $2.10 USDC to mint store layout as on-chain asset |
| Forum Marketplace | Buy/sell store layouts in USDC |
| Wallet verification | Sign-In-With-Ethereum (SIWE) on every session |

**Network config:**
```
Network:  ARC Testnet
Chain ID: 5042002
RPC:      https://rpc.testnet.arc.network
USDC:     0x3600000000000000000000000000000000000000
Explorer: https://testnet.arcscan.app
Faucet:   https://faucet.circle.com
```

---

## Quick Start

### Prerequisites

- Node.js 18+
- MetaMask browser extension
- ARC Testnet USDC (from https://faucet.circle.com)

### 1. Clone & Install

```bash
git clone https://github.com/levanhung789/storescope-ai.git
cd storescope-ai
npm install
```

### 2. Environment Variables

Create `.env.local`:

```env
# Roboflow (AI image detection)
ROBOFLOW_API_KEY=QH9U94r31RusAz0TaO3O
RF_WORKSPACE=levanhungs-workspace
RF_PROJECT=fmcg-project
# RF_VERSION=1   ← fill after model is trained
```

### 3. Run Dev Server

```bash
npm run dev
```

Open **http://localhost:3000**

---

## Add ARC Testnet to MetaMask

1. Open MetaMask → Networks → Add Network
2. Fill in:

| Field | Value |
|---|---|
| Network Name | ARC Testnet |
| RPC URL | https://rpc.testnet.arc.network |
| Chain ID | 5042002 |
| Currency Symbol | USDC |
| Block Explorer | https://testnet.arcscan.app |

3. Get free testnet USDC: https://faucet.circle.com

---

## Key Features to Test

### 1. Connect Wallet + SIWE Verification
- Click **"Connect Wallet"** in the navbar
- Every session requires signing a message to prove wallet ownership
- Nonce is randomized per session (replay-attack safe)

### 2. Anonymous Access (No wallet needed)
- Go to `/login`
- Click **"Access Anonymously"**
- System generates a random identity (e.g., `SwiftAnalyst#7F2A`)
- Full access — same as regular account

### 3. AI Image Analysis with USDC Payment
- Go to `/dashboard/analysis`
- Upload a retail shelf photo (JPEG/PNG)
- Approve **$0.025 USDC** on ARC Testnet
- Watch 10 micro-tasks execute (each = 1 USDC tx)
- Get full report: brands detected, prices, shelf share, recommendations
- Final proof hash recorded on ArcScan

### 4. Store Layout Editor
- Go to `/layout-editor`
- Add fixtures (coolers, shelves, checkout, etc.) — drag to position
- Scroll over fixture = rotate 15°/step
- Click **"Mint & Sell"** → pay $2.10 USDC → list on Forum

### 5. Forum / Marketplace
- Go to `/forum`
- Browse store layouts listed for sale
- Buy layouts with USDC on ARC Testnet

### 6. My Reports
- Go to `/dashboard/reports`
- View saved analysis reports per wallet address
- Export as CSV, JSON, or print as PDF

---

## Project Structure

```
app/
├── page.tsx                    # Landing page
├── login/page.tsx              # Login + Anonymous access
├── dashboard/
│   ├── page.tsx                # Product catalog
│   ├── analysis/page.tsx       # AI shelf analysis + USDC payment
│   ├── product/page.tsx        # Product detail (prices, competitors)
│   └── reports/page.tsx        # My Reports per wallet
├── forum/                      # Layout marketplace
├── layout-editor/              # 3D store layout editor
├── _lib/
│   ├── arc.ts                  # ARC chain config, USDC, pricing
│   └── anonymousAuth.ts        # Anonymous identity
├── _components/
│   ├── WalletButton.tsx        # Connect + SIWE verification
│   ├── AnonBadge.tsx           # Anonymous identity display
│   ├── AnalysisReport.tsx      # Report + export
│   └── LayoutEditor/           # 3D editor (React Three Fiber)
└── api/
    ├── analyze/route.ts        # Roboflow + OCR inference
    └── companies/route.ts      # Product catalog from filesystem
```

---

## Analysis Pipeline

```
User uploads shelf image
        ↓
[Task 1] Upload/Register       $0.001 USDC  → image hash on-chain
[Task 2] Quality check         $0.001 USDC  → blur/lighting check
[Task 3] Shelf detection       $0.003 USDC  → detect shelf rows (Roboflow)
[Task 4] SKU detection         $0.004 USDC  → identify brands via OCR + AI
[Task 5] Competitor analysis   $0.003 USDC  → shelf share calculation
[Task 6] Stock risk            $0.002 USDC  → out-of-stock detection
[Task 7] Layout simulation     $0.004 USDC  → update store model
[Task 8] Recommendations       $0.003 USDC  → AI suggestions
[Task 9] Human review          $0.002 USDC  → flag uncertain detections
[Task 10] Final report         $0.002 USDC  → proof hash on ArcScan
        ↓
Total: $0.025 USDC · Report saved to wallet account
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router), TypeScript |
| Styling | Tailwind CSS v4 |
| 3D Editor | React Three Fiber + Three.js (toon shading) |
| Blockchain | wagmi v3, viem — ARC Testnet |
| AI/OCR | Roboflow (object detection) + Tesseract.js (OCR) |
| Auth | Sign-In-With-Ethereum (SIWE) |
| Storage | localStorage per wallet address |

---

## Screens

| URL | Description |
|---|---|
| `/` | Landing page |
| `/login` | Sign in or anonymous access |
| `/dashboard` | Product catalog (50+ FMCG companies) |
| `/dashboard/analysis` | AI shelf analysis + USDC payment |
| `/dashboard/reports` | My saved reports |
| `/layout-editor` | 3D store layout editor |
| `/forum` | Layout marketplace |
| `/contact` | Contact form |

---

## GitHub Repositories

| Repo | Purpose |
|---|---|
| [storescope-ai](https://github.com/levanhung789/storescope-ai) | Main — Vercel deployment |
| [storescope-ai-ARC](https://github.com/levanhung789/storescope-ai-ARC) | ARC hackathon submission |

---

## Notes for ARC Team

1. **USDC Payments are real** — all payments go through ARC Testnet USDC contract `0x3600000000000000000000000000000000000000`
2. **Service wallet** (placeholder for demo): `0x1234567890123456789012345678901234567890`
3. **Tesseract.js OCR** runs client-side in browser — no server cost, works offline
4. **Roboflow model** — 1001 Vietnamese FMCG product images uploaded, model training pending (auto-label in progress)
5. **SIWE verification** — every wallet connection requires a signature with random nonce, preventing replay attacks

---

*Built for ARC Hackathon 2026 · storescope.ai*
