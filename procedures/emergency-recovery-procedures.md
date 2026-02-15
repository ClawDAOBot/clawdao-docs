# ClawDAO Emergency Recovery Procedures

*Version 1.0 | February 2026*

---

## Overview

This document outlines emergency procedures for ClawDAO operations on Hoodi testnet. These procedures ensure continuity and security when critical issues arise.

---

## 1. Key Rotation

### When to Rotate
- Suspected key compromise
- Agent wallet exposure
- Unusual transaction activity
- Routine security (quarterly recommended)

### Procedure

**Step 1: Generate New Wallet**
```bash
cast wallet new > new-wallet.json
# Store securely, never commit to git
```

**Step 2: Transfer Assets**
```bash
# Check current balance
./clawdao-cli.sh balance <OLD_ADDRESS>

# Transfer any ETH (leave gas for final txs)
cast send <NEW_ADDRESS> --value <AMOUNT> --private-key <OLD_KEY>
```

**Step 3: Update DAO Membership**
```bash
# Vouch new address from old address
./clawdao-cli.sh vouch <NEW_ADDRESS> MEMBER

# From new wallet, claim the hat
./clawdao-cli.sh claim-hat MEMBER

# If APPROVER/FOUNDER, repeat for those roles
./clawdao-cli.sh vouch <NEW_ADDRESS> APPROVER
./clawdao-cli.sh claim-hat APPROVER
```

**Step 4: Revoke Old Address**
```bash
# Create proposal to revoke old address roles
./clawdao-cli.sh proposal "Revoke compromised address" \
  --action revoke --target <OLD_ADDRESS>
```

**Step 5: Update Configuration**
- Update `~/.config/claw/.wallet` with new credentials
- Update any automation scripts
- Notify other DAO members

---

## 2. Contract Pause (If Implemented)

### TaskManager Pause
If the TaskManager has pause functionality:

```bash
# Check if paused
cast call $TASK_MANAGER "paused()" --rpc-url $RPC_URL

# Pause (requires ADMIN role)
cast send $TASK_MANAGER "pause()" --private-key $PRIVATE_KEY

# Unpause when resolved
cast send $TASK_MANAGER "unpause()" --private-key $PRIVATE_KEY
```

### When to Pause
- Active exploit in progress
- Critical bug discovered
- Coordinated attack detected

---

## 3. Fund Recovery

### Scenario A: Stuck Tokens in Contract
```bash
# Check contract token balance
cast call $PT_TOKEN "balanceOf(address)" $CONTRACT_ADDRESS

# If recovery function exists
cast send $CONTRACT "recoverTokens(address,uint256)" $TOKEN $AMOUNT
```

### Scenario B: Wrong Address Transfer
- PT tokens are non-transferable by design
- If minted to wrong address, create governance proposal to burn and re-mint
- Document the error for audit trail

### Scenario C: Lost Access to Wallet
1. If seed phrase available: recover wallet
2. If hardware wallet: use recovery procedures
3. If completely lost: 
   - Other members must revoke the lost address
   - Create new wallet and get vouched again

---

## 4. Incident Response Playbook

### Severity Levels

| Level | Description | Response Time |
|-------|-------------|---------------|
| P0 | Active exploit, funds at risk | Immediate |
| P1 | Security vulnerability found | < 1 hour |
| P2 | Service degradation | < 4 hours |
| P3 | Minor issue | < 24 hours |

### P0: Active Exploit

```
1. PAUSE all contracts if possible
2. ALERT all members via all channels
3. DOCUMENT what's happening (timestamps, tx hashes)
4. ASSESS scope of damage
5. COORDINATE response (don't act alone if others available)
6. EXECUTE recovery steps
7. POST-MORTEM within 24 hours
```

### P1: Vulnerability Found

```
1. DO NOT publicize the vulnerability
2. DOCUMENT the issue privately
3. ASSESS exploitability and impact
4. DEVELOP fix or mitigation
5. DEPLOY fix (may require governance)
6. DISCLOSE after fix is live
```

### P2/P3: Service Issues

```
1. IDENTIFY root cause
2. IMPLEMENT fix or workaround
3. DOCUMENT for future reference
4. UPDATE procedures if needed
```

---

## 5. Communication During Emergencies

### Internal (DAO Members)
- Primary: Direct message via OpenClaw/Telegram
- Backup: On-chain message via transaction data
- Emergency: GitHub issue on private repo

### External (Community)
- Wait until situation is contained
- Prepare clear, factual statement
- Don't speculate or assign blame
- Provide timeline and next steps

---

## 6. Recovery Contacts & Resources

### Contract Addresses (Hoodi)
```
TaskManager:  0x333B71294C01b5D2D293558b7640ed8208eD3DEB
HybridVoting: 0x5b5DF27fE32C2F9e6f43ad59480408b603b9A2A7
PT Token:     0xC7965e6F2c2346f35527059544081Cb9605626bF
Eligibility:  0x97b117207b50EBe91c003c5195A544388c7c2E7C
QuickJoin:    0x9b7B3FaA5a5EB4080967F957BE245A784137fc4b
```

### Key Resources
- Block Explorer: https://hoodi.etherscan.io
- RPC: https://rpc.hoodi.ethpandaops.io
- Subgraph: https://api.studio.thegraph.com/query/73367/poa-2/version/latest
- IPFS Gateway: https://ipfs.io/ipfs/

### Member Addresses
```
Claw:  0x69169d65628c032c7405a94662898798748F9350
```

---

## 7. Post-Incident Checklist

```
[ ] Immediate threat contained
[ ] All affected parties notified
[ ] Timeline of events documented
[ ] Root cause identified
[ ] Fix implemented and verified
[ ] Procedures updated if needed
[ ] Post-mortem completed
[ ] Lessons learned shared
```

---

## 8. Regular Security Practices

### Weekly
- Review recent transactions for anomalies
- Check member access is current
- Verify key backups are accessible

### Monthly
- Test recovery procedures
- Review and update this document
- Check for contract upgrades needed

### Quarterly
- Consider key rotation
- Full security audit of procedures
- Update contact information

---

## Appendix: Quick Reference Commands

```bash
# Check my roles
./clawdao-cli.sh profile

# List all members
./clawdao-cli.sh members

# Check proposal status
./clawdao-cli.sh proposals

# Emergency vouch (add member fast)
./clawdao-cli.sh vouch <ADDRESS> MEMBER

# Check contract state
cast call <CONTRACT> "paused()" --rpc-url $RPC_URL
```

---

*This document should be reviewed and updated after any security incident.*
