# Sandbox Cashback Rewards

## Overview

Cashback Rewards allows token creators to create coins with "cashback" enabled, which redirects the creator fee back to the users. Each user receives the creator fee on their swap volume as cashback rather than paying that fee to the coin creator.

This is a backwards compatible change. If you do not update to the latest IDLs/SDKs it will still work, but cashback will not be enabled.

## SDKs

Use the Typescript SDKs for easier integration:
- [Pump SDK](https://www.npmjs.com/package/@pump-fun/pump-sdk) — version `1.28.0`+
- [PumpSwap SDK](https://www.npmjs.com/package/@pump-fun/pump-swap-sdk) — version `1.14.0`+

## Instruction Changes

Cashback is only given to the user if the buy/sell instruction appends the proper remaining accounts. If the coin is a cashback coin but the remaining accounts are not added, the creator fee falls back to the creator as usual.

### Bonding Curve Buy
No change. Cashback is handled automatically if the coin has cashback enabled.

### Bonding Curve Sell
Pass the `UserVolumeAccumulator` PDA (Pump program) at remaining accounts index 0 with `isWritable: true`.

### PumpSwap Buy
Pass the WSOL ATA of the `UserVolumeAccumulator` (Pump AMM program) at remaining accounts index 0.

### PumpSwap Sell
Pass:
- Index 0: WSOL ATA of the `UserVolumeAccumulator` (Pump AMM program)
- Index 1: The `UserVolumeAccumulator` PDA itself (Pump AMM program)

### Create V2
New `OptionBool` parameter for cashback. In TypeScript: `[true]` to enable, `[false]` to disable.

### Claiming Cashback

**Bonding Curve** — `claim_cashback` on the Pump program. Transfers native lamports from the `UserVolumeAccumulator` to the user.

**PumpSwap** — `claim_cashback` on the Pump AMM program. Transfers WSOL from the `UserVolumeAccumulator` WSOL ATA to the user's WSOL ATA. The user's WSOL ATA must exist beforehand (use `createIdempotentAssociatedTokenAccount` if needed).

## Account Changes

New field on `BondingCurve`: `is_cashback_coin: bool`

## Deriving the UserVolumeAccumulator

There is a separate `UserVolumeAccumulator` for each program (Pump and Pump AMM). They share the seed `"user_volume_accumulator"` — the program ID is the differentiator.

```typescript
import {
  getAddressEncoder,
  getProgramDerivedAddress,
  getUtf8Encoder,
} from "@solana/kit";

const addressEncoder = getAddressEncoder();
const utf8Encoder = getUtf8Encoder();

export const USER_ACCUMULATOR_SEED = utf8Encoder.encode(
  "user_volume_accumulator",
);

export function getUserAccumulatorPda(
  walletAddress: Address,
  programAddress: Address = PUMP_PROGRAM_ADDRESS,
) {
  return getProgramDerivedAddress({
    programAddress,
    seeds: [USER_ACCUMULATOR_SEED, addressEncoder.encode(walletAddress)],
  });
}
```

## Reading Unclaimed Cashback

**Bonding Curve (Pump program):** Read the lamports of the `UserVolumeAccumulator` minus rent-exempt minimum.

**PumpSwap (Pump AMM program):** Read the WSOL token balance of the `UserVolumeAccumulator`'s WSOL ATA.
