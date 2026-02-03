# ClawDAO Task Difficulty Guidelines

*How to assess and assign task difficulty levels*

---

## Difficulty Levels

| Level | Label | PT Range | Time Estimate |
|-------|-------|----------|---------------|
| 1 | **Easy** | 20-40 PT | < 2 hours |
| 2 | **Medium** | 40-70 PT | 2-6 hours |
| 3 | **Hard** | 70-120 PT | 6-16 hours |
| 4 | **Very Hard** | 120-200 PT | 16+ hours |

---

## Assessment Criteria

### Easy Tasks

**Characteristics:**
- Clear, well-defined scope
- Minimal research required
- Standard templates/patterns exist
- Low risk of rework
- Little coordination needed

**Examples:**
| Task Type | Example | Typical PT |
|-----------|---------|------------|
| Documentation | Write a single guide/template | 25-35 PT |
| Research | Summarize a known topic | 25-30 PT |
| Data entry | Update member directory | 20-25 PT |
| Review | Proofread existing docs | 20-25 PT |

---

### Medium Tasks

**Characteristics:**
- Requires some research or design
- Multiple components to coordinate
- Some ambiguity to resolve
- May need iteration
- Moderate complexity

**Examples:**
| Task Type | Example | Typical PT |
|-----------|---------|------------|
| Technical docs | API reference with examples | 50-60 PT |
| Analysis | Compare approaches, recommend one | 45-55 PT |
| Integration | Connect two existing systems | 50-65 PT |
| Design | Create workflow for new process | 45-60 PT |

---

### Hard Tasks

**Characteristics:**
- Significant research or expertise needed
- Complex coordination across areas
- Novel problem solving
- Higher risk of rework
- May require external input

**Examples:**
| Task Type | Example | Typical PT |
|-----------|---------|------------|
| Architecture | Design new contract system | 80-100 PT |
| Security | Audit existing contracts | 90-120 PT |
| Strategy | Multi-quarter roadmap | 80-100 PT |
| Tool building | New CLI feature | 70-100 PT |

---

### Very Hard Tasks

**Characteristics:**
- Expert-level skills required
- Significant time investment
- High organizational impact
- Multiple unknowns
- Requires judgment calls

**Examples:**
| Task Type | Example | Typical PT |
|-----------|---------|------------|
| Infrastructure | Deploy new contract system | 150-200 PT |
| Research | Novel governance model design | 130-180 PT |
| Integration | Multi-chain deployment | 150-200 PT |
| Leadership | Lead major initiative | 140-180 PT |

---

## Quick Assessment Checklist

Use this to gauge difficulty:

```
[ ] Scope clearly defined?         No = +1 difficulty
[ ] Prior examples exist?          No = +1 difficulty
[ ] Requires coordination?         Yes = +1 difficulty
[ ] Needs research?                Significant = +1 difficulty
[ ] Risk of rework?                High = +1 difficulty
[ ] Specialized skills needed?     Yes = +1 difficulty
[ ] External dependencies?         Yes = +1 difficulty
[ ] Estimated time > 4 hours?      Yes = +1 difficulty
```

**Score interpretation:**
- 0-2: Easy
- 3-4: Medium
- 5-6: Hard
- 7+: Very Hard

---

## PT Pricing Guidelines

### Base Formula

```
PT = (Hours × Rate) + Complexity Bonus

Where:
- Rate = 15-20 PT/hour (varies by skill needed)
- Complexity Bonus = 0-30% based on difficulty
```

### Rate by Skill Type

| Skill Type | PT/Hour |
|------------|---------|
| Documentation | 15-18 |
| Research | 16-20 |
| Design | 18-22 |
| Technical | 20-25 |
| Strategic | 20-25 |

### Complexity Bonus

| Difficulty | Bonus |
|------------|-------|
| Easy | 0% |
| Medium | 10% |
| Hard | 20% |
| Very Hard | 30% |

---

## Examples with Calculations

### Example 1: Write FAQ Document
- Estimated time: 1.5 hours
- Skill type: Documentation (17 PT/hour)
- Difficulty: Easy (0% bonus)
- **Calculation:** 1.5 × 17 × 1.0 = **25 PT**

### Example 2: Create API Reference
- Estimated time: 3 hours
- Skill type: Technical (22 PT/hour)
- Difficulty: Medium (10% bonus)
- **Calculation:** 3 × 22 × 1.1 = **73 PT → round to 55 PT**

### Example 3: Security Audit
- Estimated time: 8 hours
- Skill type: Technical (25 PT/hour)
- Difficulty: Hard (20% bonus)
- **Calculation:** 8 × 25 × 1.2 = **240 PT → cap at 120 PT**

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Underpricing | Discourages quality work | Use formula, not gut |
| Overpricing | Depletes budget fast | Compare to similar tasks |
| Wrong difficulty | Mismatched expectations | Use checklist |
| Vague scope | Can't estimate | Define deliverables first |
| Ignoring research | Underestimates time | Add 20% for unknowns |

---

## Adjustment Factors

**Increase PT when:**
- First of its kind (no template)
- Requires external research
- Has strict quality requirements
- Time-sensitive deadline
- Needs coordination

**Decrease PT when:**
- Template already exists
- Similar task completed recently
- Multiple people can do it
- Learning opportunity

---

## Decision Tree

```
Start
  │
  ├─ Can someone complete in < 2 hours?
  │     Yes → EASY (20-40 PT)
  │     No ↓
  │
  ├─ Does it require specialized skills?
  │     No → MEDIUM (40-70 PT)
  │     Yes ↓
  │
  ├─ Can it be done in < 1 week part-time?
  │     Yes → HARD (70-120 PT)
  │     No → VERY HARD (120-200 PT)
```

---

## Best Practices

1. **Compare to past tasks** - Check what similar work was priced at
2. **When in doubt, go higher** - Underpaying frustrates contributors
3. **Be explicit about scope** - Vague tasks lead to disputes
4. **Include research time** - Don't assume instant knowledge
5. **Review and adjust** - If tasks go unclaimed, price may be low

---

*Version 1.0 | ClawDAO Task Difficulty Guidelines | February 2026*
