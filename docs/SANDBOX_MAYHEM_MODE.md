# Mayhem Mode

## Overview

Mayhem Mode is an optional feature enabled via the `is_mayhem_mode` parameter in `create_v2`. It introduces time-limited or reserve-limited gameplay where all held tokens are burned once the mode concludes.

## Key Concepts

- **Mayhem Program ID**: `MAyhSmzXzV1pTf7LsNkrNwkWKTo4ougAJ1PPg47MD4e`
- **Token Burn**: All held tokens are burned when Mayhem Mode ends
- **Mode Expiration**: Mode concludes when either:
  - 24-hour window expires, OR
  - SOL reserves are depleted
- **is_mayhem_mode**: Boolean flag on bonding curve and pool accounts

## How Mayhem Mode Works

In Mayhem Mode, traders have a limited time window to buy and sell tokens before:
1. The mode timer expires (24 hours), or
2. The bonding curve's SOL reserves run out

Once either condition is met, all remaining held tokens are permanently burned. This creates urgency and unique trading dynamics.

## Creating a Mayhem Mode Coin

To create a coin with Mayhem Mode enabled, set `is_mayhem_mode: true` when calling `create_v2`:

```ts
// Set is_mayhem_mode flag to true
const tx = await PUMP_SDK.create({
  mint,
  name: "Mayhem Cat",
  symbol: "MCAT",
  address: "EXXZDh1CzomtLwixWvZ947frkwyMGDygw3CWkeRTpump",
  // ... other parameters
  is_mayhem_mode: true,
});
```

## Important Notes

- **Irreversible**: Token burns are permanent once the mode concludes
- **Reserve Depletion**: If SOL reserves are depleted before 24 hours, the mode ends immediately
- **Testing Environment**: Behavior may change before mainnet deployment
