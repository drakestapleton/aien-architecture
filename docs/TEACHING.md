# Learn from an architecture decision

At `b1d5fa3c20de8db277890d16d37b14c391196630`, this is a dated documentation snapshot. [`docs/02-implementation-status.md`](02-implementation-status.md) says its source review was 2026-09-23 and names a different code pin. Use the current [aien-dev architecture](https://github.com/aien-dev/aien-architecture-mv) and [aienix](https://github.com/aien-dev/aienix) for current navigation. This personal repository explains design intent; it does not ship a runtime.

One worked path: [ADR 0007](adr/0007-jspace-effect-boundary.md) chooses to keep external writes as intents during speculative J-Space exploration. [ADR 0005](adr/0005-effect-broker.md) then requires AEGIS authorization and an Effect Broker after winner selection. [The proposed flow](03-flows.md) draws that order. The September [implementation status](02-implementation-status.md) calls the Broker partial and J-Space a target. Thus the diagrams teach the intended boundary, while the current implementation and negative test must be checked in the active component repo at a named commit. Treat the claim of a safe external write as blocked here.

## Fresh checkout reading exercise (offline)

Prerequisites: Git and Python 3. Checkout `b1d5fa3c20de8db277890d16d37b14c391196630`, then run from repository root:

```sh
python3 - <<'PYEX'
from pathlib import Path
a=Path('docs/adr/0007-jspace-effect-boundary.md').read_text()
b=Path('docs/02-implementation-status.md').read_text()
assert 'EffectIntents' in a and '2026-09-23' in b
assert 'Effect Broker | 🟡' in b and 'J-Space | ⬜' in b
print('DECISION PRESENT; IMPLEMENTATION PARTIAL OR TARGET')
PYEX
```

Expected that line, exit 0. This checks the historical decision/status record, not effect enforcement. The negative case is assuming an architecture diagram proves a live denial; no runtime exists in this repository to test that. [Replay receipt](teaching-replay-2026-10-22.txt).
