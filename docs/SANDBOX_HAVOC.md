# Havoc Bot Guide

## Overview

Havoc is an internal testing tool that simulates trading activity on Pump Mayhem Mode tokens. It's used by developers to validate bonding curve behavior, fee routing, and transaction throughput under load conditions.

**Status**: Sandbox testing only - not for production or user trading

## Key Features

- **Multi-wallet coordination**: Randomized buy/sell cycles across multiple wallets
- **Automated liquidity supplementation**: Intelligent token distribution during critical phases
- **Low-latency transaction routing**: Integration with Jito, Nozomi, 0slot, BlockRazor, and bloXroute
- **Configurable parameters**: Timing, position sizing, and wallet randomization
- **Parallel submission**: Send transactions to multiple providers simultaneously for faster inclusion

## Prerequisites

- Node.js 18+
- TypeScript 4.9+
- Solana wallet(s) with devnet SOL
- Access to at least one transaction landing provider

## Installation

Coming soon - includes:
- Repository setup
- Dependency installation
- Configuration file creation
- Wallet setup

## Configuration

### Mayhem Config

Havoc pulls dynamic configuration from the Mayhem program:

```typescript
const { solAmt, sellPercentage } = await getMayhemConfig();
```

**Key Parameters**:
- `solAmt`: Amount of SOL per transaction
- `sellPercentage`: Percentage of tokens to sell per cycle
- Additional parameters as defined by Mayhem program state

### Transaction Landing Providers

Havoc supports multiple providers for parallel submission:

- **Jito**: Validator-optimized landing
- **Nozomi**: MEV protection routing
- **0slot**: Slot-based optimization
- **BlockRazor**: Fast block inclusion
- **bloXroute**: Liquidity aggregation

## Basic Usage

### Simple Buy/Sell Cycle

```typescript
const mint = '2az8Wzi99L8Ee5TGXoyPXRnRoKToqq6dHN8DgVZEpump';

const sdk = new PumpSwapSDK();
await sdk.buy(new PublicKey(mint), wallet_1.publicKey, solAmt);
await sdk.sell_percentage(new PublicKey(mint), wallet_1.publicKey, sellPercentage);
```

### Transaction Submission Best Practices

1. **Warm up connections**: Send health pings to providers before burst submissions
2. **Use fresh blockhashes**: Avoid reusing expired blockhashes
3. **Parallel submission**: Send time-sensitive trades to multiple providers
4. **Monitor responses**: Track provider latency and adjust routing in real time

## Advanced Features

### Distributed Wallet Management

Coming soon - coordinating multiple wallets:
- Wallet derivation and funding
- Random wallet selection
- Position tracking across wallets

### Dynamic Configuration Updates

Coming soon - pulling updates from:
- Mayhem program global state
- Per-token mayhem state
- Real-time market conditions

### Custom Strategies

Coming soon - examples:
- Linear liquidity supplementation
- Exponential accumulation
- Market-aware positioning

## Limitations

- Works best with `is_mayhem_mode = true` tokens
- Requires adequate SOL for transaction fees
- Depends on transaction landing provider availability
- Not optimized for mainnet use

## Developer Use Cases

### Testing Bonding Curve Dynamics

Use Havoc during development to:
- Verify price curve calculations under load
- Test slippage calculations match expected behavior
- Validate fee routing to correct recipients
- Stress test transaction throughput limits
- Confirm account size requirements are met

### Volume Simulation

Simulate trading volume in sandbox to:
- Test how bonding curves respond to various trading patterns
- Verify state updates occur correctly
- Validate Mayhem mode fee recipient configuration
- Monitor transaction submission across different providers

## Monitoring and Debugging

Coming soon - includes:
- Transaction log analysis
- Wallet balance tracking
- Provider performance metrics
- Error handling and retries

## Resources

- [Havoc Repository](https://github.com/pf-sandbox/havoc)
- [Mayhem Mode Testing](SANDBOX_MAYHEM_MODE.md)
- [Token Creation](SANDBOX_TOKEN_CREATION.md)
- [Getting Started](SANDBOX_GETTING_STARTED.md)

## Support

For issues or questions:
1. Check transaction logs with `solana logs`
2. Verify wallet balances
3. Confirm transaction provider connectivity
4. Review configuration parameters
