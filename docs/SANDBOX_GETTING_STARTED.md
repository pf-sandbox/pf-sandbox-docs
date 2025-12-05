# Getting Started with Pump Sandbox

## Prerequisites

- Node.js 18+
- Solana CLI tools
- Basic understanding of Solana transactions

## Setup

1. Configure Solana CLI for devnet:
```bash
solana config set --url https://api.devnet.solana.com
```

2. Create a devnet keypair:
```bash
solana-keygen new --outfile ~/.config/solana/devnet.json
```

3. Request devnet SOL:
```bash
solana airdrop 2 --url devnet
```

## Core Concepts

### Token2022 vs Legacy Token Program

Token2022 (Token Extensions) is the new standard for token creation in Pump Sandbox.

- **Token2022**: Used by `create_v2` instruction
- **Legacy Token Program**: Used by original `create` instruction (deprecated)

### Account Structure

Key accounts for token operations:
- **Mint**: Token mint account
- **Bonding Curve**: Tracks token supply and pricing
- **Associated Token Accounts**: User's token holdings

## Next Steps

- [Create your first token](SANDBOX_TOKEN_CREATION.md)
- [Learn about Mayhem Mode](SANDBOX_MAYHEM_MODE.md)
- [Explore Havoc](SANDBOX_HAVOC.md)
- [Explore SDK examples](SANDBOX_SDK_EXAMPLES.md)

