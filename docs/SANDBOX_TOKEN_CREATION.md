# Token Creation with create_v2

## Overview

The `create_v2` instruction creates tokens using the Token2022 program, enabling advanced features and metadata management.

## Key Differences from Legacy `create`

| Feature | create (Legacy) | create_v2 |
|---------|-----------------|-----------|
| Token Program | Token Program (Legacy) | Token2022 |
| Metadata | Metaplex | Token2022 Extensions |
| Mayhem Mode Support | Not supported | Supported |
| Account Size | 81 bytes | 82+ bytes |

## Basic Workflow

1. **Derive Program-Derived Accounts (PDAs)**
   - Mint
   - Bonding Curve
   - Associated Token Accounts

2. **Call create_v2 Instruction**
   - Set `is_mayhem_mode` parameter
   - Provide fee recipient

3. **Initialize Associated Token Accounts**
   - For the bonding curve
   - For the user

## Account Requirements

The `create_v2` instruction requires the following accounts:

| Index | Account | Description |
|-------|---------|-------------|
| 1 | Mint | Token mint account |
| 2 | Mint Authority | Mint authority PDA |
| 3 | Bonding Curve | Bonding curve state account |
| 4 | Associated Bonding Curve | Token2022 token account |
| 5 | Global | Global program state |
| 6 | User | Transaction signer |
| 7 | System Program | System program |
| 8 | Token Program | Token2022 program |
| 9 | Associated Token Program | ATA program |
| 10 | Mayhem Program | Mayhem program |
| 11 | Global Params | Mayhem global params |
| 12 | Sol Vault | Mayhem sol vault |
| 13 | Mayhem State | Mayhem state for this mint |
| 14 | Mayhem Token Vault | Mayhem token vault |

## Instruction Parameters

```
create_v2 {
  is_mayhem_mode: bool,
  name: String,
  symbol: String,
  uri: String,
  // ... additional metadata
}
```

## Testing in Sandbox

1. Use devnet for all testing
2. Verify account sizes match requirements
3. Confirm fee recipients are properly configured
4. Test both `is_mayhem_mode: true` and `is_mayhem_mode: false`

## Common Pitfalls

- Using wrong token program (Token vs Token2022)
- Incorrect ATA derivation for Token2022
- Missing Mayhem program accounts
- Insufficient account rent

See [Troubleshooting](SANDBOX_TROUBLESHOOTING.md) for solutions.

## Code Examples

Coming soon.
