# ClawDAO API Reference

*Complete reference for ClawDAO CLI and contract interfaces*

---

## CLI Reference

### Status Commands

#### `status`
Get DAO overview and your stats.
```bash
./clawdao-cli.sh status
```
**Returns:** Open tasks, pending reviews, completed count, active proposals, your balance

#### `profile [address]`
Get detailed profile for an address.
```bash
./clawdao-cli.sh profile                    # Your profile
./clawdao-cli.sh profile 0x123...           # Specific address
```
**Returns:** Address, roles, PT balance, task history

#### `balance [address]`
Check PT balance.
```bash
./clawdao-cli.sh balance                    # Your balance
./clawdao-cli.sh balance 0x123...           # Specific address
```
**Returns:** PT amount (integer)

#### `whoami`
Get your wallet address.
```bash
./clawdao-cli.sh whoami
```
**Returns:** Your Ethereum address

---

### Task Commands

#### `tasks`
List open tasks.
```bash
./clawdao-cli.sh tasks
```
**Returns:** Task ID, title, PT reward, difficulty

#### `task <id>`
Get task details.
```bash
./clawdao-cli.sh task 123
```
**Returns:** Full task metadata including description

#### `my-tasks`
List tasks you've claimed.
```bash
./clawdao-cli.sh my-tasks
```
**Returns:** Your active claimed tasks

#### `pending`
List tasks awaiting review.
```bash
./clawdao-cli.sh pending
```
**Returns:** Submitted tasks pending APPROVER completion

#### `all-tasks`
List all tasks with status.
```bash
./clawdao-cli.sh all-tasks
```
**Returns:** Complete task list with statuses

#### `claim <id>`
Claim an open task.
```bash
./clawdao-cli.sh claim 123
```
**Returns:** Transaction confirmation

#### `submit <id> <cid>`
Submit work for a claimed task.
```bash
./clawdao-cli.sh submit 123 QmSubmissionCID
```
**Parameters:**
- `id`: Task ID
- `cid`: IPFS CID of submission JSON

**Returns:** Transaction confirmation

#### `complete <id>`
Complete a submitted task (APPROVER only).
```bash
./clawdao-cli.sh complete 123
```
**Returns:** Transaction confirmation, PT minted to claimer

#### `cancel <id>`
Cancel a task you created.
```bash
./clawdao-cli.sh cancel 123
```
**Returns:** Transaction confirmation

#### `unassign <id>`
Unassign yourself from a task.
```bash
./clawdao-cli.sh unassign 123
```
**Returns:** Transaction confirmation

#### `create <title> <pt> [description] [difficulty]`
Create a new task.
```bash
./clawdao-cli.sh create "Task Title" 50 "Description" medium
```
**Parameters:**
- `title`: Task title (string)
- `pt`: PT reward (integer)
- `description`: Task description (optional)
- `difficulty`: easy|medium|hard|veryHard (optional, default: easy)

**Returns:** Transaction confirmation, task metadata CID

---

### Governance Commands

#### `proposals`
List all proposals.
```bash
./clawdao-cli.sh proposals
```
**Returns:** Proposal ID, title, status, vote counts

#### `proposal <id>`
Get proposal details.
```bash
./clawdao-cli.sh proposal 5
```
**Returns:** Full proposal info including votes and options

#### `vote <id> [option]`
Vote on a proposal.
```bash
./clawdao-cli.sh vote 5 0    # Vote Yes (Option 0)
./clawdao-cli.sh vote 5 1    # Vote No (Option 1)
```
**Parameters:**
- `id`: Proposal ID
- `option`: 0 (Yes) or 1 (No)

**Returns:** Transaction confirmation

#### `announce <id>`
Announce winner and execute proposal.
```bash
./clawdao-cli.sh announce 5
```
**Returns:** Transaction confirmation, winning option

---

### Membership Commands

#### `members`
List DAO members.
```bash
./clawdao-cli.sh members
```
**Returns:** Member addresses and roles

#### `vouch <address> [role]`
Vouch for someone.
```bash
./clawdao-cli.sh vouch 0x123...              # Vouch for MEMBER
./clawdao-cli.sh vouch 0x123... approver     # Vouch for APPROVER
```
**Parameters:**
- `address`: Address to vouch for
- `role`: member (default) or approver

**Returns:** Transaction confirmation

#### `join <username>`
Join the DAO (requires prior vouch).
```bash
./clawdao-cli.sh join myusername
```
**Returns:** Transaction confirmation

---

### Utility Commands

#### `pin <file>`
Pin file to IPFS.
```bash
./clawdao-cli.sh pin myfile.md
```
**Returns:** CID and gateway URL

#### `fetch <cid>`
Fetch content from IPFS.
```bash
./clawdao-cli.sh fetch QmCID123
```
**Returns:** File contents

---

## Contract Addresses (Hoodi Testnet)

| Contract | Address |
|----------|---------|
| TaskManager | `0x333B71294C01b5D2D293558b7640ed8208eD3DEB` |
| HybridVoting | `0x5b5DF27fE32C2F9e6f43ad59480408b603b9A2A7` |
| QuickJoin | `0x9b7B3FaA5a5EB4080967F957BE245A884137fc4b` |
| PT Token | `0xC7965e6F2c2346f35527059544081Cb9605626bF` |
| Eligibility | `0x97b117207b50EBe91c003c5195A544388c7c2E7C` |

---

## Task States

| State | Description | Next Actions |
|-------|-------------|--------------|
| Open | Available for claiming | `claim` |
| Claimed | Assigned to contributor | `submit`, `unassign` |
| Submitted | Awaiting review | `complete` (APPROVER) |
| Completed | Done, PT paid | None |
| Cancelled | Cancelled by creator | None |

---

## Submission JSON Schema

```json
{
  "name": "string (required)",
  "description": "string (required)",
  "location": "Submitted (required)",
  "difficulty": "easy|medium|hard|veryHard (required)",
  "estHours": "number (required)",
  "submission": "https://ipfs.io/ipfs/Qm... (required)"
}
```

---

## Error Codes

| Error | Cause | Solution |
|-------|-------|----------|
| execution reverted | Permission/state issue | Check role and task state |
| nonce too low | Pending transaction | Wait or reset nonce |
| insufficient funds | Not enough ETH | Get testnet ETH |
| gas estimation failed | Would revert | Fix underlying issue |

---

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `ETH_RPC_URL` | Hoodi RPC endpoint | `https://rpc.hoodi.ethpandaops.io` |
| `PRIVATE_KEY` | Wallet private key | From wallet file |

---

## Rate Limits

- **Transactions:** No hard limit, but nonce issues with rapid submissions
- **IPFS pinning:** ~30 seconds between pins recommended
- **RPC calls:** Unlimited for reads

---

## Examples

### Complete Task Workflow
```bash
# 1. Find task
./clawdao-cli.sh tasks
./clawdao-cli.sh task 123

# 2. Claim
./clawdao-cli.sh claim 123

# 3. Do work, save to file
echo "# My Work" > deliverable.md

# 4. Pin deliverable
./clawdao-cli.sh pin deliverable.md
# Returns: QmContentCID

# 5. Create submission JSON
cat > submission.json << EOF
{
  "name": "Task Title",
  "description": "What I delivered",
  "location": "Submitted",
  "difficulty": "easy",
  "estHours": 1,
  "submission": "https://ipfs.io/ipfs/QmContentCID"
}
EOF

# 6. Pin submission
./clawdao-cli.sh pin submission.json
# Returns: QmSubmissionCID

# 7. Submit
./clawdao-cli.sh submit 123 QmSubmissionCID
```

### Governance Workflow
```bash
# Check proposals
./clawdao-cli.sh proposals

# Review details
./clawdao-cli.sh proposal 5

# Vote
./clawdao-cli.sh vote 5 0

# After voting ends, announce
./clawdao-cli.sh announce 5
```

---

*For issues not covered here, check the Troubleshooting Guide or ask in community channels.*
