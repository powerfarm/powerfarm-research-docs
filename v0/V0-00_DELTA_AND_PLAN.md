# V0-00 — Delta and plan

**State as of:** 2026-09-26. **Owner:** Director. **Executed by:** engineers (LLM agents and sessions).

## 1. C — what exists (verified 2026-09-26)

| Area | State |
|---|---|
| LAB 8GB, LAB 512 | Home roots organized (4 fixed folders). AI-created services removed at user and system level. Remaining: Manhattan, remote-access tunnels, vendor apps |
| LAB 256 | Organized. Bench only: nothing depends on it |
| Agents | Eve 0.67 on all three LABs, running as the only authorized service (`app.powerfarm.agente`):<br>• signals every minute;<br>• inventory every 15 minutes;<br>• every conversation event copied;<br>• chat door accepts only short signed tokens;<br>• AI Gateway answers on all three;<br>• staged install with automatic rollback, proven |
| Agent identity | Registered as `pf.host-runner.*` in the legacy Registry: wrong, they are agents |
| Identity substrate | Holds the legacy Registry (15 entities, 0 contracts, 0 grants, bootstrapped without the V0-01 design) and a temporary observation schema. 0 auth users |
| Host Runner | Not materialized |
| Antenna service | Not running; its daemon is removed; source retained |
| Coloured Places | Legacy endpoint returns 502; Vercel copy returns 503 (unconfigured); blank Vercel project `powerfarm-places` created for the monorepo |
| Monorepo (Places + agent + contract + CI) | Local only; CI passes (house rules, types, tests, database tests, builds for 3 machines) |
| Search | Airtable, single projection table |
| The book | Kept (V0-01 §11) |
| Archive | 3,282 unique items (23.2 GB) in Google Drive, cloud upload in progress; being consolidated complete on LAB 512 |
| Google ADK, Minivault on the substrate | Not present |

## 2. Delta

### I − C (to build)

| # | Item | Target in |
|---|---|---|
| +1 | Registry rebuilt: migration without rows, institutional API, Foundation Act | V0-01 §2, §6 |
| +2 | Identity keyring: bindings, admissions, acceptances, sign-in gates | V0-01 §3 |
| +3 | Content Store: insert-only bucket, server-side SHA-256, manifests | V0-01 §4 |
| +4 | Antenna store (Neon) with Registry projection and the two views | V0-01 §7 |
| +5 | Agents renamed `pf.agent.*` and writing to the Antenna store, one database role each | V0-01 §7–§8 |
| +6 | Coloured Places on Vercel: Registry authority, Antenna reads, live chat with approval cards | V0-02 |
| +7 | Tunnel hostname and access policy per agent for the chat | V0-02 |
| +8 | Engineer office with the autonomy matrix; precedent ledger read from agent events | V0-01 §2.8 |
| +9 | Host Runner per LAB | V0-02 |
| +10 | Experiment tickets with expiry; quarantine of services created outside the agent | V0-02 |
| +11 | Dependency discipline: single package store, shared build caches, clone dedupe, version policy | V0-02 |
| +12 | Minivault on the substrate, over the Content Store | V0-01 §5 |
| +13 | Google ADK in Engine Park, behind the Continuity compiler | V0-02 |
| +14 | Monorepo published (private) with protected main and an engineer identity | — |
| +15 | Rebuild: signed genesis manifest, second failure domain, restore drill | — |
| +16 | Frozen Airtable Registry export recognized as the first Content Store object | V0-01 §4 |

### C − I (to remove)

| # | Item | Disposition |
|---|---|---|
| −1 | Legacy Registry schema | `ARCHIVE_THEN_DELETE`: export, rename, close access; the Director deletes |
| −2 | Temporary observation schema in the substrate | `ARCHIVE_THEN_DELETE` after +4 |
| −3 | Archived items on LAB 256 and LAB 8GB | `DELETE` (to Trash) after the Drive upload and the LAB 512 consolidation are verified; items in use stay |
| −4 | Legacy Places endpoint and unconfigured Vercel copy | `REPLACE` by +6 |
| −5 | Old Antenna path folder at the LAB 8GB root | `QUARANTINE_OR_DECIDE` |
| −6 | Loose credential files on the bench | `QUARANTINE_OR_DECIDE`: rotate if exposed |
| −7 | Legacy `powerfarm-registry` source (preserved on LAB 8GB) | `KEEP_OUTSIDE_REGISTRY`: migration input only; runs and workspace drafts do not migrate |

## 3. Plan

| Wave | Steps | Exit |
|---|---|---|
| **0 Close** | finish the LAB 512 consolidation; after the upload, apply −3; rotate exposed credentials; start the coordination log | Drive and LAB 512 each hold the 3,282 items; −3 applied with receipts |
| **1 Identity** | +1, +2, +3, tested on a throwaway database; apply; Foundation Act; Director signs in; inscriptions from `registry-v0.yaml` | a second Foundation Act fails; the Registry answers what is current without GitHub |
| **2 Eyes** | +4, +5, +6, +7; −1, −2, −4 | the Director sees every LAB from a phone, labeled against the Registry; a stopped principal falls back to the reserve |
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
| Archive | complete on LAB 512 and in Drive |
| Observation store | Neon, owned by `pf.antenna`, Registry as an API projection |
| MCP door for external assistants | closed until the identity provider supports audience-bound tokens and public clients |
| Node | newest LTS |

**Open:**

| Decision | Recommendation |
|---|---|
| Publish the monorepo (+14) | private, protected main |
| Initial rung per engineer operation class | OBSERVE or SUGGEST |
| Large bytes location | outside the Content Store; manifest inside |
| Off-machine backup destination | to decide |
| Exchange format for executable graphs | OWS 1.0.3 |

## 5. Proofs

| Proof | Evidence | Wave |
|---|---|---|
| P0 Eyes | Places on a phone showing what exists × what is recognized | 2 |
| P1 Nothing lost | canon and archive in custody with verified digests | 0–1 |
| P2 One vocabulary | single term table; no collisions in the corpus | 3 |
| P3 Engineer loop | three digests; a refused out-of-rung action | 4 |
| P4 No forest | clean inventory on all LABs for a week | 5 |
| P5 Graph runs | bundle executed with traceable content id | 6 |
| P6 Rebuild | signed drill receipt | 7 |
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
