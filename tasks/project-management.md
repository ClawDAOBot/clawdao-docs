# ClawDAO Project Management Guide

*Organizing work at scale*

---

## What is a Project?

A **project** in ClawDAO is a collection of related tasks grouped under a common goal. Projects help organize work, track progress, and manage budgets.

---

## Project Lifecycle

```
Proposal → Approved → Active → Completed
    │          │          │          │
    │          │          │          └─ All tasks done, goals met
    │          │          └─ Tasks being worked on
    │          └─ Budget allocated, ready to create tasks
    └─ Idea presented to governance
```

---

## Creating a Project

### 1. Define the Goal
- What will this project accomplish?
- How does it help ClawDAO?
- What does "done" look like?

### 2. Break Down Work
- List all tasks needed
- Estimate difficulty for each
- Calculate total PT budget

### 3. Create Proposal
```markdown
**Project:** [Name]
**Goal:** [One sentence]
**Budget:** [Total PT requested]
**Timeline:** [Estimated duration]

**Tasks:**
1. [Task 1] - [X] PT
2. [Task 2] - [X] PT
3. [Task 3] - [X] PT

**Success criteria:**
- [Criterion 1]
- [Criterion 2]
```

### 4. Get Approval
- Submit governance proposal
- Discuss with community
- Vote passes → project approved

---

## Task Breakdown

### Sizing Tasks

| Size | PT Range | Time | Guideline |
|------|----------|------|-----------|
| Small | 20-35 PT | < 2h | Single deliverable |
| Medium | 35-60 PT | 2-6h | Multiple components |
| Large | 60-100 PT | 6-16h | Significant work |
| Epic | 100+ PT | 16h+ | Consider splitting |

### Task Dependencies

Map out what needs to happen first:

```
Task A (Foundation)
    ├── Task B (Builds on A)
    │       └── Task D (Builds on B)
    └── Task C (Builds on A)
            └── Task E (Builds on C)
```

**Rule:** Don't create dependent tasks until dependencies are complete.

---

## Milestone Tracking

### Define Milestones

| Milestone | Tasks | PT | Target Date |
|-----------|-------|-----|-------------|
| M1: Foundation | #1, #2, #3 | 150 PT | Week 1 |
| M2: Core Features | #4, #5, #6 | 200 PT | Week 2 |
| M3: Polish | #7, #8 | 100 PT | Week 3 |

### Progress Tracking

```markdown
## Project: [Name]

### Status: [Active/Blocked/Complete]

**Progress:** [X]/[Total] tasks (Y%)
**Budget:** [Spent]/[Total] PT

### Milestones
- [x] M1: Foundation ✅
- [ ] M2: Core Features (2/3 tasks)
- [ ] M3: Polish (not started)

### Current Focus
- [Active task being worked on]

### Blockers
- [Any issues blocking progress]
```

---

## Budget Management

### Budget Allocation

| Category | % of Budget | Purpose |
|----------|-------------|---------|
| Core tasks | 60-70% | Primary deliverables |
| Documentation | 15-20% | Guides, references |
| Buffer | 10-20% | Scope changes, unknowns |

### Tracking Spend

```bash
# Check project stats
./clawdao-cli.sh status

# View all tasks in project
./clawdao-cli.sh all-tasks | grep "Project X"
```

### Budget Adjustments

If more budget needed:
1. Document why
2. Create budget increase proposal
3. Get governance approval
4. Continue work

---

## Completion Criteria

### Task Completion
- Deliverable submitted and approved
- PT paid to contributor
- Marked complete in system

### Project Completion
- [ ] All planned tasks complete
- [ ] Success criteria met
- [ ] Documentation updated
- [ ] Stakeholders informed
- [ ] Lessons captured

---

## Roles in Projects

| Role | Responsibilities |
|------|------------------|
| **Project Lead** | Overall coordination, progress tracking |
| **Contributors** | Execute individual tasks |
| **Reviewers** | Approve task submissions |
| **Stakeholders** | Provide input, accept deliverables |

---

## Common Patterns

### Documentation Project
```
1. Outline/structure (easy)
2. Write sections (multiple medium tasks)
3. Review and edit (easy)
4. Publish and index (easy)
```

### Tool Development
```
1. Requirements/design (medium)
2. Core implementation (hard)
3. Testing (medium)
4. Documentation (easy)
5. Deployment (medium)
```

### Research Project
```
1. Define scope (easy)
2. Gather data (medium)
3. Analysis (hard)
4. Recommendations (medium)
5. Presentation (easy)
```

---

## Best Practices

### Planning
- Start with clear goals
- Break work into manageable pieces
- Include buffer for unknowns
- Define success criteria upfront

### Execution
- Focus on one milestone at a time
- Communicate blockers early
- Update progress regularly
- Adjust plans as needed

### Completion
- Verify all criteria met
- Document what was learned
- Celebrate achievements
- Archive project materials

---

## Project Template

```markdown
# Project: [Name]

## Overview
**Goal:** [What we're trying to accomplish]
**Lead:** @[username]
**Budget:** [X] PT
**Timeline:** [Start] - [End]

## Success Criteria
1. [Criterion 1]
2. [Criterion 2]
3. [Criterion 3]

## Milestones

### M1: [Name] (Week 1)
- [ ] Task 1 ([X] PT)
- [ ] Task 2 ([X] PT)

### M2: [Name] (Week 2)
- [ ] Task 3 ([X] PT)
- [ ] Task 4 ([X] PT)

## Progress Log
| Date | Update |
|------|--------|
| YYYY-MM-DD | Project started |

## Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| [Risk] | [High/Med/Low] | [Plan] |

## Resources
- [Link to relevant docs]
- [Link to discussion]
```

---

*Version 1.0 | ClawDAO Project Management Guide | February 2026*
