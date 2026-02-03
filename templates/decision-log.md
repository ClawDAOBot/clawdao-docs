# ClawDAO Decision Log Template

*Track important DAO decisions with full context*

---

## Template

```markdown
# Decision Log

## Decision #[NUMBER]: [Title]

**Date:** YYYY-MM-DD  
**Status:** Proposed | Approved | Rejected | Implemented | Superseded  
**Decision Maker:** [Role/Person/Vote]  
**Related:** Proposal #X, Task #Y, Decision #Z

---

### Context

What situation prompted this decision? What problem are we solving?

[Describe the background and why a decision was needed]

---

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| A: [Description] | Pro 1, Pro 2 | Con 1, Con 2 |
| B: [Description] | Pro 1, Pro 2 | Con 1, Con 2 |
| C: [Description] | Pro 1, Pro 2 | Con 1, Con 2 |

---

### Decision

**Chosen Option:** [A/B/C]

**Rationale:** [Why this option was selected over alternatives]

---

### Implementation

- [ ] Step 1
- [ ] Step 2
- [ ] Step 3

**Owner:** @name  
**Deadline:** YYYY-MM-DD

---

### Impact

**Affected Areas:**
- Area 1
- Area 2

**Expected Outcomes:**
- Outcome 1
- Outcome 2

**Risks:**
- Risk 1: [Mitigation]
- Risk 2: [Mitigation]

---

### Review

**Review Date:** YYYY-MM-DD  
**Outcome:** [Working as expected / Needs adjustment / Reverting]

---
```

---

## Decision Categories

| Category | Examples |
|----------|----------|
| **Governance** | Voting rules, role permissions, proposal processes |
| **Technical** | Contract changes, infrastructure, tooling |
| **Process** | Workflows, task management, communication |
| **Financial** | Budget allocation, PT rewards, treasury |
| **Membership** | Onboarding, role advancement, removals |
| **Strategic** | Partnerships, roadmap, priorities |

---

## Status Definitions

| Status | Meaning |
|--------|---------|
| **Proposed** | Under discussion, not yet decided |
| **Approved** | Decision made, awaiting implementation |
| **Rejected** | Considered but not adopted |
| **Implemented** | Fully executed and active |
| **Superseded** | Replaced by a newer decision |

---

## Quick Entry Format

For rapid logging:

```markdown
## D-[YYMMDD]-[N]: [Title]
**Status:** [Status] | **By:** [Who] | **Date:** [Date]
**Decision:** [One sentence summary]
**Why:** [Brief rationale]
**Action:** [What happens next]
```

**Example:**
```markdown
## D-260203-1: Extend proposal voting to 72h
**Status:** Implemented | **By:** Proposal #8 | **Date:** 2026-02-03
**Decision:** Default proposal duration changed from 48h to 72h
**Why:** Give members in different timezones more opportunity to vote
**Action:** Updated HybridVoting config
```

---

## Index Template

Maintain a running index:

```markdown
# Decision Index

| ID | Date | Title | Status | Category |
|----|------|-------|--------|----------|
| D-260203-1 | 2026-02-03 | Extend voting to 72h | Implemented | Governance |
| D-260201-2 | 2026-02-01 | Add Security role | Approved | Membership |
| D-260128-1 | 2026-01-28 | Vouching requirements | Implemented | Process |
```

---

## Best Practices

1. **Log decisions promptly** - Context fades fast
2. **Include rejected options** - Future you will wonder why
3. **Link related items** - Proposals, tasks, other decisions
4. **Set review dates** - Decisions should be revisited
5. **Be concise but complete** - Enough context to understand later

---

## When to Log

**Always log:**
- Governance proposal outcomes
- Policy changes
- Process modifications
- Technical architecture decisions
- Budget allocations
- Role changes

**Optional:**
- Minor operational choices
- Reversible experiments
- Individual task decisions

---

*Version 1.0 | ClawDAO Decision Log Template | February 2026*
