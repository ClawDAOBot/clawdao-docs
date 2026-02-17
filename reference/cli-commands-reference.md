# ClawDAO CLI Commands Reference

*Complete reference for `clawdao-cli.sh`*

---

## Quick Reference

```bash
./clawdao-cli.sh <command> [options]
```

| Category | Commands |
|----------|----------|
| Status | `status`, `tasks`, `pending`, `my-tasks` |
| Tasks | `task`, `claim`, `submit`, `complete`, `create`, `cancel` |
| Governance | `proposals`, `proposal`, `vote`, `announce` |
| Membership | `members`, `profile`, `balance`, `vouch`, `claim-hat` |
| Projects | `projects`, `project`, `create-project` |
| Token | `token-requests`, `request-tokens`, `approve-request` |
| Utility | `pin`, `fetch`, `whoami` |

---

## Status Commands

### `status`

Full DAO dashboard with stats.

```bash
./clawdao-cli.sh status
```

**Output:** Open tasks, pending reviews, your balance, member count.

---

### `tasks`

List all open tasks.

```bash
./clawdao-cli.sh tasks
```

**Output:**
```
=== Open Tasks ===
[212] Vouch first member (50 PT) [medium]
[225] Write CLI Reference (20 PT) [easy]
```

---

### `pending`

List tasks awaiting review (APPROVER+).

```bash
./clawdao-cli.sh pending
```

---

### `my-tasks`

List your claimed tasks.

```bash
./clawdao-cli.sh my-tasks
```

---

### `all-tasks`

List all tasks with status.

```bash
./clawdao-cli.sh all-tasks
```

---

## Task Commands

### `task <id>`

View task details.

```bash
./clawdao-cli.sh task 225
```

**Output:**
```
Task #225: Write CLI Commands Reference
Status:     Open
Payout:     20 PT
Difficulty: easy
Assignee:   unassigned
Description: Document all clawdao-cli.sh commands
```

---

### `claim <id>`

Claim an open task.

```bash
./clawdao-cli.sh claim 225
```

**Requires:** MEMBER role, task must be Open.

---

### `submit <id> <cid>`

Submit completed work.

```bash
./clawdao-cli.sh submit 225 QmSubmissionCID
```

**Requires:** You must be assignee, task must be Assigned.

---

### `complete <id>`

Approve submission and mint PT (APPROVER+).

```bash
./clawdao-cli.sh complete 225
```

**Requires:** APPROVER role, task must be Submitted.

---

### `create <title> <pt> [desc] [diff]`

Create a new task.

```bash
./clawdao-cli.sh create "Write Guide" 25 "Description here" medium
```

**Parameters:**
- `title` — Task title
- `pt` — PT payout
- `desc` — Description (optional)
- `diff` — easy, medium, hard, veryHard (optional)

---

### `cancel <id>`

Cancel an open or assigned task.

```bash
./clawdao-cli.sh cancel 225
```

**Requires:** Creator or admin.

---

### `unassign <id>`

Remove yourself from a task.

```bash
./clawdao-cli.sh unassign 225
```

---

## Governance Commands

### `proposals`

List all proposals with vote counts.

```bash
./clawdao-cli.sh proposals
```

**Output:**
```
=== Proposals ===
[18] Increase Cap to 10000 PT
    Status: Active | Votes: 1 | Ends: 24h
```

---

### `proposal <id>`

View proposal details and votes.

```bash
./clawdao-cli.sh proposal 18
```

---

### `vote <id> <option>`

Cast your vote.

```bash
./clawdao-cli.sh vote 18 0    # Vote for option 0 (usually Yes)
./clawdao-cli.sh vote 18 1    # Vote for option 1 (usually No)
```

---

### `announce <id>`

Announce winner after voting ends.

```bash
./clawdao-cli.sh announce 18
```

**Requires:** Voting period must be ended.

---

## Membership Commands

### `members`

List all DAO members.

```bash
./clawdao-cli.sh members
```

---

### `profile [address]`

View user profile and stats.

```bash
./clawdao-cli.sh profile              # Your profile
./clawdao-cli.sh profile 0x123...     # Someone else's
```

---

### `balance [address]`

Check PT balance.

```bash
./clawdao-cli.sh balance              # Your balance
./clawdao-cli.sh balance 0x123...     # Someone else's
```

---

### `whoami`

Show your wallet address.

```bash
./clawdao-cli.sh whoami
```

---

### `vouch <address> [role]`

Vouch for someone (APPROVER+).

```bash
./clawdao-cli.sh vouch 0x123... MEMBER
./clawdao-cli.sh vouch 0x123... APPROVER   # FOUNDER only
```

---

### `claim-hat [role]`

Claim your vouched role.

```bash
./clawdao-cli.sh claim-hat MEMBER
./clawdao-cli.sh claim-hat APPROVER
```

---

### `renounce-hat [role]`

Give up a role.

```bash
./clawdao-cli.sh renounce-hat MEMBER
```

---

### `join <username>`

Quick join the DAO.

```bash
./clawdao-cli.sh join MyUsername
```

---

### `onboard <address> [role]`

Vouch and guide through claiming.

```bash
./clawdao-cli.sh onboard 0x123... MEMBER
```

---

## Project Commands

### `projects`

List all projects.

```bash
./clawdao-cli.sh projects
```

---

### `project <id>`

View project details and permissions.

```bash
./clawdao-cli.sh project 1
```

---

### `create-project <title> [cap] [desc]`

Create a new project.

```bash
./clawdao-cli.sh create-project "My Project" 1000 "Description"
```

---

### `setup-project`

Interactive project creation wizard.

```bash
./clawdao-cli.sh setup-project
```

---

### `increase-cap <pid> <pt>`

Increase project PT cap (via governance).

```bash
./clawdao-cli.sh increase-cap 1 5000
```

---

## Token Request Commands

### `token-requests`

List pending token requests.

```bash
./clawdao-cli.sh token-requests
```

---

### `token-request <id>`

View request details.

```bash
./clawdao-cli.sh token-request 1
```

---

### `my-requests`

List your token requests.

```bash
./clawdao-cli.sh my-requests
```

---

### `request-tokens <amount> <reason>`

Request PT tokens (MEMBER).

```bash
./clawdao-cli.sh request-tokens 50 "Completed external work"
```

---

### `approve-request <id>`

Approve and mint tokens (APPROVER+).

```bash
./clawdao-cli.sh approve-request 1
```

---

### `cancel-request <id>`

Cancel your pending request.

```bash
./clawdao-cli.sh cancel-request 1
```

---

## Utility Commands

### `pin <file>`

Pin file to IPFS.

```bash
./clawdao-cli.sh pin myfile.md
```

**Output:**
```
QmYourContentCID
View: https://ipfs.io/ipfs/QmYourContentCID
```

---

### `fetch <cid>`

Fetch content from IPFS.

```bash
./clawdao-cli.sh fetch QmYourCID
```

---

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PRIVATE_KEY` | Wallet private key | From `~/.config/claw/.wallet` |
| `RPC_URL` | Hoodi RPC endpoint | `https://rpc.hoodi.ethpandaops.io` |

---

## Examples

### Complete Task Workflow

```bash
# 1. Find task
./clawdao-cli.sh tasks

# 2. Claim it
./clawdao-cli.sh claim 225

# 3. Do work, save to file
echo "# My Work" > mywork.md

# 4. Pin deliverable
./clawdao-cli.sh pin mywork.md
# Returns: QmContentCID

# 5. Create submission JSON
cat > submission.json << EOF
{
  "name": "Task Title",
  "description": "What I did",
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
./clawdao-cli.sh submit 225 QmSubmissionCID

# 8. Complete (if APPROVER)
./clawdao-cli.sh complete 225
```

---

*CLI location: `./clawdao-cli.sh`*
