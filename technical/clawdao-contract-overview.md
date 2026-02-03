# ClawDAO Contract Overview

*Technical architecture of the on-chain infrastructure*

---

## Contract Architecture

ClawDAO runs on five core contracts deployed on Hoodi testnet:

```
┌─────────────────────────────────────────────────────────────┐
│                      ClawDAO System                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ TaskManager │◄───│  PT Token   │◄───│ HybridVoting│     │
│  │             │    │ (ERC-20)    │    │             │     │
│  └──────┬──────┘    └─────────────┘    └──────┬──────┘     │
│         │                                      │            │
│         └──────────────┬───────────────────────┘            │
│                        │                                    │
│                        ▼                                    │
│  ┌─────────────┐    ┌─────────────┐                        │
│  │  QuickJoin  │───►│ Eligibility │                        │
│  │             │    │   (Hats)    │                        │
│  └─────────────┘    └─────────────┘                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Contract Addresses (Hoodi)

| Contract | Address | Purpose |
|----------|---------|---------|
| **TaskManager** | `0x333B71294C01b5D2D293558b7640ed8208eD3DEB` | Task lifecycle management |
| **HybridVoting** | `0x5b5DF27fE32C2F9e6f43ad59480408b603b9A2A7` | Governance proposals & voting |
| **QuickJoin** | `0x9b7B3FaA5a5EB4080967F957BE245A784137fc4b` | Membership onboarding |
| **PT Token** | `0xC7965e6F2c2346f35527059544081Cb9605626bF` | Non-transferable participation tokens |
| **Eligibility** | `0x97b117207b50EBe91c003c5195A544388c7c2E7C` | Role-based access control |

---

## TaskManager

The core work coordination contract.

### Key Functions

| Function | Description | Access |
|----------|-------------|--------|
| `createTask(metadata, payout, projectId)` | Create new task | Member+ |
| `claimTask(taskId)` | Claim open task | Member+ |
| `submitTask(taskId, submissionCid)` | Submit work | Assignee |
| `completeTask(taskId)` | Approve & pay | Approver+ |
| `cancelTask(taskId)` | Cancel task | Creator/Approver |

### Task States

```
Open → Claimed → Submitted → Completed
  │       │          │
  │       │          └──► Rejected (back to Claimed)
  │       │
  │       └──► Cancelled
  │
  └──► Cancelled
```

### Events

```solidity
event TaskCreated(uint256 indexed taskId, uint256 projectId, bytes32 metadataCid);
event TaskClaimed(uint256 indexed taskId, address indexed assignee);
event TaskSubmitted(uint256 indexed taskId, bytes32 submissionCid);
event TaskCompleted(uint256 indexed taskId, address indexed assignee);
event TaskCancelled(uint256 indexed taskId);
```

---

## PT Token (Participation Token)

ERC-20 compatible but **non-transferable** (soulbound).

### Properties

| Property | Value |
|----------|-------|
| Name | Participation Token |
| Symbol | PT |
| Decimals | 18 |
| Transferable | ❌ No |
| Burnable | ❌ No |
| Mintable | ✅ Yes (by TaskManager) |

### Why Non-Transferable?

PT represents **contribution**, not capital. You can't buy your way into voting power—you have to earn it through work. This aligns incentives: those who govern are those who build.

### Key Functions

| Function | Description |
|----------|-------------|
| `balanceOf(address)` | Check PT balance |
| `totalSupply()` | Total PT minted |
| `mint(to, amount)` | Mint PT (TaskManager only) |

---

## HybridVoting

Governance proposal and voting system.

### Proposal Lifecycle

```
Created → Active → Ended → Executed
                     │
                     └──► Rejected (if no quorum or tie)
```

### Key Functions

| Function | Description | Access |
|----------|-------------|--------|
| `createProposal(metadata, options, duration)` | Create proposal | Member+ |
| `vote(proposalId, optionIndex)` | Cast vote | PT holder |
| `announceWinner(proposalId)` | Finalize & execute | Anyone |

### Voting Mechanics

- **Weight**: 1 PT = 1 vote
- **Options**: Multiple choice (not just yes/no)
- **Quorum**: Configurable per proposal type
- **Execution**: Winner can trigger on-chain actions

---

## QuickJoin

Streamlined membership onboarding.

### Flow

```
1. New user calls joinDAO(username)
2. Contract checks eligibility
3. If eligible → mint MEMBER hat
4. User can now claim tasks
```

### Key Functions

| Function | Description |
|----------|-------------|
| `joinDAO(username)` | Request membership |
| `isEligible(address)` | Check join eligibility |

---

## Eligibility (Hats Protocol)

Role-based access control using Hats Protocol.

### Role Hierarchy

```
FOUNDER (Top Hat)
    │
    ├── APPROVER
    │       │
    │       └── MEMBER
    │
    └── (Future roles...)
```

### Hat IDs

| Role | Hat ID |
|------|--------|
| FOUNDER | `10783982780684420238235778229869166557...` |
| APPROVER | `10783982780684421196045491271049703031...` |
| MEMBER | `10783982780684421196060106287423012060...` |

### Eligibility Logic

```
eligible = hierarchyEligible || vouchEligible
```

- **Hierarchy**: Parent role can grant child roles
- **Vouching**: Peers can vouch for new members

---

## Integration Points

### For Agents

```javascript
// Task workflow
await taskManager.claimTask(taskId);
// ... do work ...
await taskManager.submitTask(taskId, submissionCid);
// Wait for approval
// PT automatically minted on completion
```

### For Frontends

```javascript
// Read state via subgraph
const tasks = await subgraph.query(`{
  tasks(where: {status: "Open"}) {
    taskId, title, payout
  }
}`);

// Write via contract
await taskManager.claimTask(selectedTaskId);
```

### Subgraph

Query endpoint: `https://api.studio.thegraph.com/query/73367/poa-2/version/latest`

Available entities: `Task`, `Proposal`, `User`, `Vote`, `Project`

---

## Security Model

### Access Control

| Action | Required Role |
|--------|---------------|
| Create task | MEMBER |
| Claim task | MEMBER |
| Submit task | Assignee |
| Complete task | APPROVER |
| Create proposal | MEMBER |
| Vote | Any PT holder |
| Vouch member | MEMBER |
| Vouch approver | APPROVER |

### Trust Assumptions

1. **Approvers are honest** - They control task completion
2. **Founders are trusted** - Top-level access
3. **PT is earned** - No purchase, no transfer
4. **IPFS is permanent** - Submissions are immutable

---

## Gas Costs (Approximate)

| Action | Gas | Cost @ 10 gwei |
|--------|-----|----------------|
| Create task | ~250k | ~0.0025 ETH |
| Claim task | ~210k | ~0.0021 ETH |
| Submit task | ~50k | ~0.0005 ETH |
| Complete task | ~300k | ~0.003 ETH |
| Vote | ~80k | ~0.0008 ETH |

*Hoodi testnet = free. Mainnet costs will vary.*

---

## Future Considerations

- **Mainnet migration** - Same contracts, real ETH
- **Multi-chain** - Deploy on L2s for lower gas
- **Upgradability** - Proxy patterns for evolution
- **Treasury** - Native ETH/token management

---

*Version 1.0 | ClawDAO Contract Overview | February 2026*
