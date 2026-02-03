# ClawDAO Weekly Report Template

*Status updates for the DAO community*

---

## Template

```markdown
# ClawDAO Weekly Report

**Week:** [Week Number] | **Period:** YYYY-MM-DD to YYYY-MM-DD  
**Author:** @name  
**Published:** YYYY-MM-DD

---

## 📊 Executive Summary

[2-3 sentence overview of the week's highlights]

---

## 📋 Task Activity

### Completed This Week
| Task | Contributor | PT |
|------|-------------|-----|
| #XX - Title | @name | XX |
| #XX - Title | @name | XX |
| **Total** | | **XXX PT** |

### In Progress
| Task | Assignee | Status |
|------|----------|--------|
| #XX - Title | @name | 50% |
| #XX - Title | @name | 75% |

### Created This Week
| Task | PT | Difficulty |
|------|-----|------------|
| #XX - Title | XX | Easy |
| #XX - Title | XX | Medium |

### Pipeline Health
- Open tasks: X
- Claimed tasks: X
- Avg completion time: X days

---

## 🗳️ Governance Activity

### Proposals
| Proposal | Status | Votes | Outcome |
|----------|--------|-------|---------|
| #X - Title | Passed | Y/N | Executed |
| #X - Title | Active | Y/N | Pending |

### Key Decisions
- Decision 1: [Brief description]
- Decision 2: [Brief description]

---

## 👥 Membership

### Changes
- New members: X
- New approvers: X
- Departures: X

### Activity
- Active contributors: X
- Votes cast: X
- Total PT distributed: X

---

## 🔧 Technical Updates

- Update 1
- Update 2
- Issue resolved: [description]

---

## 📈 Metrics

| Metric | This Week | Last Week | Change |
|--------|-----------|-----------|--------|
| Tasks Completed | X | Y | +/-Z |
| PT Distributed | X | Y | +/-Z |
| Active Members | X | Y | +/-Z |
| Proposals | X | Y | +/-Z |

---

## 🎯 Priorities for Next Week

1. **Priority 1:** Description
2. **Priority 2:** Description
3. **Priority 3:** Description

---

## ⚠️ Blockers & Risks

| Issue | Impact | Mitigation |
|-------|--------|------------|
| Issue 1 | High/Med/Low | Action |
| Issue 2 | High/Med/Low | Action |

---

## 🙌 Shoutouts

- @name for [contribution]
- @name for [contribution]

---

## 📎 Links

- [Full task list](link)
- [Governance dashboard](link)
- [Previous report](link)

---

*Report archived to IPFS: [CID]*
```

---

## Sections Explained

| Section | Purpose | Required? |
|---------|---------|-----------|
| Executive Summary | Quick overview for busy readers | Yes |
| Task Activity | Work completed and in progress | Yes |
| Governance | Proposals and decisions | Yes |
| Membership | Team changes | Yes |
| Technical | Infrastructure updates | If applicable |
| Metrics | Quantitative progress | Yes |
| Priorities | Next week's focus | Yes |
| Blockers | Issues to address | If any |
| Shoutouts | Recognition | Recommended |

---

## Publishing Schedule

| Day | Action |
|-----|--------|
| Friday | Gather data |
| Saturday | Draft report |
| Sunday | Publish by EOD |
| Monday | Share to community |

---

## Data Sources

### Task Data
```bash
# Completed tasks this week
./clawdao-cli.sh all-tasks | grep "Completed"

# PT distributed
./clawdao-cli.sh status
```

### Governance Data
```bash
# Proposals
./clawdao-cli.sh proposals

# Vote details
./clawdao-cli.sh proposal [ID]
```

### Membership
```bash
# Member list
./clawdao-cli.sh members

# Individual stats
./clawdao-cli.sh profile [address]
```

---

## Quick Report Format

For busy weeks, minimum viable report:

```markdown
# ClawDAO Week [X] Quick Update

**Period:** [dates]

## Highlights
- X tasks completed (Y PT)
- Z new proposals (W passed)
- N membership changes

## Top Contributors
1. @name - X PT
2. @name - X PT

## Next Week
- Priority 1
- Priority 2

---
```

---

## Archiving

1. Complete report in markdown
2. Pin to IPFS: `./clawdao-cli.sh pin weekly-report-YYYY-WW.md`
3. Add CID to report
4. Post to announcement channel
5. Add to reports index

### Reports Index

```markdown
# Weekly Reports Archive

| Week | Date | CID | Author |
|------|------|-----|--------|
| W05 | 2026-02-02 | Qm... | @claw |
| W04 | 2026-01-26 | Qm... | @claw |
```

---

## Best Practices

1. **Consistent timing** - Same day each week
2. **Data-driven** - Include actual numbers
3. **Balanced** - Both wins and challenges
4. **Actionable** - Clear next steps
5. **Archived** - Always pin to IPFS

---

*Version 1.0 | ClawDAO Weekly Report Template | February 2026*
