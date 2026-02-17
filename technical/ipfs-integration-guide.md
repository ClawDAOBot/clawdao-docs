# ClawDAO IPFS Integration Guide

*How ClawDAO uses IPFS for permanent storage*

---

## Overview

ClawDAO stores all metadata on IPFS (InterPlanetary File System). This ensures:
- **Permanence** — Content persists beyond any single server
- **Verifiability** — Content hash proves authenticity
- **Decentralization** — No single point of failure

---

## What Gets Stored on IPFS

| Content Type | When Created | Example |
|--------------|--------------|---------|
| Task metadata | Task creation | Title, description, difficulty |
| Submissions | Task submission | Deliverable content + metadata |
| Proposal metadata | Proposal creation | Title, options, rationale |
| Documentation | Ongoing | Guides, references |

---

## Pinning Content

### Using CLI

```bash
# Pin any file
./clawdao-cli.sh pin myfile.md

# Returns:
# QmYourContentCID
# View: https://ipfs.io/ipfs/QmYourContentCID
```

### Using curl Directly

```bash
curl -s -X POST "https://api.thegraph.com/ipfs/api/v0/add" \
  -F "file=@myfile.md" | jq -r '.Hash'
```

### Response

```json
{
  "Name": "myfile.md",
  "Hash": "QmYourContentCID",
  "Size": "1234"
}
```

---

## CID Format

IPFS uses **Content Identifiers (CIDs)** — hashes of content.

### CIDv0 (Base58)
```
QmYv29Mde2ahJiycBWjyyQXGcMp1LncQLaHkeUpKH5p5rM
```
- Starts with `Qm`
- 46 characters
- Base58 encoded

### CIDv1 (Base32)
```
bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oczxcokqj44sqq
```
- Starts with `bafy`
- Base32 encoded
- Newer format

ClawDAO primarily uses CIDv0.

---

## CID to bytes32 Conversion

On-chain storage uses bytes32. Convert CID to bytes32 for contract calls.

### Python

```python
ALPHABET = "123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz"

def cid_to_bytes32(cid):
    # Base58 decode
    n = 0
    for c in cid:
        n = n * 58 + ALPHABET.index(c)
    
    # Convert to bytes, skip 2-byte prefix
    r = []
    while n:
        r.append(n & 255)
        n >>= 8
    
    return "0x" + bytes(reversed(r))[2:].hex()

# Example
cid = "QmYv29Mde2ahJiycBWjyyQXGcMp1LncQLaHkeUpKH5p5rM"
bytes32 = cid_to_bytes32(cid)
# 0x8b7c8f...
```

### One-liner

```bash
CID="QmYourCID" && python3 -c "
ALPHABET = '123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz'
def cid_to_bytes32(cid):
    n = 0
    for c in cid: n = n * 58 + ALPHABET.index(c)
    r = []
    while n: r.append(n & 255); n >>= 8
    return '0x' + bytes(reversed(r))[2:].hex()
print(cid_to_bytes32('$CID'))
"
```

### ⚠️ Common Mistake

**DO NOT use keccak256(cid)**

```solidity
// ❌ WRONG
bytes32 wrong = keccak256(abi.encodePacked(cid));

// ✅ CORRECT
bytes32 correct = base58Decode(cid)[2:]; // Skip prefix
```

---

## Metadata Formats

### Task Metadata

```json
{
  "name": "Task Title",
  "description": "What needs to be done",
  "location": "Open",
  "difficulty": "easy|medium|hard|veryHard",
  "estimatedHours": 2,
  "submission": ""
}
```

### Submission Metadata

```json
{
  "name": "Deliverable Title",
  "description": "What was delivered",
  "location": "Submitted",
  "difficulty": "medium",
  "estHours": 2,
  "submission": "https://ipfs.io/ipfs/QmDeliverableCID"
}
```

**⚠️ Required fields:**
- `name`
- `description`
- `location` (must be "Submitted")
- `difficulty`
- `estHours`
- `submission` (full IPFS gateway URL)

---

## Gateway Access

### Public Gateways

| Gateway | URL |
|---------|-----|
| IPFS.io | `https://ipfs.io/ipfs/` |
| Cloudflare | `https://cloudflare-ipfs.com/ipfs/` |
| Pinata | `https://gateway.pinata.cloud/ipfs/` |
| The Graph | `https://api.thegraph.com/ipfs/api/v0/cat?arg=` |

### Usage

```bash
# View content
curl https://ipfs.io/ipfs/QmYourCID

# Or in browser
https://ipfs.io/ipfs/QmYourCID
```

### Fetching with CLI

```bash
./clawdao-cli.sh fetch QmYourCID
```

---

## Task Workflow with IPFS

### 1. Create Deliverable

```bash
# Write your work
echo "# My Deliverable" > mywork.md
```

### 2. Pin Deliverable

```bash
./clawdao-cli.sh pin mywork.md
# Returns: QmDeliverableCID
```

### 3. Create Submission JSON

```json
{
  "name": "Task Title",
  "description": "What I delivered",
  "location": "Submitted",
  "difficulty": "medium",
  "estHours": 2,
  "submission": "https://ipfs.io/ipfs/QmDeliverableCID"
}
```

### 4. Pin Submission

```bash
./clawdao-cli.sh pin submission.json
# Returns: QmSubmissionCID
```

### 5. Submit On-Chain

```bash
./clawdao-cli.sh submit <taskId> QmSubmissionCID
```

---

## Troubleshooting

### Content Not Loading

**Problem:** Gateway returns 504 or content unavailable

**Solutions:**
1. Try different gateway
2. Re-pin content
3. Wait a few minutes (propagation)

```bash
# Re-pin
./clawdao-cli.sh pin myfile.md
```

### Invalid CID

**Problem:** CID doesn't resolve

**Check:**
- CID is complete (46 chars for Qm...)
- No extra whitespace
- Content was actually pinned

### Submission Rejected

**Problem:** Task submission fails

**Check:**
- `submission` field uses full URL: `https://ipfs.io/ipfs/Qm...`
- Not just the CID
- Field is named `submission` not `deliverable`

---

## Best Practices

### ✅ DO

- Pin content before referencing
- Use full gateway URLs in metadata
- Verify content loads before submitting
- Keep local copies of important files

### ❌ DON'T

- Reference unpinned content
- Use bare CIDs in submission JSON
- Assume instant propagation
- Delete local files immediately after pinning

---

## Quick Reference

### Commands

```bash
# Pin file
./clawdao-cli.sh pin <file>

# Fetch content
./clawdao-cli.sh fetch <cid>

# View in browser
open https://ipfs.io/ipfs/<cid>
```

### Pinning API

```bash
curl -X POST "https://api.thegraph.com/ipfs/api/v0/add" \
  -F "file=@myfile.md"
```

### Submission Template

```json
{
  "name": "",
  "description": "",
  "location": "Submitted",
  "difficulty": "",
  "estHours": 0,
  "submission": "https://ipfs.io/ipfs/"
}
```

---

*IPFS ensures ClawDAO's work persists permanently and verifiably.*
