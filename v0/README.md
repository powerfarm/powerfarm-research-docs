# V0

Current materialization of the canon: what should exist now (**I**), what exists (**C**), and the plan from C to I.

| File | Contents |
|---|---|
| [V0-00_DELTA_AND_PLAN.md](V0-00_DELTA_AND_PLAN.md) | C, delta, plan, decisions, proofs |
| [V0-01_DATA_REGISTRY_IDENTITY_AND_STORES.md](V0-01_DATA_REGISTRY_IDENTITY_AND_STORES.md) | Target: Registry, Identity, Content Store, Minivault, Antenna store, offices and autonomy |
| [V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md](V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md) | Target: LABs, agents, Host Runners, Parks, onboarding, Places |
| [V0-06_POWERFARM_SEARCH.md](V0-06_POWERFARM_SEARCH.md) | Target: Search |
| [registry-v0.yaml](registry-v0.yaml) | Target, machine-readable |
| [history/](history/) | Executed tranches and superseded notes |

## Delta

```text
negative delta = C − I     remove, archive, move, quarantine
positive delta = I − C     build, materialize, recognize
```

Dispositions: `DELETE`, `ARCHIVE_THEN_DELETE`, `ARCHIVE_THEN_MOVE`, `KEEP_OUTSIDE_REGISTRY`, `QUARANTINE_OR_DECIDE`, `REPLACE`.

Rules:
- nothing is removed before custody is verified;
- observation is evidence of C; it does not admit anything into I.

Converged when `C − I` holds only explicit exceptions, `I − C` is empty, and the latest census matches the target.

Changes are adopted by Director merge. No secrets, personal data or internal addresses in this folder.
