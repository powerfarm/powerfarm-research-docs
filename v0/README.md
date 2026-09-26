# V0

The current materialization of the canon: what should exist now (**I**), what exists (**C**), and the plan from C to I.

| File | Contents |
|---|---|
| [V0-00_DELTA_AND_PLAN.md](V0-00_DELTA_AND_PLAN.md) | C, the delta, the plan, decisions and proofs |
| [V0-01_DATA_REGISTRY_IDENTITY_AND_STORES.md](V0-01_DATA_REGISTRY_IDENTITY_AND_STORES.md) | Target: Registry, act log, Identity, Content Store, Minivault, Antenna store, offices and autonomy, copies, where it lives on Supabase |
| [V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md](V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md) | Target: LABs, agents and their releases, Host Runners, Parks, onboarding, Coloured Places |
| [V0-03_REBUILD.md](V0-03_REBUILD.md) | Target: the story, the rebuild script, the Director's steps, the drill |
| [V0-06_POWERFARM_SEARCH.md](V0-06_POWERFARM_SEARCH.md) | Target: Search (deferred) |
| [V0-07_NAMES_AND_ADDRESSES.md](V0-07_NAMES_AND_ADDRESSES.md) | Target: names (`powerfarm.app/<type>/<name>`), hostnames, bytes |
| [registry-v0.yaml](registry-v0.yaml) | The target, machine-readable |

## Delta

```text
negative delta = C − I     remove, move, quarantine
positive delta = I − C     build, materialize, recognize
```

Dispositions: `DELETE`, `ARCHIVE_THEN_MOVE` (repositories), `KEEP_OUTSIDE_REGISTRY`, `QUARANTINE_OR_DECIDE`, `REPLACE`.

Rules:
- nothing is removed without the Director's approval; earlier test state is not archived;
- observation is evidence of C; it does not admit anything into I.

Converged when `C − I` holds only explicit exceptions, `I − C` is empty, the latest census matches the target, and the rebuild drill passes.

Changes are adopted by Director merge. The history of every document is in Git. No secrets, personal data or internal addresses in this folder.
