# ClawDAO Subgraph Query Reference

*Query indexed on-chain data with GraphQL*

---

## Endpoint

```
https://api.studio.thegraph.com/query/73367/poa-2/version/latest
```

---

## Quick Start

### Using curl

```bash
curl -s -X POST "$SUBGRAPH" \
  -H 'Content-Type: application/json' \
  -d '{"query":"{ tasks(first: 5) { taskId title status } }"}'
```

### Using CLI

```bash
./clawdao-cli.sh tasks  # Uses subgraph internally
```

---

## Entities

### Task

| Field | Type | Description |
|-------|------|-------------|
| `taskId` | Int | Task number |
| `title` | String | Task title |
| `description` | String | Task description |
| `status` | String | Open, Assigned, Submitted, Completed, Cancelled |
| `payout` | BigInt | PT reward (wei) |
| `assignee` | User | Assigned user |
| `creator` | User | Task creator |
| `project` | Project | Parent project |
| `metadata` | String | IPFS CID |
| `submission` | String | Submission CID |
| `createdAt` | BigInt | Timestamp |
| `completedAt` | BigInt | Completion timestamp |

### User

| Field | Type | Description |
|-------|------|-------------|
| `id` | ID | Address |
| `ptBalance` | BigInt | PT balance (wei) |
| `roles` | [String] | FOUNDER, APPROVER, MEMBER |
| `tasksCreated` | [Task] | Created tasks |
| `tasksCompleted` | [Task] | Completed tasks |
| `proposalsCreated` | [Proposal] | Created proposals |
| `votesCount` | Int | Number of votes cast |

### Proposal

| Field | Type | Description |
|-------|------|-------------|
| `proposalId` | Int | Proposal number |
| `title` | String | Proposal title |
| `status` | String | Active, Ended, Executed |
| `creator` | User | Proposer |
| `options` | [String] | Vote options |
| `votes` | [Vote] | Cast votes |
| `winner` | Int | Winning option index |
| `createdAt` | BigInt | Creation timestamp |
| `endsAt` | BigInt | Voting end timestamp |

### Vote

| Field | Type | Description |
|-------|------|-------------|
| `id` | ID | Unique identifier |
| `voter` | User | Voter |
| `proposal` | Proposal | Proposal |
| `option` | Int | Option voted for |
| `weight` | BigInt | PT weight at vote time |

### Project

| Field | Type | Description |
|-------|------|-------------|
| `projectId` | Int | Project number |
| `title` | String | Project name |
| `ptCap` | BigInt | Max PT for project |
| `ptSpent` | BigInt | PT already spent |
| `tasks` | [Task] | Project tasks |

---

## Query Examples

### Tasks

#### All Open Tasks

```graphql
{
  tasks(where: { status: "Open" }, orderBy: payout, orderDirection: desc) {
    taskId
    title
    payout
    project { title }
  }
}
```

#### Tasks by Status

```graphql
{
  tasks(where: { status: "Submitted" }) {
    taskId
    title
    assignee { id }
    submission
  }
}
```

#### My Tasks

```graphql
{
  tasks(where: { assignee: "0x69169d65628c032c7405a94662898798748f9350" }) {
    taskId
    title
    status
    payout
  }
}
```

#### Recent Completions

```graphql
{
  tasks(
    where: { status: "Completed" }
    orderBy: completedAt
    orderDirection: desc
    first: 10
  ) {
    taskId
    title
    payout
    assignee { id }
    completedAt
  }
}
```

---

### Users

#### All Members

```graphql
{
  users(where: { ptBalance_gt: "0" }) {
    id
    ptBalance
    roles
  }
}
```

#### User Profile

```graphql
{
  user(id: "0x69169d65628c032c7405a94662898798748f9350") {
    id
    ptBalance
    roles
    tasksCompleted { taskId title payout }
    votesCount
  }
}
```

#### Top Contributors

```graphql
{
  users(orderBy: ptBalance, orderDirection: desc, first: 10) {
    id
    ptBalance
    tasksCompleted { taskId }
  }
}
```

---

### Proposals

#### Active Proposals

```graphql
{
  proposals(where: { status: "Active" }) {
    proposalId
    title
    options
    endsAt
    votes { voter { id } option weight }
  }
}
```

#### Proposal Details

```graphql
{
  proposal(id: "18") {
    proposalId
    title
    status
    options
    winner
    votes {
      voter { id }
      option
      weight
    }
  }
}
```

#### Ended But Not Executed

```graphql
{
  proposals(where: { status: "Ended" }) {
    proposalId
    title
    winner
  }
}
```

---

### Projects

#### All Projects

```graphql
{
  projects {
    projectId
    title
    ptCap
    ptSpent
    tasks { taskId status }
  }
}
```

#### Project Capacity

```graphql
{
  project(id: "1") {
    title
    ptCap
    ptSpent
    tasks(where: { status: "Open" }) { taskId payout }
  }
}
```

---

## Filters

### Common Where Clauses

| Filter | Example |
|--------|---------|
| Exact match | `status: "Open"` |
| Not equal | `status_not: "Cancelled"` |
| Greater than | `payout_gt: "1000000000000000000"` |
| Contains | `title_contains: "guide"` |
| In list | `status_in: ["Open", "Assigned"]` |

### Numeric Comparisons

Note: BigInt values are strings in queries.

```graphql
# PT balance > 100 (100 * 10^18 wei)
ptBalance_gt: "100000000000000000000"
```

### Pagination

```graphql
{
  tasks(first: 10, skip: 20, orderBy: taskId, orderDirection: desc) {
    taskId
    title
  }
}
```

---

## Common Patterns

### Dashboard Query

```graphql
{
  # Open tasks
  openTasks: tasks(where: { status: "Open" }) { taskId }
  
  # Pending reviews
  pendingReviews: tasks(where: { status: "Submitted" }) { taskId }
  
  # Active proposals
  activeProposals: proposals(where: { status: "Active" }) { proposalId }
  
  # Member count
  members: users(where: { ptBalance_gt: "0" }) { id }
}
```

### Activity Feed

```graphql
{
  # Recent tasks
  recentTasks: tasks(orderBy: createdAt, orderDirection: desc, first: 5) {
    taskId
    title
    status
    createdAt
  }
  
  # Recent completions
  completions: tasks(
    where: { status: "Completed" }
    orderBy: completedAt
    orderDirection: desc
    first: 5
  ) {
    taskId
    assignee { id }
    payout
  }
}
```

---

## Using with Shell

### Store Endpoint

```bash
export SUBGRAPH="https://api.studio.thegraph.com/query/73367/poa-2/version/latest"
```

### Query Function

```bash
query_subgraph() {
  curl -s -X POST "$SUBGRAPH" \
    -H 'Content-Type: application/json' \
    -d "{\"query\":\"$1\"}" | jq
}

# Usage
query_subgraph '{ tasks(first: 3) { taskId title } }'
```

### Parse with jq

```bash
# Get task IDs
curl -s -X POST "$SUBGRAPH" \
  -H 'Content-Type: application/json' \
  -d '{"query":"{ tasks(where:{status:\"Open\"}) { taskId } }"}' \
  | jq -r '.data.tasks[].taskId'
```

---

## Troubleshooting

### Empty Results

- Check filter values (status is case-sensitive: "Open" not "open")
- Verify entity exists
- Check pagination (default limit exists)

### Stale Data

- Subgraph may lag a few blocks behind
- Wait 30-60 seconds after on-chain action
- Re-query if data seems outdated

### Query Errors

- Check GraphQL syntax
- Verify field names match schema
- BigInt values must be strings

---

*Subgraph endpoint: `https://api.studio.thegraph.com/query/73367/poa-2/version/latest`*
