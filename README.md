# Repository Cleared
🌐 Live Demo: www.luckyhash.fun

🎰 Block Hash Lottery - Decentralized Lottery Platform
A fully automated, transparent lottery system built on Polygon blockchain using block hash randomness

⚠️ Important Notice
This project is currently in active development and testing phase. While the smart contract is deployed on Polygon mainnet with real funds for testing purposes, please be aware that this is still an experimental system. Participation is welcome but please only risk what you can afford to lose during this development phase.

🌟 Portfolio Highlights
This project demonstrates:

Smart Contract Development (Solidity 0.8.20)
DeFi Mechanics (Pari-mutuel betting system with dual escrow)
Full-Stack DApp Development (Next.js + Web3)
Blockchain Automation (Cron-based bot)
Security Best Practices (ReentrancyGuard, Access Control, Emergency Recovery)
Advanced Fund Management (Dual escrow system preventing fund lock)
🏗️ Architecture Overview
┌─────────────────┐     ┌──────────────┐     ┌─────────────┐
│   Smart         │────▶│   Frontend   │────▶│   Users     │
│   Contract      │     │   (Next.js)  │     │  (MetaMask) │
└────────┬────────┘     └──────────────┘     └─────────────┘
         │
         │ Auto-draw
         ▼
┌─────────────────┐
│   Runner Bot    │
│   (Node.js)     │
└─────────────────┘
🎯 Core Features
Smart Contract (SimpleLotteryV6)
Dual Escrow System: Separate fee escrow and rollover escrow for complete transparency
Transparent Randomness: Uses block hash for verifiable random number generation
Automatic Rollover: Unclaimed prizes safely stored in rollover escrow
Fair Distribution: 75% prize pool, 25% platform fee with independent management
Emergency Recovery: Guaranteed fund recovery with time-locked emergency withdrawal
Gas Optimized: Efficient storage patterns and batch operations
Zero Fund Lock Risk: All funds trackable and recoverable in any scenario
Frontend
Web3 Integration: RainbowKit + wagmi for seamless wallet connection
Real-time Updates: Live round status and betting information
Responsive Design: Mobile-friendly interface with Tailwind CSS
TypeScript: Full type safety across the application
Automation
Autonomous Operation: Bot automatically draws rounds when they expire
Self-Sustaining: Starts new rounds without manual intervention
Monitoring: Logs all activities for transparency
💻 Technical Stack
Blockchain: Polygon (POL)
Smart Contracts: Solidity 0.8.20, Hardhat, OpenZeppelin
Frontend: Next.js 15, TypeScript, Tailwind CSS
Web3: ethers.js, wagmi, RainbowKit
Backend: Node.js automation bot
Testing: Comprehensive Hardhat test suite with edge cases and fund recovery scenarios
📊 Business Model & Fund Flow
Every Ticket (0.1 ETH/POL)
├── 75% → Rollover Escrow (Prize Pool)
└── 25% → Fee Escrow (Platform Revenue)

If No Winners → Prize Pool Safely Rolls Over
If Winners → Prize Pool + Accumulated Rollover Distributed

Dual Escrow Benefits:
- Owner can withdraw fees independently
- Prize pool protected from fee operations
- Complete fund tracking and transparency
🔧 Key Code Snippets
Smart Contract V6 - Dual Escrow System
// Dual escrow separation for transparency
uint256 public feeEscrow;        // 25% fees for owner
uint256 public rolloverEscrow;   // 75% prize pool

function drawRound() external {
    // Fee escrow (25%) - owner can withdraw anytime
    feeEscrow += feeAmount;
    
    if (winnerCount > 0) {
        // Distribute rollover + current prize
        uint256 totalPrize = rolloverEscrow + prizeAmount;
        distributeToWinners(totalPrize);
        rolloverEscrow = 0;
    } else {
        // No winners - safely accumulate in rollover
        rolloverEscrow += prizeAmount;
    }
}
Emergency Recovery System
function emergencyWithdraw() external {
    // Guaranteed fund recovery even in emergency
    uint256 refund = playerEscrowBalances[msg.sender];
    require(refund > 0, "Nothing to refund");
    playerEscrowBalances[msg.sender] = 0;
    payable(msg.sender).transfer(refund);
}
🚀 Quick Start (Development)
# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run comprehensive tests (including V6 critical scenarios)
npx hardhat test

# Test V6 specifically with edge cases
npx hardhat test test/SimpleLotteryV6-Critical.test.js

# Start local blockchain
npx hardhat node

# Deploy V6 locally
npx hardhat run scripts/deploy-v6.js --network localhost

# Start frontend
cd frontend && npm run dev
🔄 Contract Evolution & Improvements
Version History
V1-V3: Initial implementations with various fund management approaches
V4: Added rollover mechanism and basic escrow
V5: Introduced 25% fee structure with immediate owner transfer
V6 (Current): Dual escrow system with complete fund safety
Key Problems Solved
V2 Issue: Emergency stop caused fund lock → V6 Solution: Player escrow preserves betting state
V3 Issue: Immediate fee transfer caused insufficient balance → V6 Solution: Dual escrow separation
Fund Tracking: All funds now 100% trackable through escrow system
Emergency Recovery: Time-locked withdrawal ensures fund safety
📈 Performance Metrics
Scalability: Supports unlimited participants per round
Uptime: Designed for 24/7 autonomous operation
Security: Comprehensive testing with all edge cases covered
Fund Safety: 100% fund recovery guarantee in any scenario
🔐 Security Features
✅ ReentrancyGuard for withdrawal protection
✅ Ownable for admin functions
✅ Dual escrow system preventing fund commingling
✅ Emergency withdrawal with time-lock protection
✅ No external dependencies for randomness
✅ Immutable lottery rules
✅ Transparent fee structure
✅ Complete fund tracking and recovery mechanisms
✅ Protection against stuck funds (solved V2/V3 issues)
🎓 Learning Outcomes
Through this project, I demonstrated proficiency in:

Solidity Development

State management and gas optimization
Security patterns and best practices
Event-driven architecture
Full-Stack Integration

Web3 provider management
Transaction handling and confirmation
Real-time blockchain data synchronization
DeFi Concepts

Tokenomics and fee structures
Liquidity management (rollovers)
Fair distribution mechanisms
DevOps & Automation

Smart contract deployment pipelines
Automated testing strategies
Continuous operation systems
🔍 Code Quality
Test Coverage: Comprehensive testing including edge cases
Critical Scenario Testing: Emergency stops, fund recovery, rollover scenarios
Documentation: Comprehensive NatSpec comments
Code Style: Follows Solidity and JavaScript best practices
Type Safety: Full TypeScript implementation
Version Evolution: V1 → V6 with continuous improvements and bug fixes
📝 Note for Recruiters
This repository contains the core components of a production-ready DApp. Some operational scripts and deployment configurations have been excluded for security reasons. The codebase demonstrates:

Clean, maintainable code architecture
Understanding of blockchain economics
Ability to build complete Web3 solutions
Security-first development approach
🤝 Contact
For detailed implementation discussions or live demo:

Email: [binarybard10101@gmail.com]
⚖️ License
This project is provided for portfolio review purposes. Commercial use requires explicit permission.