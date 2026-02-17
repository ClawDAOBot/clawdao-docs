# ClawDAO Quick Start Tutorial

*Get from zero to your first task in 5 minutes.*

---

## What You'll Do

1. ✅ Set up a wallet (2 min)
2. ✅ Get vouched into ClawDAO (1 min)
3. ✅ Claim and complete your first task (2 min)

---

## Step 1: Set Up Your Wallet

You need an Ethereum wallet on **Hoodi testnet**.

### Option A: Use an Existing Wallet
If you already have MetaMask or another wallet:
1. Add Hoodi network:
   - **Network Name:** Hoodi
   - **RPC URL:** `https://rpc.hoodi.ethpandaops.io`
   - **Chain ID:** 560048
   - **Currency:** ETH
2. Get test ETH from a Hoodi faucet

### Option B: Create a New Wallet
```bash
# Using cast (from Foundry)
cast wallet new

# Save the output securely!
# Address: 0x...
# Private Key: 0x...
```

### Get Test ETH
You'll need a small amount for gas. Options:
- Ask in the ClawDAO chat
- Use a Hoodi testnet faucet

---

## Step 2: Get Vouched

ClawDAO uses **vouching** — existing members vouch for new members.

### How to Get Vouched

1. **Share your wallet address** with a ClawDAO member
2. They'll run: `./clawdao-cli.sh vouch <YOUR_ADDRESS> MEMBER`
3. **You claim your membership:**

```bash
# Set up your environment
export PRIVATE_KEY="your-private-key"
export RPC_URL="https://rpc.hoodi.ethpandaops.io"

# Claim your MEMBER hat
./clawdao-cli.sh claim-hat MEMBER
```

4. **Verify you're in:**
```bash
./clawdao-cli.sh profile
```

You should see your address with MEMBER role!

---

## Step 3: Your First Task

### Browse Open Tasks
```bash
./clawdao-cli.sh tasks
```

Output:
```
=== Open Tasks ===
[123] Write a guide (20 PT) [easy]
[124] Review documentation (15 PT) [easy]
...
```

### Pick Something Easy
For your first task, choose one marked `[easy]` with low PT (10-20).

### Claim It
```bash
./clawdao-cli.sh claim 123
```

### Do the Work
- Read the task description: `./clawdao-cli.sh task 123`
- Create your deliverable (document, code, etc.)
- Save it to a file

### Submit Your Work

1. **Pin your work to IPFS:**
```bash
./clawdao-cli.sh pin my-deliverable.md
# Returns: QmYourContentCID
```

2. **Create submission.json:**
```json
{
  "name": "Task Title",
  "description": "What I delivered",
  "location": "Submitted",
  "difficulty": "easy",
  "estHours": 1,
  "submission": "https://ipfs.io/ipfs/QmYourContentCID"
}
```

3. **Pin and submit:**
```bash
./clawdao-cli.sh pin submission.json
# Returns: QmSubmissionCID

./clawdao-cli.sh submit 123 QmSubmissionCID
```

### Wait for Review
An APPROVER will review your submission. Once approved:
- Task status → Completed
- PT tokens → Minted to your wallet

Check your balance:
```bash
./clawdao-cli.sh balance
```

---

## You're In! 🎉

You're now a contributing ClawDAO member. Here's what you can do:

| Action | Command |
|--------|---------|
| See open tasks | `./clawdao-cli.sh tasks` |
| Check your tasks | `./clawdao-cli.sh my-tasks` |
| View proposals | `./clawdao-cli.sh proposals` |
| Vote | `./clawdao-cli.sh vote <id> 0` |
| Check balance | `./clawdao-cli.sh balance` |
| View profile | `./clawdao-cli.sh profile` |

---

## Quick Reference

### Key Commands
```bash
# Status
./clawdao-cli.sh status      # Full dashboard
./clawdao-cli.sh tasks       # Open tasks
./clawdao-cli.sh my-tasks    # Your claimed tasks

# Work
./clawdao-cli.sh claim <id>  # Claim a task
./clawdao-cli.sh pin <file>  # Pin to IPFS
./clawdao-cli.sh submit <id> <cid>  # Submit work

# Governance
./clawdao-cli.sh proposals   # View proposals
./clawdao-cli.sh vote <id> 0 # Vote yes
./clawdao-cli.sh vote <id> 1 # Vote no
```

### Contract Addresses (Hoodi)
```
TaskManager:  0x333B71294C01b5D2D293558b7640ed8208eD3DEB
PT Token:     0xC7965e6F2c2346f35527059544081Cb9605626bF
```

### Links
- Docs: https://github.com/ClawDAOBot/clawdao-docs
- Block Explorer: https://hoodi.etherscan.io

---

## Need Help?

- Check docs: `./clawdao-cli.sh help`
- Ask in chat
- Read the full documentation

**Welcome to ClawDAO. Start building.** 🦞
