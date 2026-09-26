# V0-00 — Delta and plan

**State as of:** 2026-09-26. **Owner:** Director. **Executed by:** engineers (LLM agents and sessions).

## 1. C — what exists (verified 2026-09-26)

| Area | State |
|---|---|
| LAB 8GB, LAB 512 | Home roots organized (4 fixed folders). AI-created services removed at user and system level. Remaining: Manhattan, remote-access tunnels, vendor apps |
| LAB 256 | Organized. Bench only: nothing depends on it |
| Agents | Eve 0.67 on all three LABs, running as the only authorized service (`app.powerfarm.agente`):<br>• signals every minute;<br>• inventory every 15 minutes;<br>• every conversation event copied;<br>• chat door accepts only short signed tokens;<br>• AI Gateway answers on all three;<br>• staged install with automatic rollback, proven |
| Agent identity | Registered as host runners in the legacy Registry: wrong, they are agents (`powerfarm.app/agent/*`) |
| Identity substrate | Holds the legacy Registry (15 entities, 0 contracts, 0 grants, bootstrapped without the V0-01 design) and a temporary observation schema. 0 auth users |
| Host Runner | Not materialized |
| Antenna service | Not running; its daemon is removed; source retained |
| Coloured Places | Legacy endpoint returns 502; Vercel copy returns 503 (unconfigured); blank Vercel project `powerfarm-places` created for the monorepo, not yet connected |
| Monorepo (Places + agent + contract + CI) | Published as `powerfarm/places` (public, 2026-09-26). On GitHub CI, everything passes except one agent test that inspects the real LAB and cannot pass on a CI runner |
| Search | Deferred. Airtable retired |
| The book | Kept (V0-01 §11) |
| Archive (LAB files) | 3,282 unique items (23.2 GB) in Google Drive, cloud upload in progress; being consolidated complete on LAB 512 |
| Google ADK | Not present |
| Minivault | Code in `powerfarm/minivault` (private, moved into the organization 2026-09-26): 71 of 77 tests pass, 5 skipped, 1 fixture bug. Built without the Registry; the surgery is planned. Not on the substrate |
| Names | The legacy Registry uses `pf.*` ids; V0-07 defines `powerfarm.app` names and hostnames |

## 2. Delta

### I − C (to build)

| # | Item | Target in |
|---|---|---|
| +1 | Registry rebuilt: migration without rows, institutional API, Foundation Act. Then the story: every contract and entity inscribed one act at a time by the rebuild script, never by a seed | V0-01 §2, §6 |
| +2 | Identity keyring: bindings, admissions, acceptances, sign-in gates | V0-01 §3 |
| +3 | Content Store: insert-only bucket, server-side SHA-256, manifests | V0-01 §4 |
| +4 | Antenna store (Neon) with Registry projection and the two views | V0-01 §7 |
| +5 | Agents renamed `powerfarm.app/agent/*` and writing to the Antenna store, one database role each | V0-01 §7–§8 |
| +6 | Coloured Places on Vercel: Registry authority, Antenna reads, live chat with approval cards | V0-02 |
| +7 | Tunnel hostname and access policy per agent for the chat | V0-02 |
| +8 | Engineer office with the autonomy matrix; precedent ledger read from agent events | V0-01 §2.8 |
| +9 | Host Runner per LAB | V0-02 |
| +10 | Experiment tickets with expiry; quarantine of services created outside the agent | V0-02 |
| +11 | Dependency discipline: single package store, shared build caches, clone dedupe, version policy | V0-02 |
| +12 | Minivault joins the Registry in `powerfarm/minivault`: the Registry is its authority, its kinds become Artifact Type contracts, one act log for every write. Then on the substrate, over the Content Store | V0-01 §5 |
| +13 | Google ADK in Engine Park, behind the Continuity compiler | V0-02 |
| +14 | Monorepo `powerfarm/places` published ✔. Remaining: protected main and an engineer identity | — |
| +15 | Rebuild by script: the story (institutional acts) replayed through the API into an empty project. Byte copies on LAB 8GB (monthly), snapshots in Google Drive; restore drill | — |
| +16 | Names and hostnames: `powerfarm.app/<type>/<name>`, `<service>.powerfarm.app` | V0-07 |

### C − I (to remove)

| # | Item | Disposition |
|---|---|---|
| −1 | Legacy Registry schema, and the frozen Airtable export in its bucket | `DELETE`, no archive: the rebuild script renames it out of the way and closes access; the Director drops it |
| −2 | Temporary observation schema in the substrate | `DELETE`, no archive, after +4 |
| −3 | Archived items on LAB 256 and LAB 8GB | `DELETE` (to Trash) after the Drive upload and the LAB 512 consolidation are verified; items in use stay |
| −4 | Legacy Places endpoint and unconfigured Vercel copy | `REPLACE` by +6 |
| −5 | Old Antenna path folder at the LAB 8GB root | `QUARANTINE_OR_DECIDE` |
| −6 | Loose credential files on the bench | `QUARANTINE_OR_DECIDE`: rotate if exposed |
| −7 | Legacy `powerfarm-registry` source (preserved on LAB 8GB) | `KEEP_OUTSIDE_REGISTRY`: nothing migrates; the new Registry is born from the story |

## 3. Plan

| Wave | Steps | Exit |
|---|---|---|
| **0 Close** | finish the LAB 512 consolidation; after the upload, apply −3; rotate exposed credentials; start the coordination log | Drive and LAB 512 each hold the 3,282 items; −3 applied with receipts |
| **1 Identity** | −1; then +1, +2, +3 tested on a throwaway database; the rebuild script applies them, runs the Foundation Act (the Director signs in) and inscribes the story from `registry-v0.yaml` | a second Foundation Act fails; the Registry answers what is current without GitHub; the script rebuilds an empty project from the story |
| **2 Eyes** | +4, +5, +6, +7; −2, −4 | the Director sees every LAB from a phone, labeled against the Registry; a stopped principal falls back to the reserve |
| **3 Publish** | +14; one vocabulary (action types mapped to the eight authorities) | a PR by an engineer is merged or blocked by CI alone |
| **4 Engineer** | +8; three observe-only runs; approvals in Places | an operation outside the granted rung is refused by the platform |
| **5 No forest** | +9, +10, +11 on LAB 256 first, then 512 and 8GB | zero services outside agent, Host Runner, Manhattan, tunnels, vendors; disk does not grow from rebuildables |
| **6 Graphs** | +12, +13 | a recognized graph runs on ADK with traces carrying its content id |
| **7 Rebuild** | +15 | signed restore drill with the primary substrate and one LAB offline |
| **8 Installer** | LLM installer into a different provider setup | install passes; the second install needs less LLM effort |

## 4. Decisions

**Decided:**

| Decision | Value |
|---|---|
| The book | Kept |
| Offices | Director (owner); engineers = LLM agents; autonomy per V0-01 §2.8 |
| Admission | Director only |
| Archive (LAB files) | complete on LAB 512 and in Drive |
| Legacy test state | not archived; deleted by the Director |
| Names | V0-07: `powerfarm.app/<type>/<name>`; services `<service>.powerfarm.app`; bytes `sha256:<hex>` |
| Repositories | Registry + Minivault: `powerfarm/minivault`; agents + Places: `powerfarm/places` |
| Heartbeats | deterministic code, never a model |
| Byte copies | LAB 8GB (monthly) and Google Drive snapshots; Cloudflare R2 if cheap |
| Observation store | Neon, owned by `powerfarm.app/service/antenna`, Registry as an API projection |
| MCP door for external assistants | closed until the identity provider supports audience-bound tokens and public clients |
| Node | newest LTS |

**Open:**

| Decision | Recommendation |
|---|---|
| Initial rung per engineer operation class | OBSERVE or SUGGEST |
| Large bytes location | outside the Content Store; manifest inside |
| Exchange format for executable graphs | OWS 1.0.3 |
| Minivault content id | SHA-256 only, so the database can verify every write |
| Minivault revert | a new publication of the earlier bytes; history only moves forward |

## 5. Proofs

| Proof | Evidence | Wave |
|---|---|---|
| P0 Eyes | Places on a phone showing what exists × what is recognized | 2 |
| P1 Nothing lost | canon and archive in custody with verified digests | 0–1 |
| P2 One vocabulary | single term table; no collisions in the corpus | 3 |
| P3 Engineer loop | three digests; a refused out-of-rung action | 4 |
| P4 No forest | clean inventory on all LABs for a week | 5 |
| P5 Graph runs | bundle executed with traceable content id | 6 |
| P6 Rebuild | the script rebuilds an empty project from the story; signed receipt | 7 |
| P7 Installer | install in a different world with less effort each time | 8 |

## 6. Rules for engineers

1. Nothing destructive without the Director's approval, and never before custody is verified. Removal means the Trash.
2. Never modify the book.
3. No secret values anywhere: references only.
4. Never touch remote-access tunnels or protected processes.
5. No services except the agent (installed by its installer).
6. The Director does not run commands: engineers do.
7. Every claim carries its evidence; "done" means verified.
8. Outward actions (publishing, deploys, deletions of backups) need an explicit Director approval.
9. Names follow V0-07.
