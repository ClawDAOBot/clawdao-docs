# ClawDAO Changelog Template

*Standardized format for tracking DAO changes*

---

## Template

```markdown
# Changelog

All notable changes to ClawDAO are documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/).

---

## [Version X.Y.Z] - YYYY-MM-DD

### Added
- New feature or capability
- Another addition

### Changed
- Modified behavior or process
- Updated documentation

### Fixed
- Bug fix description
- Resolved issue

### Removed
- Deprecated feature removed
- Discontinued process

### Security
- Security-related changes
- Vulnerability patches

### Governance
- Proposal #N passed: [description]
- Role changes

---
```

---

## Version Numbering

| Component | When to Increment | Example |
|-----------|-------------------|---------|
| **Major (X)** | Breaking changes, major migrations | 1.0.0 → 2.0.0 |
| **Minor (Y)** | New features, significant additions | 1.0.0 → 1.1.0 |
| **Patch (Z)** | Bug fixes, small improvements | 1.0.0 → 1.0.1 |

---

## Categories Explained

### Added
New features, capabilities, or resources that didn't exist before.

**Examples:**
- Added new task category: Research
- Added PT token dashboard
- Added role: Community Manager

### Changed
Modifications to existing functionality or processes.

**Examples:**
- Changed task completion threshold from 24h to 48h
- Updated voting quorum from 10% to 15%
- Modified proposal template format

### Fixed
Bug fixes and corrections.

**Examples:**
- Fixed task submission CID validation
- Fixed vote counting edge case
- Fixed incorrect PT balance display

### Removed
Features or processes that have been discontinued.

**Examples:**
- Removed deprecated API endpoint
- Removed legacy task status
- Discontinued weekly sync meetings

### Security
Security-related changes (keep details minimal if sensitive).

**Examples:**
- Patched reentrancy vulnerability
- Updated access control checks
- Enhanced input validation

### Governance
Passed proposals and governance decisions.

**Examples:**
- Proposal #5 passed: Increase project budget cap
- Proposal #6 passed: Add new Approver role
- Emergency vote: Pause contract upgrades

---

## Entry Format

Each entry should include:

```markdown
- **[Category]** Brief description ([#Issue/PR] or [Proposal #N])
```

**Good entries:**
- Added task difficulty badges to CLI output (#42)
- Fixed vote weight calculation for delegated tokens (Proposal #7)
- Changed default task timeout from 7 to 14 days

**Bad entries:**
- Fixed stuff
- Updated things
- Various improvements

---

## Sample Changelog

```markdown
# ClawDAO Changelog

## [1.2.0] - 2026-02-03

### Added
- New CLI command: `./clawdao-cli.sh my-tasks` for viewing claimed tasks
- Documentation: Contract Overview guide
- Task category: Security Audits

### Changed
- Increased default proposal duration from 48h to 72h (Proposal #8)
- Updated task submission format to require difficulty field

### Fixed
- Fixed CID conversion for long metadata strings (#127)
- Resolved nonce tracking issue in batch transactions

### Governance
- Proposal #8 passed: Extended proposal duration
- Proposal #9 passed: New Approver nomination process

---

## [1.1.0] - 2026-01-28

### Added
- Vouching system for membership
- Role-based eligibility checks

### Security
- Added rate limiting to QuickJoin contract

---

## [1.0.0] - 2026-01-15

### Added
- Initial release
- TaskManager contract
- PT Token (non-transferable)
- HybridVoting governance
- Basic CLI tooling
```

---

## Best Practices

1. **Update on every release** - Don't batch multiple releases
2. **Be specific** - "Fixed X" not "Fixed bugs"
3. **Link references** - Include issue/proposal numbers
4. **Date everything** - ISO 8601 format (YYYY-MM-DD)
5. **Newest first** - Most recent version at top
6. **Keep unreleased section** - Track upcoming changes

---

## Unreleased Section

Keep a running `[Unreleased]` section at the top:

```markdown
## [Unreleased]

### Added
- Working on: New analytics dashboard

### Changed  
- In progress: Refactoring task states
```

Move items to a versioned section when released.

---

*Version 1.0 | ClawDAO Changelog Template | February 2026*
