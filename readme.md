---

# HISA PEOPLES CHAIN

HISA PEOPLES CHAIN is a grassroots movement powered by Hedera's distributed ledger technology, connecting everyday Africans with agentic AI to address the 17 UN SDGs. It focuses on sustainability finance, ecotourism, conservation databases, telemedicine, economic inclusion, and cultural preservation through tokenized actions and rewards (e.g., $HISA, UMOJA, JANI, CULTURE tokens). Built on principles of Ubuntu, it enables ownership over data, culture, and finances, working on any device—including feature phones via USSD/SMS.

This repository contains the code for the HISA platform. Below are instructions to set it up and run locally for testing or judging.

https://hisa-chain-dapp.vercel.app/

## Prerequisites

- [Node.js](https://nodejs.org/) (version 14.0.0 or higher)
- [npm](https://www.npmjs.com/) (comes with Node.js; version 6.0.0 or higher recommended)
- [Git](https://git-scm.com/)
- A Hedera testnet account (free from [portal.hedera.com](https://portal.hedera.com)) for blockchain interactions
- Optional: [Postman](https://www.postman.com/) for API testing, or a browser for the web interface

Ensure your system has at least 4GB of RAM and a stable internet connection (for Hedera network access).

## Getting Started

Follow these steps to clone, set up, and run the project locally:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Drekahshi/HISA.git
   cd HISA
   ```

2. **Install dependencies:**
   All required packages, including the Hedera SDK (`@hashgraph/sdk`), are listed in `package.json`. Run:
   ```bash
   npm install
   ```
   > _Note: If `@hashgraph/sdk` isn't installed automatically or you need a specific version, run `npm install @hashgraph/sdk` explicitly._
   >
   > _If using Yarn: `yarn install`. This may take a few minutes._

3. **Configure Hedera and Environment:**
   HISA uses Hedera for smart contracts, token management (e.g., UMOJA for inflation hedging, JANI for conservation), and verification (e.g., AVL for AI/community consensus).
   - Copy `.env.example` to `.env` in the root directory.
   - Edit `.env` with your Hedera credentials (do NOT commit this file to Git):
     ```
     HEDERA_NETWORK=testnet  # or 'mainnet' for production
     MY_ACCOUNT_ID=0.0.123456  # Your Hedera account ID
     MY_PRIVATE_KEY=302e0201...  # Your Ed25519 private key (keep secure!)
     # Add other vars if needed, e.g., API keys for AI services or databases
     ```
   - For testing: Use Hedera testnet (free HBAR faucet available). Check network status at [status.hedera.com](https://status.hedera.com).
   - If your setup involves databases (e.g., conservation or cultural DBs), install and configure them here (e.g., MongoDB: `npm install mongoose` if not already in dependencies).

   ### Hedera Integrations and APIs
   HISA leverages Hedera's ecosystem for real-time webhooks, APIs, and third-party tools to enable features like AI-driven verification, conservation tokenization, and SDG-aligned metrics. Below are setup instructions for key integrations used in the project. These are configured via the Hedera SDK and may require additional API keys—add them to your `.env` file.

   - **Hedera Webhooks:** Used for real-time notifications (e.g., transaction confirmations, token minting events for JANI or UMOJA). 
     - Setup: Install any webhook handlers if not in dependencies (e.g., `npm install express` for a local server). Configure in code (e.g., `/src/hedera/webhooks.js`).
     - Local Testing: Run a mock webhook server: `node src/hedera/webhook-server.js`. Simulate events via Hedera Mirror Node API (add `MIRROR_NODE_URL=https://testnet.mirrornode.hedera.com` to `.env`).
     - Docs: [Hedera Mirror Node Webhooks](https://docs.hedera.com/hedera/sdks-and-apis/sdks/webhooks).

   - **Dovu:** Integrates for carbon credits and environmental data tokenization (e.g., for JANI conservation engine).
     - Setup: Add Dovu API key to `.env` (e.g., `DOVU_API_KEY=your_key_here`). Ensure `@dovu/sdk` or similar is installed via `npm install`.
     - Local Testing: Trigger a mock carbon offset: `node src/integrations/dovu-test.js`. Verify via console logs or Hedera explorer.

   - **Guardian:** For ESG reporting and tokenized securities (e.g., aligning with UMOJA's stability features).
     - Setup: Add Guardian credentials to `.env` (e.g., `GUARDIAN_API_URL=https://api.guardian.example`, `GUARDIAN_TOKEN=your_token`).
     - Local Testing: Run `npm run test-guardian` to simulate ESG data submission. Check for Hedera transaction IDs in output.
     - Docs: [Guardian on Hedera](https://docs.hedera.com/hedera/sdks-and-apis/sdks/guardian).

   - **Kabila:** Hedera-based platform for African community projects (e.g., cultural databases and governance).
     - Setup: Configure Kabila endpoint in `.env` (e.g., `KABILA_API= https://api.kabila.io`, `KABILA_KEY=your_key`).
     - Local Testing: Test community consensus flows: `node src/integrations/kabila-verify.js`. Integrates with AVL for redundancy.

   - **Hedera AI Studio ADK:** AI development kit for agentic AI features (e.g., verification in AVL, culture-aware automation).
     - Setup: Install if needed (`npm install @hedera/ai-studio-adk`). Add API key to `.env` (e.g., `HEDERA_AI_STUDIO_KEY=your_key`).
     - Local Testing: Run AI models locally: `npm run ai-studio-test`. Simulate SDG actions (e.g., tree planting verification).
     - Docs: [Hedera AI Studio](https://docs.hedera.com/hedera/sdks-and-apis/sdks/ai-studio).

   - **Eliza Plugins:** Custom plugins for chatbot/AI interactions (e.g., for mental health support or cultural storytelling in telemedicine).
     - Setup: Add plugin configs to `.env` (e.g., `ELIZA_PLUGIN_ENDPOINT=https://eliza.example`, `ELIZA_API_KEY=your_key`).
     - Local Testing: Start plugin server: `node src/plugins/eliza.js`. Test via browser console or API calls for voice/SMS interfaces.

   - **OpenCovAI:** Open-source AI for coverage/verification (e.g., health outcomes tracking, biodiversity via satellite AI).
     - Setup: Install dependencies if needed (`npm install opencovai-sdk`). Configure in `.env` (e.g., `OPENCOVAI_MODEL=health-verifier`, `OPENCOVAI_KEY=your_key`).
     - Local Testing: Run verification scripts: `node src/integrations/opencovai-test.js`. Integrates with ZK-proofs for privacy.

   **Note:** All integrations use Hedera's Consensus Service (HCS) or Token Service (HTS) for immutable records. For local dev, use testnet to avoid costs. If APIs require sign-up, get keys from their respective docs.

4. **Start the development server:**
   ```bash
   npm start
   ```
   > _Alternative: `npm run dev` if using tools like Vite or Next.js. The console will show when it's ready (e.g., "Server running on http://localhost:3000")._

5. **View and test locally:**
   - Open a browser and go to: http://localhost:3000 (or the port shown in the console).
   - For feature phone simulation: Test USSD/SMS interfaces via console logs or emulators (details in `/docs` if available).
   - Interact with Hedera features: Trigger actions like token minting or verifications—monitor transactions on [Hedera Explorer](https://hashscan.io/testnet).

The app should now be running locally, allowing you to test SDG-aligned features like tokenized actions, cultural archiving, or conservation tracking.

## Usage

- **Web Interface:** Navigate to http://localhost:3000. Log in with demo credentials (e.g., username: 'admin', password: 'password'—update with your actual demos).
- **Hedera Interactions:** Use the dashboard to simulate actions (e.g., plant a tree → mint JANI token). View on testnet explorer.
- **API Testing:** Send requests to endpoints like http://localhost:3000/api/tokenize (use Postman). For example:
  ```bash
  curl -X POST http://localhost:3000/api/verify-action -d '{"action": "plant_tree"}'
  ```
- **Inclusive Access Testing:** For feature phones, check SMS/USSD mocks in code (e.g., `/src/inclusive-access`).
- **Integration Testing:** Test webhooks by simulating events; use Postman for Dovu/Guardian APIs; run AI scripts for Hedera AI Studio or OpenCovAI.
- Refer to the SDG impact table in the project overview for metrics (e.g., verified via smart contracts).

## Build for Production

To build a production-ready version:
```bash
npm run build
```
Serve the build:
```bash
npm install -g serve
serve -s build
```
Access at http://localhost:5000.

## Folder Structure

- `/src`: Core source code (e.g., components for AI verification, token logic, SDG integrations).
- `/public`: Static assets (e.g., images for cultural database, favicons).
- `/config`: Hedera SDK configs, environment setups.
- `/docs`: Additional documentation (e.g., governance model, token economy).
- `package.json`: Dependencies and scripts.
- `.env.example`: Template for env vars.

## Troubleshooting

- **Node version issues?** Use nvm: `nvm install 14 && nvm use 14`.
- **Install fails?** Delete `node_modules` and `package-lock.json`, then `npm install`. Update npm: `npm install -g npm`.
- **Hedera errors (e.g., invalid key)?** Double-check `.env` creds. Ensure network is up. Test with minimal code: `node test-hedera.js` (if provided).
- **Integration errors (e.g., API key invalid)?** Verify keys in `.env`; check API docs for rate limits. For webhooks, ensure local server is running.
- **Port conflict?** Set `PORT=4000 npm start`.
- **AI/Verification fails?** Check internet; ensure API keys in `.env` for agentic AI services.
- **Other problems?** Check console logs. Open an [issue](https://github.com/Drekahshi/HISA/issues) with details.

## Contributing

Fork the repo, create a branch, and submit a PR. For Hedera or AI changes, discuss in an issue first.

## License

MIT License (see [LICENSE](LICENSE) file).

For questions, open an [issue on GitHub](https://github.com/Drekahshi/HISA/issues).

--- 

This addition makes the README more comprehensive for Hedera-focused setups without overwhelming the core local run instructions. If you need code snippets, links to specific docs, or adjustments (e.g., exact package names), let me know!
