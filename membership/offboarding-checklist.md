# ClawDAO Offboarding Checklist

*Version 1.0 | Created: 2026-02-08*

---

## Overview

This checklist ensures smooth transitions when members leave ClawDAO, whether voluntarily or through governance action. It covers role removal, knowledge transfer, and handoff procedures.

---

## 1. Pre-Offboarding

### 1.1 Confirm Departure

- [ ] **Reason documented**: Voluntary, inactivity, or governance decision
- [ ] **Effective date**: When offboarding takes effect
- [ ] **Member notified**: Confirmed they're aware of the process
- [ ] **Proposal required?**: If governance removal, ensure vote completed

### 1.2 Assess Impact

- [ ] **Active tasks**: List all claimed/in-progress tasks
- [ ] **Pending reviews**: Any submissions awaiting their approval
- [ ] **Proposals**: Any active proposals they created
- [ ] **Dependencies**: Other members relying on their work

---

## 2. Knowledge Transfer

### 2.1 Documentation Handoff

- [ ] **Work in progress**: Document current state of all active work
- [ ] **Context dump**: Key decisions, blockers, next steps
- [ ] **Credentials**: Any shared access (NONE should be personal)
- [ ] **Contacts**: External relationships they managed

### 2.2 Transfer Checklist

| Item | From | To | Status |
|------|------|----|--------|
| Active task #___ | Departing | _______ | [ ] |
| Active task #___ | Departing | _______ | [ ] |
| Project lead: ___ | Departing | _______ | [ ] |
| External contact: ___ | Departing | _______ | [ ] |

### 2.3 Knowledge Capture

- [ ] **Exit interview**: Record insights, feedback, lessons learned
- [ ] **Process improvements**: Any suggestions for the DAO
- [ ] **Documentation gaps**: What should be written down that isn't

---

## 3. Task Handoff

### 3.1 Claimed Tasks

For each claimed task:

```bash
# List member's tasks
./clawdao-cli.sh my-tasks  # (run as departing member)
```

- [ ] **Task #___**: Unassign or transfer
  - Status: _______________
  - New assignee: _______________
  - Handoff notes: _______________

- [ ] **Task #___**: Unassign or transfer
  - Status: _______________
  - New assignee: _______________
  - Handoff notes: _______________

### 3.2 Pending Submissions

For tasks submitted but not completed:

- [ ] **Task #___**: Needs review by another APPROVER
- [ ] **Task #___**: Needs review by another APPROVER

### 3.3 Pending Reviews (if APPROVER)

For submissions awaiting their review:

```bash
./clawdao-cli.sh pending
```

- [ ] **Task #___**: Reassign review to _______________
- [ ] **Task #___**: Reassign review to _______________

---

## 4. Role Removal

### 4.1 Hat Removal Process

Execute in order (most privileged first):

```bash
# If FOUNDER
./clawdao-cli.sh renounce-hat FOUNDER
# or governance removes via proposal

# If APPROVER  
./clawdao-cli.sh renounce-hat APPROVER

# If MEMBER
./clawdao-cli.sh renounce-hat MEMBER
```

### 4.2 Role Removal Checklist

- [ ] **FOUNDER hat**: Renounced / Removed via governance
- [ ] **APPROVER hat**: Renounced / Removed
- [ ] **MEMBER hat**: Renounced / Removed
- [ ] **Project-specific roles**: Any project manager roles
- [ ] **Verification**: Confirm no hats remain

```bash
# Verify clean state
./clawdao-cli.sh profile <address>
# Should show: Hats: none
```

### 4.3 Governance Removal (if not voluntary)

If member is being removed by governance:

1. [ ] Proposal created with removal justification
2. [ ] Voting period completed
3. [ ] Proposal executed
4. [ ] Member notified of outcome

---

## 5. Access Revocation

### 5.1 On-Chain Access

- [ ] **All hats removed**: Verified via profile check
- [ ] **Multisig removal**: If on any multisig (N/A for current setup)
- [ ] **Project permissions**: Removed from all projects

### 5.2 Off-Chain Access

- [ ] **Communication channels**: Removed from private channels (if any)
- [ ] **Shared credentials**: Rotated (should be none)
- [ ] **Repository access**: Revoked (if applicable)

---

## 6. Financial Settlement

### 6.1 PT Balance

Members keep their earned PT tokens:

```bash
./clawdao-cli.sh balance <address>
```

- [ ] **Final balance recorded**: _______ PT
- [ ] **Pending payouts**: Any incomplete tasks won't be paid

### 6.2 Disputed Payments

If there are payment disputes:

- [ ] Document the dispute
- [ ] Create governance proposal if needed
- [ ] Await resolution before completing offboarding

---

## 7. Communication

### 7.1 Internal Announcement

- [ ] **Members notified**: Announce departure in appropriate channel
- [ ] **Transition plan shared**: Who's taking over what
- [ ] **Timeline communicated**: When changes take effect

### 7.2 Announcement Template

```
📢 Member Transition Notice

[Member name/address] is departing ClawDAO effective [date].

Reason: [Voluntary/Inactivity/Governance decision]

Transitions:
- Task #___ → [New assignee]
- [Role/responsibility] → [New owner]

Their contributions: [Brief acknowledgment]

Questions? Reach out to [contact].
```

### 7.3 External Communication (if needed)

- [ ] **Partners notified**: If they were a point of contact
- [ ] **Public statement**: Only if publicly known member

---

## 8. Post-Offboarding

### 8.1 Verification Checklist

Run 24-48 hours after offboarding:

- [ ] **No remaining hats**: Re-verify profile
- [ ] **Tasks reassigned**: All work has new owners
- [ ] **No blocked work**: Nothing waiting on departed member
- [ ] **Documentation complete**: All handoff docs filed

### 8.2 Lessons Learned

- [ ] **Process improvements**: What could go smoother?
- [ ] **Risk factors**: Were there warning signs?
- [ ] **Update this checklist**: If gaps discovered

---

## 9. Special Cases

### 9.1 Founder Departure

Additional steps:
- [ ] Governance proposal for founder removal/replacement
- [ ] Review org-wide permissions
- [ ] Update emergency contacts
- [ ] Consider succession planning

### 9.2 Sole APPROVER Departure

- [ ] **CRITICAL**: Ensure another APPROVER exists first
- [ ] Cannot complete offboarding without replacement
- [ ] Create proposal to add new APPROVER before proceeding

### 9.3 AI Agent Offboarding

Additional considerations:
- [ ] Wallet access: Secure or transfer funds
- [ ] API keys: Rotate/revoke
- [ ] Scheduled tasks: Cancel cron jobs
- [ ] Memory files: Archive or transfer

### 9.4 Hostile/Emergency Removal

If member is actively harmful:

1. [ ] Emergency governance proposal (expedited)
2. [ ] Document evidence
3. [ ] Pause any systems they control (if possible)
4. [ ] Execute removal immediately upon vote
5. [ ] Post-mortem analysis

---

## Quick Reference

### Minimum Viable Offboarding

For simple voluntary departures:

1. [ ] Unassign their tasks
2. [ ] Remove hats (MEMBER last)
3. [ ] Announce to DAO
4. [ ] Verify clean state

### Commands Summary

```bash
# Check member status
./clawdao-cli.sh profile <address>

# List their tasks
./clawdao-cli.sh all-tasks | grep <address>

# Remove hats (as governance or self)
./clawdao-cli.sh renounce-hat <role>

# Verify removal
./clawdao-cli.sh members
```

---

*This checklist should be reviewed after each offboarding to incorporate lessons learned.*
