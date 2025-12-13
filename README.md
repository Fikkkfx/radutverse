# RadutVerse

Generate, register, and manage IP on the blockchain.

RadutVerse is a Web3 platform for creating and registering intellectual property on-chain. Generate AI images, register them as NFTs on Story Protocol, and manage your IP portfolio all in one place.

---

## What Works Right Now

### Pages Live and Functional
- Home at the root path — Landing page
- IP Assistant at /ip-assistant — Register IP with analysis and smart licensing, search and explore IP assets
- IP Imagine at /ip-imagine — Generate and remix existing IP, with text prompts
- IP Imagine Results at /ip-imagine/result — View and register your generated images
- My Portfolio at /my-portfolio — View your registered IP assets
- History at /history — Chat and creation history
- Settings at /settings — Account and integration settings

### Pages Coming Soon
- IPFi Assistant — Financial insights for IP licensing
- NFT Marketplace — Browse and trade IP-backed NFTs

### Core Features
1. Generate Images — Text-to-image using DALL-E 3 in IP Imagine (demo mode works without API keys)
2. Auto-Watermark — Generated images get a visible lock emoji for protection
3. Smart Licensing — Choose from 3 license types with automatic IP protection
4. Remix IP — Create derivatives with text prompts in IP Imagine and set royalty sharing
5. Image Analysis — Vision AI analyzes creations before registration in IP Assistant
6. Register on Story Protocol — Mint as on-chain IP with licensing terms via IP Assistant
7. Asset Search — Find IP by title, description, or creator in IP Assistant with detailed asset views
8. Portfolio Tracking — View registered assets and derivatives in My Portfolio

---

## Quick Start

### Prerequisites
- Node.js 18 or newer with pnpm 10.14 or newer
- EVM Wallet like MetaMask or Privy

### Installation

```bash
# Clone and install
git clone <repo>
cd radutverse
pnpm install

# Create .env.local (see the section below)
```

### Run Development Server

```bash
pnpm dev
```

Opens at http://localhost:5173 with hot reload.

### Important Mainnet Notice

This application is configured to run on Story Protocol mainnet for full functionality. Testnet has limitations that make testing and comparing IP registration features difficult. On mainnet, you can register IP, test all license types, and monitor everything through Story Protocol's official tools.

Transaction costs are minimal. Hundreds of transactions will not consume even 0.1 dollars worth of IP tokens. For safety, use a new wallet dedicated to testing rather than your primary wallet.

### Try It Out Demo Mode
No API keys required to try:
1. Go to IP Imagine
2. Type a prompt and click generate
3. Watch the demo image appear with a lock emoji watermark
4. Click Register to see the registration flow requires keys to actually submit

---

## Smart Licensing

RadutVerse uses Story Protocol to enforce licensing on-chain. When you register your IP, you choose a license that automatically protects your work and enables remix revenue sharing.

### 3 License Types

Non-Commercial Social Remix works best for art and hobby projects. Remixing is free, commercial use is not allowed, AI training is disabled, and no revenue share applies.

Commercial Use is for professional work and products. Remixing is restricted, commercial use is allowed, AI training can be configured, and no revenue share applies.

Commercial Remix is for collaborative work and IP trading. Remixing is paid, commercial use is allowed, AI training is disabled, and you can set a revenue share from 0 to 50 percent.

### How It Works

When you register your IP:

1. Choose License Type — System recommends based on content (AI-generated, human-made, etc.)
2. Set Minting Fee (optional) — One-time fee when someone remixes your IP (0-1000 units)
3. Set Revenue Share (optional) — Royalty percentage for derivatives (0-50%)
4. License Stored On-Chain — Story Protocol enforces automatically

### Example

You register: Digital Landscape
Selected: Commercial Remix license
- Minting Fee: 100 units (paid by remixer)
- Revenue Share: 20 percent (you get 20 percent of remixer's earnings)

Creator A remixes your image
- Pays 100 unit minting fee → You receive this
- Creates derivative and earns money
- You earn 20 percent of their revenue automatically

Creator B remixes Creator A's work
- Pays another fee
- You still earn your 20 percent from the derivative chain

### AI Training Control

Non-Commercial always has AI training disabled.
Commercial Use has no AI training allowed.
Commercial Remix has AI training disabled.

Your images won't be used to train commercial AI models unless you explicitly enable it.

---

## Environment Variables

### Minimal Setup Demo Only

Optional key that enables wallet login but the app still works without it:
VITE_PRIVY_APP_ID=your_privy_app_id

No other keys needed for demo mode. Just pnpm dev and try the app!

### Full Setup Production

AI and Image Generation:
OPENAI_API_KEY=sk-...  Required for real image generation and analysis
OPENAI_VERIFIER_MODEL=gpt-4o  Optional model override (defaults provided)
OPENAI_PRIMARY_MODEL=gpt-4o-mini  Optional model override (defaults provided)

Story Protocol (Blockchain IP):
STORY_API_KEY=your_story_api_key  Required for IP asset search
VITE_PUBLIC_STORY_RPC=https://mainnet.storyrpc.io  Required for registration
VITE_PUBLIC_SPG_COLLECTION_USERS=0x98971...  SPG contract address

Authentication:
VITE_PRIVY_APP_ID=your_privy_app_id  Optional (app works without it)
VITE_GUEST_PRIVATE_KEY=your_guest_key  Optional demo private key

Database (Persistent Storage):
VITE_SUPABASE_URL=https://project.supabase.co  Required for saved creations
VITE_SUPABASE_ANON_KEY=eyJhbGc...  Required for saved creations

IPFS (Decentralized Storage):
PINATA_JWT=eyJhbGc...  Optional (custom IPFS gateway)
PINATA_GATEWAY=your.mypinata.cloud  Optional (custom IPFS gateway)

Deployment and Server:
PORT=8080  Optional (default: 3000)
NODE_ENV=development  development or production

### Which Keys Do I Actually Need

For Demo (generates dummy images):
None required

For Real Generation:
OPENAI_API_KEY — Must have this to generate real images

For Story Protocol Features (search assets, register IP):
STORY_API_KEY — Search and view IP assets
VITE_PUBLIC_STORY_RPC — Blockchain RPC endpoint
VITE_PUBLIC_SPG_COLLECTION_USERS — Contract address for minting

For Saving Your Work (persistent storage):
VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY — Save creations to database

For Wallet Login:
VITE_PRIVY_APP_ID — Enable Privy wallet authentication (optional)

For IPFS/Pinata (optional):
PINATA_JWT and PINATA_GATEWAY — Use Pinata IPFS gateway (fallback to ipfs.io)

---

## API Endpoints 27 Working

### Image Generation (3)
POST /api/generate-image — Generate from text prompt
POST /api/generate-with-watermark — Generate with watermark
POST /api/edit — Edit existing image

### Image Analysis (3)
POST /api/analyze-image-vision — Analyze content before registration
POST /api/vision-image-detection — Detect image type (AI, photo, etc)
POST /api/check-image-similarity — Find similar registered IP

### Asset Search (4)
POST /api/search-ip-assets — Search all IP assets
POST /api/search-by-owner — Search by creator address
POST /api/get-asset-by-id — Get asset details
POST /api/check-ip-assets — Get user's registered assets

### Creation Management (4)
GET /api/wallet-creations/:walletAddress — List user's creations
POST /api/wallet-creations — Save new creation
POST /api/wallet-creations/:id — Update creation
DELETE /api/wallet-creations/:id — Delete creation

### Storage and Upload (3)
POST /api/ipfs/upload — Upload file to IPFS
POST /api/ipfs/upload-json — Upload JSON metadata to IPFS
POST /api/upload — Upload to Vercel Blob

### Utilities (7)
POST /api/describe — Get AI description of image
POST /api/resolve-ip-name — Look up IP by name
POST /api/resolve-owner-domain — Look up owner domain
POST /api/parse-search-intent — Parse search query intent
POST /api/get-suggestions — Get typing suggestions
POST /api/capture-asset-vision — Analyze asset on click
GET /api/ping — Health check

---

## How to Use

### Generate Images with AI

1. Go to IP Imagine
2. Type a prompt like A digital landscape with mountains and aurora
3. Click Generate
4. Watch your image appear with a lock emoji watermark for protection
5. Your generated image is now ready to use

### Register IP with Analysis and Smart Licensing

1. Go to IP Assistant
2. Upload your image (generated or created elsewhere)
3. Type Register to trigger AI analysis
4. Vision AI analyzes:
   - Image type (AI-generated, human-made, photo, etc.)
   - Content safety and licensing recommendations
   - Asset classification
5. Choose your license type:
   - Non-Commercial Social Remix (free to remix, no commercial use)
   - Commercial Use (restricted remix, commercial allowed)
   - Commercial Remix (paid remix, commercial allowed, with royalties)
6. Optional: Set minting fee and revenue share percentage (0-50%)
7. Connect wallet and confirm transaction
8. IP registered on-chain with enforced licensing

### Remix Existing IP

1. Go to IP Imagine
2. Use the search feature to find IP assets by title, description, or creator
3. Find an IP you want to remix
4. Click Remix to create a derivative
5. Edit the image with your own prompt or modifications
6. Generate the new image with your changes
7. Choose to register as a derivative (via IP Assistant)
8. Story Protocol automatically tracks:
   - Parent-child relationship
   - Royalty distribution
   - Creator attribution
9. Original creator earns royalties automatically from your derivative sales

### Search and Explore IP Assets

1. Go to IP Assistant
2. Search for IP by:
   - Creator address or name
   - Title or description
   - Any keywords related to content
3. View detailed information about each asset:
   - Licensing terms
   - Creator information
   - Remix history
   - Derivative tracking
4. Connect wallet to register your own IP with analysis

### View Your Portfolio

1. Go to My Portfolio
2. Connect wallet
3. View all your registered IP assets
4. See licensing terms and metadata
5. Track derivatives created from your work

---

## Architecture

### Frontend
- Framework: React 18 plus React Router 6 (SPA)
- Language: TypeScript
- Styling: TailwindCSS 3 plus Radix UI
- State: React Context plus React Query
- Build: Vite 7

### Backend
- Framework: Express 5
- Language: TypeScript
- Port: 3000 (dev) or PORT env var (prod)
- APIs: 27 endpoints
- Integration: Single-port with Vite dev server

### Storage Layers
- Session: Browser sessionStorage (chat history, temporary images)
- Local: localStorage (creation cache)
- Database: Supabase PostgreSQL (persistent creations, metadata)
- Files: IPFS via Pinata (immutable asset storage)
- CDN: Vercel Blob (fast image delivery)

### Blockchain
- Story Protocol: IP registration, licensing, derivatives
- Network: Story Network (testnet/mainnet)
- Wallet Auth: Privy (optional) or custom wallet via Viem

---

## Development Commands

```bash
pnpm dev              # Start dev server (frontend and backend)
pnpm build            # Build for production
pnpm start            # Run production server
pnpm typecheck        # TypeScript type checking
pnpm test             # Run tests with Vitest
pnpm format.fix       # Format code with Prettier
```

---

## Deployment

### Vercel Recommended

```bash
vercel
```
Add environment variables in Vercel dashboard. Auto-deploys on git push.

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

## Security Notes

Good Practices:
- API keys stored server-side only (never exposed to frontend)
- CORS configured for trusted origins
- Input validated with Zod schemas
- Wallet signatures verified before state changes
- XSS protection via React's escaping

What You Should Do:
1. Never commit .env.local to version control
2. Keep API keys secret (rotate them regularly)
3. Validate wallet addresses before transactions
4. Monitor API logs for suspicious activity
5. Keep dependencies updated: pnpm update

---

## Frequently Asked Questions

Can I use this without API keys?
Yes. Demo mode works without any keys. You'll see placeholder images, but the UI functions perfectly. Set keys to use real image generation and blockchain features.

Do I need a wallet?
Only to register IP on-chain. You can generate images and use the app without a wallet (in demo mode).

What blockchain does this use?
Story Protocol on Story Network (testnet or mainnet). Requires VITE_PUBLIC_STORY_RPC and VITE_PUBLIC_SPG_COLLECTION_USERS.

How does licensing work?
When you register IP, you choose a license type (Non-Commercial Social Remix, Commercial Use, or Commercial Remix). Story Protocol enforces it automatically. Commercial Remix lets you set minting fees and revenue share (0-50 percent) for remixes.

Can I change my license after registering?
No. License terms are immutable on-chain. Choose carefully before registering.

How do royalties work?
If you set revenue share (for example, 20 percent), you automatically earn that percentage whenever someone creates a licensed remix of your IP. Story Protocol handles transfers directly to your wallet.

Can someone remix my IP without permission?
Only if your license allows remixing. Non-Commercial and Commercial Remix allow it. Commercial Use restricts remixing. Story Protocol enforces these rules automatically.

Where are my images stored?
Generated images are stored as data URLs in your browser until you register them. Once registered, they go to IPFS (via Pinata) and Vercel Blob for CDN delivery.

Can I use this without Supabase?
Yes. Creations stay local without Supabase. With Supabase, they persist across sessions and devices.

What if I don't set OpenAI API key?
Demo endpoints return placeholder images. Set OPENAI_API_KEY to generate real images with DALL-E 3.

Is this fully decentralized?
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
