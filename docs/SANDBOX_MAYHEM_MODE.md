# Mayhem Mode Testing

## Overview

Mayhem Mode is an optional feature enabled via the `is_mayhem_mode` parameter in `create_v2`. It introduces dynamic fee routing through the Mayhem program.

## Key Concepts

- **Mayhem Program ID**: `MAyhSmzXzV1pTf7LsNkrNwkWKTo4ougAJ1PPg47MD4e`
- **Dynamic Fee Recipient**: Fee routing managed by Mayhem program
- **is_mayhem_mode**: Boolean flag on bonding curve and pool accounts

## Enabling Mayhem Mode

When creating a token with `create_v2`:

```typescript
const instruction = {
  is_mayhem_mode: true,
  name: "Mayhem Token",
  symbol: "MAYHEM",
  uri: "https://example.com/metadata.json",
};
```

## Fee Recipient Configuration

### For Mayhem Mode Tokens (`is_mayhem_mode = true`)

**Bonding Curve Program**:
- Account Index 2: Must be Mayhem fee recipient

**Pump Swap Program**:
- Account Index 10: Must be Mayhem fee recipient
- Account Index 11: WSOL token account of Mayhem fee recipient

### For Non-Mayhem Tokens (`is_mayhem_mode = false`)

Use the standard fee recipient configuration as before.

## Sandbox Mayhem Accounts

### Available Fee Recipients (use any):

- `GesfTA3X2arioaHp8bbKdjG9vJtskViWACZoYvxp4twS`
- `4budycTjhs9fD6xw62VBducVTNgMgJJ5BgtKq7mAZwn6`
- `8SBKzEQU4nLSzcwF4a74F2iaUDQyTfjGndn6qUWBnrpR`
- `4UQeTP1T39KZ9Sfxzo3WR5skgsaP6NZa87BAkuazLEKH`
- `8sNeir4QsLsJdYpc9RZacohhK1Y5FLU3nC5LXgYB4aa6`
- `Fh9HmeLNUMVCvejxCtCL2DbYaRyBFVJ5xrWkLnMH6fdk`
- `463MEnMeGyJekNZFQSTUABBEbLnvMTALbT6ZmsxAbAdq`
- `6AUH3WEHucYZyC61hqpqYUWVto5qA5hjHuNQ32GNnNxA`

## Testing Steps

1. Create a token with `is_mayhem_mode: true`
2. Verify the bonding curve and pool have `is_mayhem_mode = true`
3. Execute buy/sell transactions with Mayhem fee recipient
4. Confirm fees are routed correctly
5. Monitor fee recipient token accounts

## Retrieving Fee Recipients from Chain

The Mayhem fee recipient can be retrieved from:

- **Bonding Curve**: Check `global.reserved_fee_recipient` or `reserved_fee_recipients`
- **Pump Swap**: Check `GlobalConfig.reserved_fee_recipient` or `reserved_fee_recipients`

## Limitations in Sandbox

This is a testing environment. Mayhem mode behavior may change before mainnet deployment.
