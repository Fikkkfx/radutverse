# RadutVerse

Generate, register, and manage IP on the blockchain.

RadutVerse is a Web3 platform for creating and registering intellectual property on-chain. Generate AI images, register them as NFTs on Story Protocol, and manage your IP portfolio all in one place.

---

## What Works Right Now

### Live Pages
- Home: Landing page
- IP Assistant: Register IP with analysis and smart licensing, search and explore IP assets
- IP Imagine: Generate and remix existing IP with text prompts
- IP Imagine Results: View and register generated images
- My Portfolio: View your registered IP assets
- History: Chat and creation history
- Settings: Account and integration settings

### Coming Soon
- IPFi Assistant: Financial insights for IP licensing
- NFT Marketplace: Browse and trade IP-backed NFTs

### Core Features
1. Generate Images: Text-to-image using DALL-E 3 in IP Imagine (demo mode works without API keys)
2. Auto-Watermark: Generated images get a lock emoji for protection
3. Smart Licensing: Choose from 3 license types with automatic IP protection
4. Remix IP: Create derivatives with text prompts and set royalty sharing
5. Image Analysis: Vision AI analyzes creations before registration
6. Register on Story Protocol: Mint as on-chain IP with licensing terms
7. Asset Search: Find IP by title, description, or creator with detailed views
8. Portfolio Tracking: View registered assets and derivatives

---

## Quick Start

### Prerequisites
- Node.js 18+ with pnpm 10.14+
- EVM Wallet (MetaMask, Privy, etc.)

### Installation

```bash
git clone <repo>
cd radutverse
pnpm install
```

### Run

```bash
pnpm dev
```

Opens at http://localhost:5173 with hot reload.

### Important: Running on Mainnet

his application is configured to run on Story Protocol mainnet for full functionality. Testnet has limitations that make testing and comparing IP registration features difficult. On mainnet, you can register IP, test all license types, and monitor everything through Story Protocol's official tools.

Costs are minimal: hundreds of transactions use less than $0.10 of IP tokens. Use a new wallet for testing, not your main one.

### Try Demo Mode
No API keys needed:
1. Go to IP Imagine
2. Type a prompt and click generate
3. See demo image with lock emoji watermark
4. Click Register to see the flow

---

## Smart Licensing

RadutVerse uses Story Protocol to enforce licensing on-chain. When you register IP, choose a license that protects your work and enables remix revenue sharing.

### 3 License Types

**Non-Commercial Social Remix**: Best for art and hobby projects. Free remixing, no commercial use, AI training disabled, no revenue share.

**Commercial Use**: For professional work and products. Restricted remixing, commercial allowed, configurable AI training, no revenue share.

**Commercial Remix**: For collaborative work and IP trading. Paid remixing, commercial allowed, AI training disabled, you set revenue share (0-50%).

### How It Works

When you register IP:
1. Choose License Type (system recommends based on content)
2. Set Minting Fee (optional: 0-1000 units, paid by remixer)
3. Set Revenue Share (optional: 0-50%, you earn per derivative)
4. License Stored On-Chain (Story Protocol enforces automatically)

### Example

Register: Digital Landscape (Commercial Remix license)
- Minting Fee: 100 units
- Revenue Share: 20%

Creator A remixes your image:
- Pays 100 units minting fee to you
- Creates derivative and earns money
- You earn 20% of their revenue automatically

Creator B remixes Creator A's work:
- Pays another fee
- You still earn 20% from the full derivative chain

### AI Training

Non-Commercial: AI training disabled
Commercial Use: AI training disabled
Commercial Remix: AI training disabled

Images won't be used to train AI models unless you explicitly enable it.

---

## Environment Variables

### Minimal Setup (Demo Only)

```env
VITE_PRIVY_APP_ID=your_privy_app_id  # Optional: enable wallet login
```

No other keys needed for demo. Just `pnpm dev`.

### Full Setup (Production)

```env
# AI and Image Generation
OPENAI_API_KEY=sk-...                    # Required: real image generation
OPENAI_VERIFIER_MODEL=gpt-4o            # Optional: model override
OPENAI_PRIMARY_MODEL=gpt-4o-mini        # Optional: model override

# Story Protocol (Blockchain IP)
STORY_API_KEY=your_story_api_key         # Required: IP asset search
VITE_PUBLIC_STORY_RPC=https://mainnet... # Required: registration
VITE_PUBLIC_SPG_COLLECTION_USERS=0x...   # Required: minting contract

# Authentication
VITE_PRIVY_APP_ID=your_privy_app_id      # Optional: wallet auth
VITE_GUEST_PRIVATE_KEY=your_guest_key    # Optional: demo key

# Database (Persistent Storage)
VITE_SUPABASE_URL=https://...            # Required: save creations
VITE_SUPABASE_ANON_KEY=eyJhbGc...       # Required: save creations

# IPFS (Decentralized Storage)
PINATA_JWT=eyJhbGc...                    # Optional: custom IPFS gateway
PINATA_GATEWAY=your.mypinata.cloud       # Optional: custom gateway

# Deployment
PORT=8080                                 # Optional: default 3000
NODE_ENV=development                      # development or production
```

### What Keys Do I Need?

**For Demo**: None

**For Real Images**: OPENAI_API_KEY

**For Registering IP**: STORY_API_KEY, VITE_PUBLIC_STORY_RPC, VITE_PUBLIC_SPG_COLLECTION_USERS

**For Saving Work**: VITE_SUPABASE_URL, VITE_SUPABASE_ANON_KEY

**For Wallet Login**: VITE_PRIVY_APP_ID

**For Custom IPFS**: PINATA_JWT, PINATA_GATEWAY

---

## API Endpoints (27 Total)

### Image Generation (3)
- POST /api/generate-image: Generate from text prompt
- POST /api/generate-with-watermark: Generate with watermark
- POST /api/edit: Edit existing image

### Image Analysis (3)
- POST /api/analyze-image-vision: Analyze content before registration
- POST /api/vision-image-detection: Detect image type (AI, photo, etc.)
- POST /api/check-image-similarity: Find similar registered IP

### Asset Search (4)
- POST /api/search-ip-assets: Search all IP assets
- POST /api/search-by-owner: Search by creator address
- POST /api/get-asset-by-id: Get asset details
- POST /api/check-ip-assets: Get user's registered assets

### Creation Management (4)
- GET /api/wallet-creations/:walletAddress: List user's creations
- POST /api/wallet-creations: Save new creation
- POST /api/wallet-creations/:id: Update creation
- DELETE /api/wallet-creations/:id: Delete creation

### Storage and Upload (3)
- POST /api/ipfs/upload: Upload file to IPFS
- POST /api/ipfs/upload-json: Upload JSON metadata to IPFS
- POST /api/upload: Upload to Vercel Blob

### Utilities (7)
- POST /api/describe: Get AI description
- POST /api/resolve-ip-name: Look up IP by name
- POST /api/resolve-owner-domain: Look up owner domain
- POST /api/parse-search-intent: Parse search intent
- POST /api/get-suggestions: Get typing suggestions
- POST /api/capture-asset-vision: Analyze asset on click
- GET /api/ping: Health check

---

## How to Use

### Generate Images

1. Go to IP Imagine
2. Type a prompt (example: "A digital landscape with mountains and aurora")
3. Click Generate
4. Image appears with lock emoji watermark
5. Ready to use

### Register IP with Analysis

1. Go to IP Assistant
2. Upload your image
3. Type "Register" to trigger AI analysis
4. Vision AI analyzes image type, safety, and licensing recommendations
5. Choose license type:
   - Non-Commercial Social Remix (free remix, no commercial)
   - Commercial Use (restricted remix, commercial allowed)
   - Commercial Remix (paid remix, commercial, with royalties)
6. Optional: Set minting fee and revenue share (0-50%)
7. Connect wallet and confirm transaction
8. IP registered on-chain with enforced licensing

### Remix Existing IP

1. Go to IP Imagine
2. Search for IP assets by title, description, or creator
3. Click Remix on the IP you want
4. Edit the image with your own prompt
5. Generate the new image
6. Optionally register as derivative via IP Assistant
7. Story Protocol automatically tracks parent-child relationships and royalties

### Search and Explore IP Assets

1. Go to IP Assistant
2. Search by creator address, name, title, description, or keywords
3. View detailed asset information (licensing, remix history, derivatives)
4. Connect wallet to register your own IP

### View Your Portfolio

1. Go to My Portfolio
2. Connect wallet
3. View all your registered IP assets
4. See licensing terms and track derivatives

---

## Architecture

### Frontend
- React 18 + React Router 6 (SPA)
- TypeScript, TailwindCSS 3, Radix UI
- React Context + React Query for state
- Vite 7 build

### Backend
- Express 5 with TypeScript
- 27 API endpoints
- Single-port with Vite dev server

### Storage
- Browser sessionStorage: Chat history, temporary images
- localStorage: Creation cache
- Supabase PostgreSQL: Persistent creations, metadata
- IPFS via Pinata: Immutable asset storage
- Vercel Blob: Fast image delivery

### Blockchain
- Story Protocol: IP registration, licensing, derivatives
- Story Network: mainnet
- Wallet Auth: Privy or custom wallet via Viem

---

## Commands

```bash
pnpm dev              # Start dev server
pnpm build            # Build for production
pnpm start            # Run production server
pnpm typecheck        # TypeScript checking
pnpm test             # Run tests
pnpm format.fix       # Format code
```

---

## Deploy

### Vercel
```bash
vercel
```
Add env vars in dashboard, auto-deploys on git push.

### Netlify
```bash
# Set build: pnpm build
# Publish: dist/spa
netlify deploy
```

### Self-Hosted
```bash
pnpm build && pnpm start
# Runs on PORT (default 8080)
```

### Docker
```bash
docker build -t radutverse .
docker run -p 8080:8080 -e OPENAI_API_KEY=... radutverse
```

---

## Security

Good Practices:
- API keys stored server-side only
- CORS configured for trusted origins
- Input validated with Zod
- Wallet signatures verified before state changes
- XSS protection via React's escaping

Do This:
1. Never commit .env.local to version control
2. Keep API keys secret and rotate regularly
3. Validate wallet addresses before transactions
4. Monitor API logs for suspicious activity
5. Keep dependencies updated: `pnpm update`

---

## FAQ

**Can I use this without API keys?**
Yes. Demo mode works without keys. Set keys for real generation and blockchain features.

**Do I need a wallet?**
Only to register IP on-chain. You can generate images without a wallet.

**What blockchain does this use?**
Story Protocol on Story Network (mainnet). Requires VITE_PUBLIC_STORY_RPC and VITE_PUBLIC_SPG_COLLECTION_USERS.

**How does licensing work?**
Choose a license type when registering. Story Protocol enforces it. Commercial Remix lets you set minting fees and revenue share.

**Can I change my license after registering?**
No. License terms are immutable on-chain. Choose carefully.

**How do royalties work?**
If you set revenue share (e.g., 20%), you earn that percentage whenever someone creates a licensed remix of your IP. Story Protocol handles transfers.

**Can someone remix my IP without permission?**
Only if your license allows it. Non-Commercial and Commercial Remix allow remixing. Commercial Use restricts it. Story Protocol enforces this.

**Where are my images stored?**
Generated images stay in your browser until registration. Once registered, they go to IPFS (via Pinata) and Vercel Blob for CDN delivery.

**Can I use this without Supabase?**
Yes. Without Supabase, creations stay local. With Supabase, they persist across sessions and devices.

**What if I don't set OpenAI API key?**
Demo endpoints return placeholder images. Set OPENAI_API_KEY for real DALL-E 3 generation.

**Is this fully decentralized?**
Partially. UI and generation use centralized services (React, OpenAI), but IP ownership and licensing is fully on-chain via Story Protocol.

---

## Resources

- Story Protocol: https://docs.story.foundation/
- OpenAI: https://platform.openai.com/docs
- Supabase: https://supabase.com/docs
- Privy: https://docs.privy.io
- Viem: https://viem.sh
- React Router: https://reactrouter.com/
- TailwindCSS: https://tailwindcss.com/

---

## License

© 2025 RadutVerse Contributors

---

Start building your IP empire on Web3. No gatekeepers.
