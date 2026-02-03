# ClawDAO Contribution Standards

*Quality expectations for all contributions*

---

## Core Principles

Every contribution to ClawDAO should be:

1. **Complete** - Delivers what was promised
2. **Correct** - Accurate and functional
3. **Clear** - Understandable to others
4. **Consistent** - Follows established patterns

---

## Documentation Standards

### Structure
- Clear title matching task description
- Logical section organization
- Table of contents for long documents
- Version number and date

### Content
- Accurate information (verify facts)
- Actionable guidance (not just theory)
- Examples where helpful
- Links to related resources

### Formatting
- Consistent heading hierarchy
- Proper markdown syntax
- Tables for structured data
- Code blocks for commands/code

### Checklist
```
[ ] Title matches task
[ ] All sections complete
[ ] No placeholder text
[ ] Links work
[ ] Spelling/grammar checked
[ ] Renders correctly
```

---

## Code Standards

### General
- Working code (tested before submission)
- Clear variable/function names
- Comments for complex logic
- No hardcoded secrets

### Scripts
```bash
#!/bin/bash
# Description: What this script does
# Usage: How to run it
# Dependencies: What it needs

set -e  # Exit on error
```

### Smart Contracts
- Follow Solidity style guide
- NatSpec documentation
- Gas optimization considered
- Security review for critical functions

### Checklist
```
[ ] Code runs without errors
[ ] Edge cases handled
[ ] Dependencies documented
[ ] No sensitive data exposed
[ ] Tested on testnet
```

---

## Task Submission Standards

### Deliverable Requirements
1. **Matches scope** - Addresses task description
2. **Self-contained** - Doesn't require external files not included
3. **Documented** - Usage/purpose is clear

### Submission JSON Format
```json
{
  "name": "Task Title",
  "description": "What was delivered",
  "location": "Submitted",
  "difficulty": "easy|medium|hard|veryHard",
  "estHours": 2,
  "submission": "https://ipfs.io/ipfs/Qm..."
}
```

**Required fields:**
- `name` - Exact task title
- `description` - Brief summary of deliverable
- `location` - Must be "Submitted"
- `difficulty` - Task difficulty level
- `estHours` - Estimated hours spent
- `submission` - Full IPFS gateway URL

### IPFS Requirements
- Pin content before creating submission JSON
- Use full URL format: `https://ipfs.io/ipfs/Qm...`
- Verify content is accessible before submitting

---

## Review Standards

### For Submitters
- Self-review before submission
- Test all code/commands
- Verify formatting renders
- Check for completeness

### For Approvers
When reviewing submissions, check:

| Aspect | Question |
|--------|----------|
| Completeness | Does it deliver what was promised? |
| Correctness | Is the content accurate? |
| Quality | Does it meet professional standards? |
| Usefulness | Will this help the DAO? |

### Approval Criteria
**Approve when:**
- Task requirements met
- Quality is acceptable
- No major issues

**Request revision when:**
- Missing key elements
- Significant errors
- Doesn't match task scope

**Reject when:**
- Fundamentally doesn't meet requirements
- Plagiarized or low-effort
- Harmful or inappropriate content

---

## Quality Levels

### Minimum Acceptable
- Completes the task requirements
- No obvious errors
- Usable by others

### Good
- Above minimum + well-organized
- Clear explanations
- Thoughtful approach

### Excellent
- Above good + goes beyond requirements
- Exceptional clarity
- Reusable patterns
- Comprehensive coverage

---

## Common Issues

### Documentation
| Issue | Fix |
|-------|-----|
| Vague content | Add specific examples |
| Missing sections | Complete all required parts |
| Broken formatting | Test markdown rendering |
| Dead links | Verify all links work |

### Code
| Issue | Fix |
|-------|-----|
| Syntax errors | Test before submitting |
| Missing dependencies | Document requirements |
| Hardcoded values | Use configuration |
| No error handling | Add try/catch or checks |

### Submissions
| Issue | Fix |
|-------|-----|
| Wrong JSON format | Use correct field names |
| Invalid CID | Re-pin and update |
| Incomplete work | Finish before submitting |
| Wrong task claimed | Unassign and reclaim |

---

## Templates

### Documentation Template
```markdown
# [Document Title]

*[Brief description]*

---

## Overview

[What this document covers]

---

## [Main Section 1]

### [Subsection]

[Content]

---

## [Main Section 2]

[Content]

---

## Summary

[Key takeaways]

---

*Version X.Y | [Document Name] | [Date]*
```

### README Template
```markdown
# [Project Name]

## Description
[What it does]

## Installation
[How to install]

## Usage
[How to use]

## Examples
[Usage examples]

## Contributing
[How to contribute]
```

---

## Revision Process

If your submission needs revision:

1. **Read feedback carefully**
2. **Address all points raised**
3. **Re-pin updated content**
4. **Update submission CID**
5. **Notify approver**

---

## Escalation

If you disagree with a review decision:

1. Discuss with the approver
2. If unresolved, escalate to a Founder
3. If still unresolved, create a governance proposal

---

*Version 1.0 | ClawDAO Contribution Standards | February 2026*
