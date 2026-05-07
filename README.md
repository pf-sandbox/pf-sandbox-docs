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

## Quick Links

- [Getting Started](docs/SANDBOX_GETTING_STARTED.md)
- [Mayhem Mode](docs/SANDBOX_MAYHEM_MODE.md)
- [Havoc](docs/SANDBOX_HAVOC.md)

## What's Coming

- [ ] Havoc distributed wallet strategies
- [ ] Advanced account derivation patterns
- [ ] Custom liquidity amplification scenarios
- [ ] Batch operations examples

## Sandbox Environment

Coming soon.

**Resources**:
- [Devnet Faucet](https://faucet.solana.com/)
- [Devnet Explorer](https://explorer.solana.com/?cluster=devnet)
- [IDL Definitions](idl/)
