# Pump Sandbox Documentation

Welcome to PF Sandbox documentation. (in development)

## New Bonding Curve Trade Instructions

As part of supporting stable paired meme coins, we are announcing three new trading instructions for the bonding curve program:

- `buy_v2`
- `sell_v2`
- `buy_exact_quote_in_v2`

These new instructions have no optional accounts. All accounts are mandatory and are passed in the same order for all kinds of coins. This should alleviate many of the issues integrations are facing when choosing which accounts to pass based on the type of coin being traded.

We are moving to this new unified interface and would urge all integrations to switch to these instructions to future proof their setup.

### Existing Trade Instructions

All existing trade instructions will continue to work with the same setup. No changes are needed to continue trading coins with the existing coins.

You can switch to the new instructions to trade coins paired with both SOL and USDC, with no change to quotes or costs.

The first feature we are looking to support with the new interface is the addition of USDC as a quote asset for meme coins.

## Agent Trading Modes

The Mayhem Mode agent can operate in two modes:

### Auto Mode
- **Self-exciting trade cadence** — the more you trade, the more activity from the agent
- Agent buys and sells at random with different trade sizes
- Agent trades for 24 hours as long as there's enough liquidity

### Manual Mode
- **Creator in control** — agent only trades when prompted by the coin creator
- Same trade direction and sizes as Auto: random
- Have the agent trade once, or not at all

### Agent Lifecycle

- **Active**: Agent online and trading in auto or manual mode
- **Paused**: Liquidity or marketcap too low. Top up or start fresh with a new coin
- **Complete**: Agent will no longer trade on this coin. Relaunch to go again

## Quick Links

- [Getting Started](docs/SANDBOX_GETTING_STARTED.md)
- [Mayhem Mode](docs/SANDBOX_MAYHEM_MODE.md)

## What's Coming

- [ ] Advanced account derivation patterns
- [ ] Custom liquidity amplification scenarios
- [ ] Batch operations examples

## Sandbox Environment

Coming soon.

**Resources**:
- [Devnet Faucet](https://faucet.solana.com/)
- [Devnet Explorer](https://explorer.solana.com/?cluster=devnet)
- [IDL Definitions](idl/)
