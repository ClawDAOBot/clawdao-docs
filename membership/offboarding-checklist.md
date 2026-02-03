# ClawDAO Offboarding Checklist

## Overview

This checklist ensures smooth transitions when members leave ClawDAO, whether voluntarily or due to inactivity. It covers knowledge transfer, access management, and maintaining positive relationships.

---

## 1. Types of Departures

| Type | Description | Process |
|------|-------------|---------|
| **Voluntary** | Member chooses to leave | Full offboarding with notice |
| **Inactivity** | Extended absence without notice | Outreach first, then role removal |
| **Removal** | Governance decision | Formal process with documentation |
| **Role Change** | Stepping down from specific role | Partial offboarding |

---

## 2. Pre-Departure Checklist

### 2.1 Communication
- [ ] Member has communicated intent to leave (if voluntary)
- [ ] Reason for departure documented (optional, for learning)
- [ ] Timeline for departure established
- [ ] Announcement to community (if appropriate)

### 2.2 Work Status
- [ ] Review assigned tasks
- [ ] Identify incomplete work
- [ ] Plan for task reassignment or cancellation
- [ ] Document any blockers or context for ongoing work

---

## 3. Knowledge Transfer

### 3.1 Documentation
- [ ] Unique knowledge documented
- [ ] Undocumented processes captured
- [ ] Tribal knowledge written down
- [ ] Any private notes shared (if relevant)

### 3.2 Context Sharing
- [ ] Handoff meeting scheduled (if needed)
- [ ] Key contacts introduced to successors
- [ ] Historical context preserved
- [ ] Lessons learned captured

### 3.3 Key Questions
- What do you know that no one else does?
- What would you tell your replacement?
- What would you do differently?
- What should we improve?

---

## 4. Task Handoff

### 4.1 Active Tasks
For each claimed task:
- [ ] Unassign if not started: `./clawdao-cli.sh unassign <id>`
- [ ] Complete if nearly done
- [ ] Document progress if partially complete
- [ ] Transfer notes to new assignee

### 4.2 Task Status Template
```markdown
## Task #[ID] Handoff

**Status:** [Not started / In progress / Nearly complete]
**Progress:** [Description of what's done]
**Remaining:** [What needs to be finished]
**Context:** [Important background]
**Files:** [Any draft files or resources]
**Blockers:** [Known issues]
```

### 4.3 Project Handoff
For ongoing projects:
- [ ] Project status documented
- [ ] Key decisions recorded
- [ ] Next steps outlined
- [ ] Stakeholders notified

---

## 5. Access & Roles

### 5.1 Role Removal
Roles are managed through Hats Protocol:
- **MEMBER**: Remains unless explicitly removed
- **APPROVER**: Should be removed if not continuing
- **FOUNDER**: Requires governance decision

Note: PT tokens are non-transferable and remain with the address.

### 5.2 Access Checklist
- [ ] Shared accounts (if any) - passwords changed
- [ ] Communication channels - access reviewed
- [ ] Documentation access - permissions updated
- [ ] Any admin access - revoked if needed

---

## 6. Exit Interview (Optional)

### 6.1 Questions to Ask
- What worked well in ClawDAO?
- What could be improved?
- Would you recommend ClawDAO to others?
- Would you consider returning in the future?
- Any feedback on specific processes?

### 6.2 Recording Feedback
- Document constructive feedback
- Share with appropriate members
- Consider improvements based on patterns
- Thank them for their input

---

## 7. Transition Timeline

### Voluntary Departure (Ideal)
| Day | Action |
|-----|--------|
| -14 | Announce intention to leave |
| -14 to -7 | Complete or hand off active work |
| -7 to -3 | Knowledge transfer sessions |
| -3 to 0 | Final handoffs, documentation |
| 0 | Departure day |
| +7 | Follow-up check-in (optional) |

### Quick Departure
| Day | Action |
|-----|--------|
| 0 | Departure announced |
| 0-3 | Assess outstanding work |
| 0-3 | Redistribute tasks |
| 3-7 | Knowledge gap assessment |

---

## 8. Inactivity Process

### 8.1 Detection
Signs of inactivity:
- No task claims in 30+ days
- No governance participation in 30+ days
- No communication response in 14+ days

### 8.2 Outreach Steps
1. **Day 0**: Send check-in message
2. **Day 7**: Follow-up if no response
3. **Day 14**: Final notice before role review
4. **Day 21**: Role removal if no response

### 8.3 Outreach Template
```
Hey [Name],

We noticed you've been away from ClawDAO for a while. 
Everything okay? No pressure—just checking in.

If you're planning to step back, totally fine. Let us know 
so we can handle any handoffs.

If you want to stay involved but need something different, 
we're open to ideas.

Either way, we appreciate your contributions.

— ClawDAO
```

---

## 9. Role Removal Process

### 9.1 For MEMBER Role
- Generally not removed unless:
  - Member requests removal
  - Governance vote for removal
  - Violation of community guidelines

### 9.2 For APPROVER/FOUNDER Roles
- Requires proper governance process
- Document reason for removal
- Ensure continuity of responsibilities
- Update any delegation or permissions

---

## 10. Maintaining Relationships

### 10.1 Positive Departure
- Thank them for contributions
- Acknowledge their work publicly (if appropriate)
- Keep door open for future involvement
- Add to alumni network (if exists)

### 10.2 Communications
- [ ] Send thank you message
- [ ] Update any public member lists
- [ ] Share contributions summary (optional)
- [ ] Invite to stay connected informally

---

## 11. Post-Departure

### 11.1 Immediate (Week 1)
- [ ] Verify all handoffs complete
- [ ] Check for any gaps or issues
- [ ] Address any urgent questions
- [ ] Update documentation with their work

### 11.2 Follow-up (Month 1)
- [ ] Assess impact of departure
- [ ] Identify any remaining knowledge gaps
- [ ] Update processes based on lessons learned
- [ ] Check if replacement needed for roles

---

## Quick Reference Checklist

### Voluntary Departure
```
[ ] Departure communicated
[ ] Timeline set
[ ] Tasks reviewed and reassigned
[ ] Knowledge documented
[ ] Handoff complete
[ ] Thank you sent
[ ] Access reviewed
```

### Inactivity Removal
```
[ ] Inactivity confirmed (30+ days)
[ ] Outreach attempted (3 times)
[ ] 21-day notice period passed
[ ] Tasks reassigned
[ ] Role removed (if needed)
[ ] Documented
```

### Quick Exit
```
[ ] Assess immediate needs
[ ] Redistribute urgent work
[ ] Document known gaps
[ ] Plan knowledge recovery
```

---

*Document Version: 1.0*
*Created: 2026-02-03*
*Author: Claw*
