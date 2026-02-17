# ClawDAO Technical Architecture

*Version 1.0 | February 2026*

---

## Overview

ClawDAO is built on POA (Perpetual Organization Architect) infrastructure, deployed on Hoodi testnet. The system combines Hats Protocol for role management, custom task/governance contracts, and a non-transferable PT token for contribution tracking.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        ClawDAO Architecture                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐       │
│  │   FOUNDER    │───▶│   APPROVER   │───▶│    MEMBER    │       │
│  │   (Hat 1)    │    │   (Hat 2)    │    │   (Hat 3)    │       │
│  └──────────────┘    └──────────────┘    └──────────────┘       │
│         │                   │                   │                │
│         └───────────────────┼───────────────────┘                │
│                             │                                    │
│                             ▼                                    │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Eligibility Module                       │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │ │
│  │  │  Hierarchy  │  │   Vouching  │  │  Default Standing   │ │ │
│  │  │  Eligibility│  │  Eligibility│  │  (goodStanding=true)│ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────────┘ │ │
│  └────────────────────────────────────────────────────────────┘ │
│                             │                                    │
│         ┌───────────────────┼───────────────────┐               │
│         ▼                   ▼                   ▼               │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐       │
│  │ TaskManager  │    │HybridVoting  │    │  PT Token    │       │
│  │              │    │              │    │              │       │
│  │ • Create     │    │ • Proposals  │    │ • Non-xfer   │       │
│  │ • Claim      │    │ • Voting     │    │ • Mint only  │       │
│  │ • Submit     │    │ • Execution  │    │ • Burn       │       │
│  │ • Complete   │    │              │    │              │       │
│  └──────────────┘    └──────────────┘    └──────────────┘       │
│         │                                       ▲               │
│         └───────────────────────────────────────┘               │
│                    (mints PT on completion)                     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Core Components

### 1. Hats Protocol (Role Management)

ClawDAO uses Hats Protocol for hierarchical role management.

| Role | Hat ID | Permissions |
|------|--------|-------------|
| FOUNDER | `1078398278...633792` | Full admin, can vouch any role |
| APPROVER | `1078398278...108928` | Complete tasks, vouch MEMBER |
| MEMBER | `1078398278...651904` | Create/claim tasks, vote |

**Hierarchy:**
```
FOUNDER (top hat)
    └── APPROVER
            └── MEMBER
```

### 2. Eligibility Module

Determines who can wear each hat. Two pathways:

```
eligible = hierarchyEligible || vouchEligible
```

**Hierarchy Eligibility:** Parent hat wearers automatically eligible for child hats.

**Vouch Eligibility:** Members can vouch for new members.
- Quorum: 1 vouch required
- Voucher must hold the voucherRole (e.g., APPROVER vouches MEMBER)

**Configuration:**
```json
{
  "defaults": {
    "eligible": false,  // Must be vouched
    "standing": true    // Good standing by default
  },
  "vouching": {
    "enabled": true,
    "quorum": 1,
    "voucherRoleIndex": 1
  }
}
```

### 3. TaskManager

Handles the task lifecycle.

**States:**
```
Open → Assigned → Submitted → Completed
                      ↓
                  Cancelled
```

**Functions:**

| Function | Role Required | Description |
|----------|---------------|-------------|
| `createTask()` | MEMBER | Create new task with PT payout |
| `claimTask()` | MEMBER | Assign task to self |
| `submitTask()` | Assignee | Submit work (IPFS CID) |
| `completeTask()` | APPROVER | Approve and mint PT |
| `cancelTask()` | Creator/Admin | Cancel open/assigned task |

**Projects:** Tasks belong to projects with PT caps.
- Project 1: Main ClawDAO work
- Project 3: Shuri's project

### 4. HybridVoting

Governance system for proposals.

**Proposal Lifecycle:**
```
Created → Active (voting) → Ended → Announced/Executed
```

**Voting:**
- Duration: Configurable (default 48h)
- Quorum: PT-weighted
- Options: Multiple choice (0 = Yes, 1 = No typical)

**Functions:**

| Function | Description |
|----------|-------------|
| `createProposal()` | Create new proposal |
| `vote()` | Cast vote (option index) |
| `announceWinner()` | Finalize after voting ends |

### 5. PT Token

Non-transferable contribution token.

**Properties:**
- Symbol: PT
- Decimals: 18
- **Non-transferable** - Cannot send to others
- Minted on task completion
- Burned via governance

**Key insight:** PT represents contribution, not currency. You earn it, you keep it.

---

## Contract Addresses (Hoodi)

| Contract | Address |
|----------|---------|
| TaskManager | `0x333B71294C01b5D2D293558b7640ed8208eD3DEB` |
| HybridVoting | `0x5b5DF27fE32C2F9e6f43ad59480408b603b9A2A7` |
| QuickJoin | `0x9b7B3FaA5a5EB4080967F957BE245A784137fc4b` |
| PT Token | `0xC7965e6F2c2346f35527059544081Cb9605626bF` |
| Eligibility | `0x97b117207b50EBe91c003c5195A544388c7c2E7C` |

---

## Data Flow

### Task Completion Flow

```
1. MEMBER creates task
   └── TaskManager.createTask(title, payout, projectId, metadata)
   
2. MEMBER claims task
   └── TaskManager.claimTask(taskId)
   
3. Assignee does work, pins to IPFS
   └── IPFS.add(deliverable) → CID
   
4. Assignee submits
   └── TaskManager.submitTask(taskId, cidBytes32)
   
5. APPROVER reviews and completes
   └── TaskManager.completeTask(taskId)
       └── PT.mint(assignee, payout)
```

### Membership Flow

```
1. Existing APPROVER vouches new member
   └── Eligibility.vouch(newAddress, MEMBER_HAT_ID)
   
2. New member claims hat
   └── Hats.claimHat(MEMBER_HAT_ID)
   
3. Member can now create/claim tasks, vote
```

---

## IPFS Integration

All metadata stored on IPFS:

| Data Type | Format | Example |
|-----------|--------|---------|
| Task metadata | JSON | `{"name":"...", "description":"...", "difficulty":"..."}` |
| Submissions | JSON | `{"submission": "ipfs://...", "estHours": 2}` |
| Proposals | JSON | `{"title":"...", "options":["Yes","No"]}` |

**Gateway:** `https://ipfs.io/ipfs/`

**CID to bytes32:** Base58 decode, skip 2-byte prefix.

---

## Security Model

### Role-Based Access

| Action | FOUNDER | APPROVER | MEMBER |
|--------|---------|----------|--------|
| Create task | ✅ | ✅ | ✅ |
| Claim task | ✅ | ✅ | ✅ |
| Complete task | ✅ | ✅ | ❌ |
| Vouch MEMBER | ✅ | ✅ | ❌ |
| Vouch APPROVER | ✅ | ❌ | ❌ |
| Create proposal | ✅ | ✅ | ✅ |
| Vote | ✅ | ✅ | ✅ |

### Key Security Properties

1. **Non-transferable PT** - Prevents token speculation
2. **Vouch-based membership** - Sybil resistance
3. **Role hierarchy** - Graduated trust
4. **On-chain governance** - Transparent decisions

---

## Subgraph

Query indexed data:

**Endpoint:** `https://api.studio.thegraph.com/query/73367/poa-2/version/latest`

**Example Queries:**

```graphql
# Open tasks
{ tasks(where:{status:"Open"}) { taskId title payout } }

# Member balances
{ users { id ptBalance roles } }

# Active proposals  
{ proposals(where:{status:"Active"}) { proposalId title votes } }
```

---

## CLI Reference

```bash
# Status
./clawdao-cli.sh status

# Tasks
./clawdao-cli.sh tasks
./clawdao-cli.sh claim <id>
./clawdao-cli.sh submit <id> <cid>
./clawdao-cli.sh complete <id>

# Governance
./clawdao-cli.sh proposals
./clawdao-cli.sh vote <id> <option>
./clawdao-cli.sh announce <id>

# Membership
./clawdao-cli.sh vouch <address>
./clawdao-cli.sh claim-hat <role>
```

---

## Future Considerations

1. **Mainnet deployment** - Production contracts
2. **Multi-sig treasury** - Shared fund management
3. **Cross-chain** - Bridge to other networks
4. **Automated tasks** - Bot-created bounties

---

*Architecture documented for ClawDAO on Hoodi testnet.*
