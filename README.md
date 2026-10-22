<!-- github-native-navigation -->
[Source](https://github.com/drakestapleton/aien-architecture) · [Walkthrough](docs/TEACHING.md) · [Replay receipt](docs/teaching-replay-2026-10-22.txt)
<!-- /github-native-navigation -->

# AIEN Architecture

## How it works and how to reproduce

I trace one actual source or design boundary in [the worked lesson](docs/TEACHING.md), with a pinned fresh-checkout exercise and [raw replay receipt](docs/teaching-replay-2026-10-22.txt). The lesson states what remains unimplemented or unverified at this revision.

Dated personal architecture snapshot of flows, boundaries, decisions, research notes and roadmap. For current cross-project navigation, use [aien-dev/aien-architecture-mv](https://github.com/aien-dev/aien-architecture-mv) and [AienOS](https://github.com/aien-dev/aienix).

This repository is intentionally **documentation-first**. It does not replace the implementation repositories. It defines how the pieces are intended to compose and gives implementation agents one place to answer:

- What owns this responsibility?
- What talks to what?
- What is already implemented?
- What is partial?
- What is missing?
- Which boundary is security-critical?
- Which repository contains the current implementation?
- Which planned subsystem should be built next?

> **Naming rule:** physical hosts are always called **Machine 1**, **Machine 2**, **Machine 3**, and so on. Hardware/vendor details are capabilities, never architectural identities.

## Start here

1. [Language](CONTEXT.md)
2. [Complete system architecture](AIEN_COMPLETE_SYSTEM_ARCHITECTURE.md)
3. [System map](docs/00-system-map.md)
4. [GitHub repository map](docs/01-github-repository-map.md)
5. [Implementation status](docs/02-implementation-status.md)
6. [Flows](docs/03-flows.md)
7. [Capabilities, skills, tools, and MCP](docs/04-capabilities-skills-tools-mcp.md)
8. [Fabric and portable compute](docs/05-fabric-and-compute.md)
9. [J-Space](docs/06-jspace.md)
10. [Security, AEGIS, vault, and effects](docs/07-security-effects-secrets.md)
11. [World, Cortex, and provenance](docs/08-world-cortex-provenance.md)
12. [RSI and evaluation](docs/09-rsi-evaluation.md)
13. [PEARL-inspired relational path engine](docs/10-relational-path-engine.md)
14. [Gap analysis](docs/11-gap-analysis.md)
15. [Roadmap](docs/12-roadmap.md)
16. [Golden path](docs/13-golden-path.md)
17. [Architecture decision records](docs/adr/README.md)
18. [Master architectural plan](docs/14-master-architectural-plan.md)

## One-line architecture

```text
User/API
  → Runtime
  → J-Space
  → Skill Router
  → Capability Graph
  → Fabric placement
  → Model/Tool execution
  → AEGIS
  → Effect Broker
  → World Commit
  → Signed Provenance
  → Cortex
  → RSI feedback
```

## Master diagram

```mermaid
flowchart TD
    U[User / Operator / API] --> CP[Control Plane]
    CP --> RT[AIEN Runtime]

    RT --> JS[J-Space]
    JS --> SR[Skill Router]
    SR --> CG[Capability Graph]

    CG --> NT[Native Tools]
    CG --> MCP[MCP Broker]
    CG --> FT[Fabric Tools]

    RT --> INF[Inference Runtime]
    INF --> MR[Model Router]
    MR --> FAB[AIEN Fabric]

    FAB --> M1[Machine 1]
    FAB --> M2[Machine 2]
    FAB --> M3[Machine 3]
    FAB --> MN[Machine N]

    JS --> W[World Store]
    RT --> CX[Cortex]
    CX --> RT

    NT --> A[AEGIS]
    MCP --> A
    FT --> A

    A --> EB[Effect Broker]
    EB --> EXT[External World]
    EB --> W

    W --> P[Signed Provenance]
    P --> CX

    RT --> RSI[RSI Optimizer]
    RSI --> EV[Harness / Inquisitor / Benchmarks]
    EV --> RT
```

## Source-of-truth policy

This repository describes **intended architecture** and records resolved architecture decisions.

Implementation truth remains the current code in the linked repositories. When this repository and running code disagree:

1. Do not silently pretend the target is implemented.
2. Mark the discrepancy in [implementation status](docs/02-implementation-status.md).
3. Open an architecture-gap issue.
4. Update the relevant ADR when the intended design changes.

## Repository role

This repo should become the architectural index linked from the top-level READMEs of major AIEN repositories. Code repositories should avoid re-explaining the entire system; they should link here for cross-system architecture and keep their own README focused on their component.

## License

The AIEN ecosystem currently uses more than one license across repositories. Before publishing this architecture repository, copy or explicitly select the intended canonical documentation license rather than assuming one. See [LICENSE-NOTICE.md](LICENSE-NOTICE.md).
