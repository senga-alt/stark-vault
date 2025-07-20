# StarkVault - Advanced Bitcoin Liquid Staking Protocol

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Clarity](https://img.shields.io/badge/Clarity-3.1-orange.svg)](https://clarity-lang.org/)
[![Tests](https://img.shields.io/badge/Tests-Vitest-green.svg)](https://vitest.dev/)

## 🌟 Overview

StarkVault represents the next generation of Bitcoin staking solutions, combining cutting-edge yield farming strategies with robust security measures. Built on the Stacks blockchain using Clarity smart contracts, it provides a revolutionary DeFi infrastructure enabling seamless Bitcoin staking with automated yield optimization, dynamic risk assessment, and comprehensive insurance coverage for both institutional and retail participants.

## 🎯 Key Features

- **🔄 Dynamic Yield Optimization**: Real-time APY adjustments with intelligent yield distribution
- **🛡️ Risk Assessment System**: Sophisticated risk scoring algorithms for enhanced security
- **🏦 Insurance Coverage**: Comprehensive insurance fund for asset protection
- **🪙 SIP-010 Compliance**: Fully compliant liquid staking tokens (stBTC)
- **📊 Transparent Rewards**: Clear reward distribution and claiming mechanisms
- **🏢 Enterprise-Grade**: Institutional-level security and governance controls
- **⚡ Automated Distribution**: Smart contract-driven yield distribution system

## 🏗️ System Architecture

### Core Components

```text
┌─────────────────────────────────────────────────────────────┐
│                    StarkVault Protocol                      │
├─────────────────┬──────────────────┬────────────────────────┤
│  Staking Layer  │   Yield Engine   │   Insurance Module     │
│                 │                  │                        │
│ • Stake/Unstake │ • APY Calculation│ • Coverage Management  │
│ • Balance Mgmt  │ • Distribution   │ • Risk Assessment     │
│ • Token Minting │ • Reward Claims  │ • Fund Management     │
└─────────────────┴──────────────────┴────────────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │   SIP-010 Token   │
                    │    (stBTC)        │
                    │                   │
                    │ • Transfer        │
                    │ • Balance Query   │
                    │ • Metadata        │
                    └───────────────────┘
```

### Contract Architecture

The StarkVault protocol consists of a single, comprehensive smart contract with the following architectural layers:

#### 1. **Token Layer (SIP-010 Compliance)**

- Implements standard token functions (`transfer`, `get-balance`, `get-total-supply`)
- Manages stBTC (Staked Bitcoin) token representation
- Handles token metadata and URI management

#### 2. **Staking Engine**

- **Stake Function**: Processes Bitcoin deposits and mints stBTC tokens
- **Unstake Function**: Burns stBTC tokens and releases Bitcoin
- **Balance Management**: Tracks individual staker positions
- **Minimum Stake Enforcement**: Ensures 0.01 BTC minimum stake requirement

#### 3. **Yield Distribution System**

- **Automated Calculations**: Time-based yield computation using block heights
- **Distribution History**: Immutable record of all yield distributions
- **Rate Management**: Dynamic APY adjustments by contract owner
- **Reward Claims**: Individual staker reward claiming mechanism

#### 4. **Risk Management Module**

- **Dynamic Risk Scoring**: Algorithmic risk assessment based on stake size
- **Insurance Integration**: Optional coverage for staker protection
- **Security Controls**: Multi-layer authorization and validation

## 📊 Data Flow

### Staking Process

```text
User Bitcoin → stake() → Risk Assessment → stBTC Minting → Insurance Setup
     ↓
Staker Balance Update → Total Supply Update → Event Emission
```

### Yield Distribution

```text
Owner Trigger → Time Validation → Yield Calculation → Distribution Update
     ↓
History Recording → Total Yield Update → Block Height Update
```

### Reward Claiming

```text
User Request → Balance Verification → Reward Calculation → Balance Update
     ↓
Zero Rewards → Transfer to Staker → Event Emission
```

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) CLI tool
- Node.js (v16 or higher)
- npm or yarn package manager

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/senga-alt/stark-vault.git
   cd stark-vault
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Initialize Clarinet**

   ```bash
   clarinet check
   ```

### Development

#### Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage and cost analysis
npm run test:report

# Watch mode for continuous testing
npm run test:watch
```

#### Contract Validation

```bash
# Check contract syntax and logic
clarinet check

# Run interactive REPL
clarinet console
```

## 📋 Core Functions

### Administrative Functions

#### `initialize-pool`

Initializes the staking pool with a base yield rate.

```clarity
(initialize-pool u500) ;; 5% APY
```

#### `distribute-yield`

Distributes accumulated yield to all stakers (owner-only).

```clarity
(distribute-yield)
```

### User Functions

#### `stake`

Stakes Bitcoin and receives stBTC tokens.

```clarity
(stake u1000000) ;; Stake 0.01 BTC minimum
```

#### `unstake`

Burns stBTC tokens and withdraws Bitcoin.

```clarity
(unstake u500000) ;; Unstake 0.005 BTC
```

#### `claim-rewards`

Claims accumulated staking rewards.

```clarity
(claim-rewards)
```

### Query Functions

#### `get-pool-stats`

Returns comprehensive pool statistics.

```clarity
(get-pool-stats)
;; Returns: { total-staked, total-yield, current-rate, pool-active, insurance-active, insurance-balance }
```

#### `get-staker-balance`

Retrieves individual staker balance.

```clarity
(get-staker-balance 'SP1234...)
```

## 🔧 Configuration

### Network Settings

The protocol supports multiple networks through Clarinet configuration:

- **Devnet**: Local development environment
- **Testnet**: Stacks testnet deployment  
- **Mainnet**: Production deployment

### Key Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `minimum-stake-amount` | 1,000,000 sats | 0.01 BTC minimum stake |
| `yield-rate` | 500 (5%) | Base annual yield rate |
| `distribution-interval` | 144 blocks | ~Daily distribution cycle |

## 🛡️ Security Features

### Access Controls

- **Owner-only functions**: Pool initialization, yield distribution
- **Staker-only functions**: Individual balance management
- **Transfer authorization**: Sender validation for token transfers

### Risk Mitigation

- **Minimum stake requirements**: Prevents spam attacks
- **Balance verification**: Comprehensive balance checks
- **Time-based distributions**: Prevents rapid yield manipulation

### Insurance System

- **Optional coverage**: Configurable insurance for staker protection
- **Dynamic fund management**: Automated insurance fund allocation
- **Risk-based coverage**: Coverage amounts tied to risk scores

## 🧪 Testing

The project includes comprehensive test coverage using Vitest and Clarinet SDK:

### Test Categories

- **Unit Tests**: Individual function testing
- **Integration Tests**: End-to-end workflow validation
- **Security Tests**: Access control and edge case validation
- **Performance Tests**: Gas cost optimization verification

### Running Specific Tests

```bash
# Run with coverage
vitest run --coverage

# Run with cost analysis
vitest run --costs

# Run specific test file
vitest run tests/stark-vault.test.ts
```

## 📈 Economics

### Yield Mechanism

- **Base APY**: 5% annual percentage yield
- **Time-based calculation**: Block height progression
- **Compound rewards**: Automatic reinvestment option
- **Transparent distribution**: On-chain audit trail

### Fee Structure

- **No deposit fees**: Zero-cost staking entry
- **No withdrawal fees**: Free unstaking process
- **Gas optimization**: Minimal transaction costs

## 🤝 Contributing

We welcome contributions from the community! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch
3. Write comprehensive tests
4. Ensure all tests pass
5. Submit a pull request

## 📜 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.
