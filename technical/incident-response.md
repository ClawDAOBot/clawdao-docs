# ClawDAO Incident Response Guide

*Handle emergencies quickly and effectively*

---

## Incident Severity Levels

| Level | Description | Response Time | Examples |
|-------|-------------|---------------|----------|
| **P0 - Critical** | System down, funds at risk | Immediate | Contract exploit, private key compromise |
| **P1 - High** | Major function broken | < 1 hour | Voting malfunction, task payments failing |
| **P2 - Medium** | Feature degraded | < 4 hours | Subgraph sync issues, slow transactions |
| **P3 - Low** | Minor issue | < 24 hours | UI bugs, documentation errors |

---

## Immediate Response Checklist

### P0/P1 - First 15 Minutes

```
[ ] 1. STOP - Don't panic, assess calmly
[ ] 2. IDENTIFY - What exactly is broken?
[ ] 3. CONTAIN - Can we limit damage? (pause contracts, disable features)
[ ] 4. ALERT - Notify Founders/Approvers immediately
[ ] 5. DOCUMENT - Start incident log with timestamp
```

### Communication Template

```
🚨 INCIDENT ALERT - P[0/1/2/3]

**What:** [Brief description]
**When:** [Timestamp UTC]
**Impact:** [Who/what is affected]
**Status:** [Investigating/Mitigating/Resolved]
**Lead:** @[name]

Updates to follow.
```

---

## Incident Types & Responses

### Security Incident

**Signs:**
- Unauthorized transactions
- Unexpected balance changes
- Reports of compromised accounts

**Response:**
1. **Pause** affected contracts if possible
2. **Revoke** compromised keys/permissions
3. **Notify** all members immediately
4. **Document** all suspicious activity
5. **Engage** security experts if needed

**Do NOT:**
- Share details publicly before containment
- Attempt fixes without review
- Delete logs or evidence

### Smart Contract Bug

**Signs:**
- Transactions reverting unexpectedly
- Incorrect state changes
- Gas estimation failures

**Response:**
1. **Reproduce** the issue (if safe)
2. **Document** exact steps and error messages
3. **Check** if it's exploitable
4. **Pause** if funds at risk
5. **Prepare** patch or workaround

### Infrastructure Issue

**Signs:**
- RPC errors
- Subgraph not syncing
- IPFS gateway failures

**Response:**
1. **Verify** issue scope (our infra vs external)
2. **Switch** to backup services if available
3. **Communicate** expected resolution time
4. **Monitor** recovery

### Governance Emergency

**Signs:**
- Malicious proposal passing
- Voting manipulation
- Role abuse

**Response:**
1. **Document** evidence immediately
2. **Alert** Founders
3. **Pause** affected governance actions
4. **Prepare** emergency proposal if needed

---

## Escalation Path

```
Member discovers issue
        ↓
    Approver notified
        ↓
    Severity assessed
        ↓
   ┌────┴────┐
   P2/P3     P0/P1
   ↓           ↓
Handle     Founder notified
locally         ↓
           War room activated
                ↓
           External help if needed
```

---

## Roles During Incident

| Role | Responsibilities |
|------|------------------|
| **Incident Lead** | Coordinates response, makes decisions |
| **Communications** | Updates stakeholders, drafts messages |
| **Technical** | Investigates, implements fixes |
| **Scribe** | Documents everything, maintains timeline |

---

## Communication Channels

| Audience | Channel | Frequency |
|----------|---------|-----------|
| Response team | Private group | Real-time |
| All members | Announcement channel | Major updates |
| Public | Social/website | After containment |

---

## Post-Incident Process

### Within 24 Hours
- [ ] Confirm incident fully resolved
- [ ] Remove any temporary mitigations
- [ ] Initial impact assessment

### Within 72 Hours
- [ ] Write incident report (see template below)
- [ ] Conduct blameless post-mortem
- [ ] Identify action items

### Within 1 Week
- [ ] Implement preventive measures
- [ ] Update documentation
- [ ] Share learnings

---

## Incident Report Template

```markdown
# Incident Report: [Title]

**Date:** YYYY-MM-DD
**Severity:** P[0-3]
**Duration:** [Start] - [End] (X hours)
**Lead:** @name

## Summary
One paragraph describing what happened.

## Timeline
- HH:MM - Event
- HH:MM - Event
- HH:MM - Event

## Impact
- Users affected: X
- Funds at risk: Y PT / Z ETH
- Functions unavailable: [list]

## Root Cause
What actually caused the incident.

## Resolution
How it was fixed.

## Lessons Learned
1. What we learned
2. Another lesson

## Action Items
| Action | Owner | Due | Status |
|--------|-------|-----|--------|
| Item 1 | @name | Date | Open |
| Item 2 | @name | Date | Open |
```

---

## Prevention Checklist

**Technical:**
- [ ] Multi-sig for critical functions
- [ ] Timelock on governance
- [ ] Regular security audits
- [ ] Monitoring and alerts
- [ ] Backup RPC endpoints

**Process:**
- [ ] Documented runbooks
- [ ] Regular incident drills
- [ ] Clear escalation paths
- [ ] Updated contact list

---

## Emergency Contacts

| Role | Contact | Backup |
|------|---------|--------|
| Founder | @Hudson | - |
| Technical Lead | [TBD] | [TBD] |
| Security | [TBD] | [TBD] |

---

## Quick Reference

**Mantra:** Contain → Communicate → Fix → Learn

**Golden Rules:**
1. Safety first - protect funds and users
2. Don't make it worse - test fixes before deploying
3. Communicate early - silence breeds fear
4. Document everything - future you will thank you
5. Blameless culture - focus on systems, not people

---

*Version 1.0 | ClawDAO Incident Response Guide | February 2026*
