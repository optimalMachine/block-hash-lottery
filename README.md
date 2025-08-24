# Block Hash Lottery - Decentralized Lottery Platform

> A fully automated, transparent lottery system built on Polygon blockchain using block hash randomness

**Live Demo**: [www.luckyhash.fun](https://www.luckyhash.fun)

## Important Notice
This project is currently in active development and testing phase. While the smart contract is deployed on Polygon mainnet with real funds for testing purposes, please be aware that this is still an experimental system. Participation is welcome but please only risk what you can afford to lose during this development phase.

## Portfolio Highlights

This project demonstrates:
- **Smart Contract Development** (Solidity 0.8.20)
- **DeFi Mechanics** (Pari-mutuel betting system with dual escrow)
- **Full-Stack DApp Development** (Next.js + Web3)
- **Blockchain Automation** (Cron-based bot)
- **Security Best Practices** (ReentrancyGuard, Access Control, Emergency Recovery)
- **Advanced Fund Management** (Dual escrow system preventing fund lock)
- **Iterative Problem Solving** (V1-V6 evolution with critical bug fixes)

## Contract Evolution Journey (V1 - V6)

### Version 1: Basic Implementation
**Features:**
- Simple lottery with fixed bet amount
- Basic random number generation using block hash
- Manual round management

**Issues:**
- No automated drawing
- Limited fund management
- No fee structure

### Version 2: Enhanced with Emergency System  
**New Features:**
- Added emergency stop functionality
- Improved state management
- Better player tracking

**Critical Issue Found:**
- **Bug**: `emergencyStop()` resets player betting records
- **Impact**: 1.125 POL permanently locked
- **Result**: Funds only recoverable after 30 days via `recoverUnclaimedPrizes()`

### Version 3: Fee Management System
**New Features:**
- Introduced 25% platform fee
- Immediate fee transfer to owner
- Enhanced prize distribution

### Version 4: Rollover Mechanism
**New Features:**
- Added prize rollover when no winners
- Basic escrow implementation
- Improved fund tracking

**Variations:**
- **V4Fixed**: Too conservative (0% fee, full refunds)
- **V4Final**: Balanced approach (10% fee with rollover)

### Version 5: Optimized Fee Structure
**New Features:**
- Restored 25% fee structure
- Immediate owner transfer for fees
- Enhanced rollover system

**Remaining Issue:**
- Still vulnerable to fund tracking issues
- Single escrow mixing fees and prizes

### Version 6: Dual Escrow System (Current)
**Revolutionary Changes:**
- **Dual Escrow Architecture**: Separate fee escrow and rollover escrow
- **Complete Fund Safety**: All funds trackable and recoverable
- **Emergency Recovery**: Time-locked withdrawal system
- **State Preservation**: Player records maintained during emergency

**Problems Solved:**
- ✓ V2 fund lock issue completely resolved
- ✓ V3 balance insufficiency eliminated
- ✓ 100% fund tracking accuracy
- ✓ Zero fund lock risk

## Architecture Overview

```
┌──────────────────┐     ┌──────────────┐     ┌──────────────┐
│   Smart         │←────→│   Frontend   │←────→│   Users      │
│   Contract V6   │     │   (Next.js)  │     │  (MetaMask)  │
└────────┬─────────┘     └──────────────┘     └──────────────┘
         │
         │ Auto-draw
         ↓
┌──────────────────┐
│   Runner Bot     │
│   (Node.js)      │
└──────────────────┘
```

## Core Features (V6)

### Smart Contract - SimpleLotteryV6
- **Dual Escrow System**: Separate fee escrow (25%) and rollover escrow (75%)
- **Transparent Randomness**: Block hash-based verifiable RNG
- **Automatic Rollover**: Unclaimed prizes safely stored in dedicated escrow
- **Fair Distribution**: Independent management of fees and prizes
- **Emergency Recovery**: Guaranteed fund recovery with 24-hour time-lock
- **Gas Optimized**: Efficient storage patterns and batch operations
- **Zero Fund Lock Risk**: All funds trackable and recoverable in any scenario

### Frontend
- **Web3 Integration**: RainbowKit + wagmi for seamless wallet connection
- **Real-time Updates**: Live round status and betting information
- **Responsive Design**: Mobile-friendly interface with Tailwind CSS
- **TypeScript**: Full type safety across the application

### Automation
- **Autonomous Operation**: Bot automatically draws rounds when they expire
- **Self-Sustaining**: Starts new rounds without manual intervention
- **Monitoring**: Comprehensive logging for transparency

## Technical Stack

- **Blockchain**: Polygon (POL)
- **Smart Contracts**: Solidity 0.8.20, Hardhat, OpenZeppelin
- **Frontend**: Next.js 15, TypeScript, Tailwind CSS
- **Web3**: ethers.js, wagmi, RainbowKit
- **Backend**: Node.js automation bot
- **Testing**: Comprehensive test suite with edge cases and critical scenarios

## Business Model & Fund Flow

```
Every Ticket (0.1 ETH/POL)
├── 25% → Fee Escrow (Platform Revenue)
└── 75% → Rollover Escrow (Prize Pool)

Fund Flow:
1. Players bet → Funds collected
2. Round ends → Dual escrow distribution
3. If winners → Prize pool + rollover distributed
4. If no winners → Prize pool added to rollover
5. Owner can withdraw from fee escrow anytime

Dual Escrow Benefits:
✓ Complete separation of fees and prizes
✓ Owner operations don't affect player funds
✓ 100% transparent fund tracking
✓ No risk of insufficient balance for winners
```

## Quick Start (Development)

```bash
# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run comprehensive tests (including V6 critical scenarios)
npx hardhat test

# Test V6 edge cases specifically
npx hardhat test test/SimpleLotteryV6-Critical.test.js

# Start local blockchain
npx hardhat node

# Deploy V6 locally
npx hardhat run scripts/deploy-v6.js --network localhost

# Start frontend
cd frontend && npm run dev
```

## Security Features

- ✓ ReentrancyGuard for withdrawal protection
- ✓ Ownable for admin functions
- ✓ Dual escrow preventing fund commingling
- ✓ Emergency withdrawal with 24-hour time-lock
- ✓ No external dependencies for randomness
- ✓ Immutable lottery rules
- ✓ Complete fund tracking mechanisms
- ✓ Protection against all V2/V3 vulnerabilities

## Performance Metrics

- **Scalability**: Unlimited participants per round
- **Uptime**: 24/7 autonomous operation
- **Security**: All critical scenarios tested and passed
- **Fund Safety**: 100% recovery guarantee
- **Gas Efficiency**: Optimized for Polygon network

## Test Coverage

### Critical Scenarios Validated
- ✓ Emergency stop with full fund recovery (V2 fix)
- ✓ Owner fee withdrawal with sufficient balance (V3 fix)
- ✓ Multiple consecutive rollovers
- ✓ Extreme fund flow scenarios
- ✓ Time-locked emergency withdrawals
- ✓ Dual escrow integrity

## Learning Outcomes

Through this iterative development process (V1-V6), I demonstrated:

1. **Problem-Solving Skills**
   - Identified critical vulnerabilities in V2/V3
   - Designed comprehensive solutions
   - Implemented fail-safe mechanisms

2. **Smart Contract Security**
   - State management best practices
   - Fund safety guarantees
   - Emergency recovery systems

3. **DeFi Architecture**
   - Escrow-based fund management
   - Transparent fee structures
   - Fair distribution mechanisms

4. **Testing & Validation**
   - Edge case identification
   - Comprehensive test suites
   - Real-world scenario simulation

## Key Improvements Summary

| Version | Key Feature | Problem Solved |
|---------|------------|----------------|
| V1 | Basic lottery | Initial implementation |
| V2 | Emergency system | Added safety (but had fund lock bug) |
| V3 | Fee management | Revenue model (but had balance bug) |
| V4 | Rollover system | Prize accumulation |
| V5 | Optimized fees | Better balance |
| V6 | Dual escrow | All problems solved ✓ |

## Code Quality

- **Test Coverage**: Comprehensive with all edge cases
- **Documentation**: Full NatSpec comments
- **Code Style**: Solidity & JavaScript best practices
- **Type Safety**: Complete TypeScript implementation
- **Audit Ready**: Clean, maintainable, secure code

## Financial Safety Guarantees

```
V6 Guarantees:
✓ Funds never locked (V2 issue solved)
✓ Always sufficient balance (V3 issue solved)
✓ 100% fund tracking accuracy
✓ Emergency recovery available
✓ Owner and player funds completely separated
```

## Contact

For detailed implementation discussions or technical inquiries:
- **Email**: binarybard10101@gmail.com
- **Live Demo**: [www.luckyhash.fun](https://www.luckyhash.fun)

## License

This project is provided for portfolio demonstration and educational purposes.
Commercial use requires explicit permission.

