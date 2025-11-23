## Inspiration
Our inspiration came from a shared interest in building technology that combines **AI**, **software engineering**, and **finance** in a meaningful way. As we reviewed the categories and sponsor challenges in this year’s Hackathon, Solana immediately stood out not only because of its real-world impact, but it presented the **greatest technical challenge**. With very few recent projects and a steep learning curve, building on Solana pushed us far outside our comfort zone. That challenge itself became our motivation.

## What it does
Our platform allows users to participate in **cryptographically secure polls** with Solana wallet integration and AI-powered analysis.

Users begin by connecting their crypto wallet — we support **Phantom**, **Solflare**, and **Backpack** via the Solana Wallet Adapter. Once authenticated through their wallet signature, users are redirected back to our app where their identity is cryptographically verified. They can then browse available polls and cast a vote.

Each vote is:
- **Signed** by the user's wallet (cryptographic signature)  
- **Securely stored** with signature verification  
- **Protected** through cryptographic authentication

The result is a transparent polling system with wallet-based authentication and AI-powered fraud detection. While we have deployed a Solana program for on-chain voting, the current implementation uses off-chain storage with cryptographic signatures for security and transparency.

## How we built it
Our tech stack is composed of three main components:

### **Frontend**
- React + TypeScript
- Solana Wallet Adapter integration
- Realtime UI updates with account polling

### **Backend (Python FastAPI)**
- API endpoints to handle signed votes and cryptographic verification
- AI agent orchestration for poll analysis
- Database integration for vote storage and retrieval

### **Solana (On-chain)**
- Anchor framework (Rust) for rapid development
- Custom Solana program deployed and ready for on-chain voting
- On-chain program architecture for future full decentralization

## Challenges we ran into
Our biggest challenge was building and deploying the **Solana on-chain program**.  
Solana development involves:
- learning the Anchor framework  
- managing PDAs and account constraints  
- understanding serialization and on-chain state  
- dealing with cryptic compiler errors  

Solana also had fewer active resources and examples, which made debugging difficult. Integrating wallet authentication, cryptographic signatures, and our backend required us to deeply understand how Web3 authentication flows work across frontend and backend layers.

## Accomplishments that we're proud of
We are incredibly proud that we successfully:
- deployed a **Solana program** using Anchor framework,  
- integrated **multi-wallet authentication** (Phantom, Solflare, Backpack),  
- built **cryptographic signature verification** for secure voting,  
- created **AI-powered analysis agents** for fraud detection, and  
- connected all layers of our system into a polished final product.

For all of us, Solana was new territory — accomplishing this in under 36 hours is something we consider a major achievement.

## What we learned
We learned how **centralized polling systems depend on trust** — trust in servers, databases, and admins — and how easily those systems can be manipulated.  
By contrast, building with Solana wallet integration helped us understand how cryptographic signatures, wallet-based authentication, and transparent verification create **more secure and verifiable voting systems**.

We also gained hands-on experience with:
- Rust & Anchor  
- multi-wallet integrations (Phantom, Solflare, Backpack)  
- cryptographic signature verification  
- AI agent development (Gemini API)  
- cross-system communication between Web2 and Web3 components  

This was our first time working with Solana, and it gave us a deeper appreciation for blockchain engineering.

## What's next for Gov AI: Decentralized Polling System
We want to expand this project beyond a hackathon prototype by:
- **completing on-chain integration** - migrating votes to fully on-chain storage using our deployed Solana program  
- adding **multi-option polls** and large-scale vote aggregation  
- enhancing **AI agents** with more sophisticated fraud detection patterns  
- allowing communities or organizations to **create their own polls** through our platform  
- improving UI/UX for smoother wallet onboarding  
- deploying the system on Solana Mainnet with better performance optimizations  

Our long-term vision is to create a **trustless governance platform** that empowers communities, organizations, and DAOs to make transparent and verifiable decisions at scale. 