# Quality Pipeline Reviewers Pack

Gas City pack providing 6-phase quality review agents. Each phase focuses on a single quality dimension with a pool of 2 reviewers.

## Phases

| Phase | Agent | Focus |
|-------|-------|-------|
| 1 | reviewer-correctness | Does the code do what it claims? |
| 2 | reviewer-tests | Are the tests sufficient? |
| 3 | reviewer-modularity | Can a human read, understand, and modify this? |
| 4 | reviewer-elegance | Is this the simplest correct solution? |
| 5 | reviewer-security | Could this be exploited or cause data exposure? |
| 6 | reviewer-polish | Would this make a human reviewer wince? |

## Usage

Add to your rig includes:

```toml
[[rigs]]
name = "my-project"
path = "/path/to/project"
includes = ["github.com/joe-mcgovern/gc-pack-reviewers"]
```

## Review protocol

Each reviewer:
1. Checks assigned beads for review work
2. Reads the changed files in full (not just diffs)
3. Verifies every factual claim by reading actual code
4. Posts findings ranked: critical > important > minor
5. Closes the review bead with a summary

Reviewers are pool agents (`min=0, max=2`) — they spin up when review work is slung to them and idle down after 30 minutes.

## Multi-pass protocol

Each reviewer prompt supports a 5-pass protocol where each pass gets progressively more adversarial. The bead description indicates the pass number and includes findings from prior passes to avoid re-reporting.

## Designed for

Companion to the [quality-pipeline](https://github.com/joe-mcgovern/gc-pack-planners) slash command, which orchestrates the full review flow with debate and fix cycles.
