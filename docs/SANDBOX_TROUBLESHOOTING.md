# Troubleshooting Guide

Coming soon.

## Common Issues and Solutions

### Account Size Validation

**Problem**: "Account insufficient funds for rent"

**Solution**:
- Bonding curve must be at least 82 bytes (was 81)
- Pool account must be at least 244 bytes (was 243)
- Ensure rent-exemption minimum is met

### Token Program Mismatches

**Problem**: "Invalid associated token account"

**Solution**:
- For `create_v2` tokens: Use Token2022 program
- For legacy `create` tokens: Use Token program
- Verify ATA derivation matches token program

### Fee Recipient Issues

**Problem**: "Invalid fee recipient account"

**Solution**:
- Verify fee recipient account exists and is initialized
- For Mayhem tokens: Use Mayhem fee recipient
- For non-Mayhem: Use standard fee recipient
- Check WSOL token account for Pump Swap (index 11)

### Mayhem Program Integration

**Problem**: "Mayhem account not found"

**Symptoms**:
- Missing or invalid Mayhem program state
- Mayhem token vault not initialized
- Invalid global params

**Solution**:
- Verify Mayhem program ID: `MAyhSmzXzV1pTf7LsNkrNwkWKTo4ougAJ1PPg47MD4e`
- Confirm all required Mayhem accounts are provided
- Check account derivation seeds

### Transaction Failures

**Problem**: "Instruction failed with custom error code"

**Diagnosis Steps**:
1. Check transaction logs: `solana logs <TX_SIGNATURE>`
2. Verify all account addresses
3. Confirm instruction parameters
4. Check account ownership (Token2022 vs Token)

### Devnet Faucet Issues

**Problem**: Can't get devnet SOL

**Solution**:
- Use airdrop tool: `solana airdrop 2`
- Rate limits: Wait before requesting again
- Manual faucet: https://faucet.solana.com/

## Getting Help

1. Check this troubleshooting guide
2. Review [Getting Started](SANDBOX_GETTING_STARTED.md)
3. Inspect transaction logs on devnet explorer
4. Check IDL definitions in [idl/](../idl/)

## Additional Resources

- [Solana Devnet Explorer](https://explorer.solana.com/?cluster=devnet)
- [Solana Docs](https://docs.solana.com/)
- [Token Extensions Documentation](https://solana.com/developers/token-extensions)
