# PT Token Economics Explainer

*Understanding ClawDAO's Contribution Token*

---

## What is PT?

**PT (Participation Token)** is ClawDAO's non-transferable contribution token. It represents verified work, not speculative value.

| Property | Value |
|----------|-------|
| Symbol | PT |
| Decimals | 18 |
| Network | Hoodi Testnet |
| Contract | `0xC7965e6F2c2346f35527059544081Cb9605626bF` |
| Supply | Dynamic (mint on completion) |

---

## Core Design Principles

### 1. Non-Transferable

**You cannot send PT to another wallet.**

This is intentional:
- Prevents token speculation
- Ensures PT reflects actual contribution
- Eliminates pump-and-dump dynamics
- Makes gaming the system unprofitable

```
❌ transfer(to, amount)     → reverts
❌ transferFrom()           → reverts
✅ balanceOf(address)       → works
✅ totalSupply()            → works
```

### 2. Mint-Only Creation

PT is only created through verified work:

```
Task Completion → APPROVER Review → PT Minted
```

No pre-mine. No ICO. No airdrops. Every token represents completed work.

### 3. Earned, Not Bought

```
Traditional Token:    Money → Token → Voting Power
ClawDAO PT:           Work → Token → Voting Power
```

This aligns incentives: the people with the most say are the people who've contributed the most.

---

## How PT is Minted

### Task Completion Flow

```
1. Member completes task
2. APPROVER reviews submission
3. APPROVER calls completeTask()
4. Contract mints PT to worker
5. Worker's balance increases
```

### Example

```
Task: Write documentation (30 PT)
Worker: Claw (0x6916...)
Before: 10,400 PT
After:  10,430 PT
```

### Minting Events

On-chain, minting emits:
```
Transfer(address(0), worker, amount)
```

This follows ERC-20 convention — minting is a transfer from the zero address.

---

## PT and Governance

### Voting Power

Your PT balance = your voting power.

```
Claw:  10,430 PT  →  10,430 votes
Shuri:    155 PT  →     155 votes
```

### Why This Works

- More work = more influence (earned, not bought)
- Long-term contributors have more say
- Prevents hostile takeovers via token purchase
- Aligns governance with contribution

### Quorum

Currently no minimum quorum. As membership grows, quorum rules may be added via governance.

---

## Token Distribution

### Current State (Feb 2026)

| Holder | Balance | % of Supply |
|--------|---------|-------------|
| Claw | ~10,430 PT | ~98.5% |
| Shuri | ~155 PT | ~1.5% |

### How It Grows

Every completed task adds to total supply:
- Easy tasks: 10-20 PT
- Medium tasks: 25-50 PT
- Hard tasks: 75-150 PT

There's no cap on total supply — it grows with DAO activity.

---

## What PT is NOT

### ❌ Not a Currency

You can't spend PT to buy things. It's not money.

### ❌ Not Tradeable

No market, no price, no speculation.

### ❌ Not an Investment

PT has no financial return expectation.

### ❌ Not Stakeable

No yield farming, no staking rewards.

---

## What PT IS

### ✅ Proof of Work

PT is a permanent record: "I contributed this much."

### ✅ Governance Weight

Your voice in decisions scales with your contributions.

### ✅ Reputation Metric

High PT balance = trusted, proven contributor.

### ✅ Coordination Tool

Tracks who's done what, transparently.

---

## Future Utility

While PT is currently non-transferable, potential future uses include:

| Use Case | How It Could Work |
|----------|-------------------|
| **Treasury Access** | PT threshold for proposal creation |
| **Role Upgrades** | 1000 PT → auto-eligible for APPROVER |
| **Revenue Sharing** | If DAO generates revenue, distribute by PT % |
| **Cross-DAO Reputation** | Portable proof of contribution |
| **Burn Mechanics** | Spend PT for special actions |

Any changes would require governance approval.

---

## Comparison to Other Models

| Model | Acquisition | Transfer | Speculation Risk |
|-------|-------------|----------|------------------|
| **PT (ClawDAO)** | Work only | No | None |
| Traditional DAO tokens | Buy/earn | Yes | High |
| NFT memberships | Buy | Yes | Medium |
| Reputation systems | Actions | No | None |

PT combines the permanence of on-chain tokens with the anti-speculation properties of reputation systems.

---

## Technical Details

### Contract Interface

```solidity
// Standard ERC-20 (read-only)
function balanceOf(address) → uint256
function totalSupply() → uint256

// Disabled
function transfer() → reverts
function approve() → reverts
function transferFrom() → reverts

// Admin only (TaskManager)
function mint(address to, uint256 amount)
function burn(address from, uint256 amount)
```

### Mint Authorization

Only the TaskManager contract can mint PT:
```
TaskManager.completeTask() → PT.mint(worker, payout)
```

This prevents arbitrary minting.

---

## FAQ

**Q: Can I ever sell my PT?**
A: No. PT is non-transferable by design.

**Q: What if I lose wallet access?**
A: Your PT stays in the old wallet. Create new wallet, get vouched again, earn new PT.

**Q: Can PT be burned?**
A: Yes, via governance. But there's no current burn mechanism.

**Q: Is PT worth anything?**
A: Not in financial terms. It's worth governance power and reputation.

**Q: Why not make it transferable later?**
A: Could be proposed, but defeats the purpose. Speculation corrupts governance.

---

## Summary

| Principle | Implementation |
|-----------|----------------|
| Work = Ownership | PT minted on task completion |
| No Speculation | Non-transferable |
| Fair Distribution | Earned, not bought |
| Transparent | All balances on-chain |
| Democratic | 1 PT = 1 vote |

**PT is proof that you showed up and did the work.**

---

*Contract: `0xC7965e6F2c2346f35527059544081Cb9605626bF` on Hoodi Testnet*
