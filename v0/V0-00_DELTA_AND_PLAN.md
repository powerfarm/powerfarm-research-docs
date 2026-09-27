# V0-00 — Delta and Plan

**State as of:** 2026-09-26
**Owner:** the Director
**Executed by:** engineers (LLM agents and sessions)

What exists (**C**), what the target adds (**I − C**), what must go (**C − I**), and the plan from C to I. This is the only V0 document that describes the present. Rows leave it when they are done.

---

## 1. C — what exists (verified 2026-09-26)

| area | state |
|---|---|
| LAB 8GB, LAB 512 | Home folders organized (four fixed folders). Services created by AI tools removed. Remaining: Manhattan, remote-access tunnels, vendor apps |
| LAB 256 | Organized. The bench: nothing depends on it |
| Agents | Eve 0.67 on all three LABs, the only authorized service (`app.powerfarm.agente`):<br>• signals every minute and inventory every 15 minutes, by deterministic code;<br>• every conversation event copied;<br>• the chat door accepts only short signed tokens;<br>• the AI Gateway answers on all three;<br>• staged install with automatic rollback, proven |
| Agent names | Recorded as host runners in the current Registry; they are agents (`powerfarm.app/agent/*`) |
| Identity substrate | Supabase `powerfarm.kernal`, free plan (1 GB Storage, pauses after 7 quiet days). Holds a Registry made without the V0-01 design (15 entities, 0 contracts, 0 grants, `pf.*` names), a temporary observation schema, and one object in its bucket (a frozen Airtable export). 0 auth users |
| Identity host | `id.powerfarm.app` answers from the earlier Identity app (`powerfarm/powerfarm-identity`) |
| Host Runner | Not materialized |
| Antenna service | Not running; its daemon removed; source kept in `powerfarm/powerfarm-antenna` |
| Coloured Places | Code published as `powerfarm/places` (public) with the agents. Vercel project `powerfarm-places` exists, not yet connected; its keys are not yet in Vercel. GitHub CI passes except one agent test that inspects the real LAB and cannot pass on a CI runner |
| Minivault | Code in `powerfarm/minivault` (private): 71 of 77 tests pass, 5 need Postgres, 1 fixture bug. It keeps its own permissions and uses BLAKE3 ids; not on the substrate |
| Hostnames | `powerfarm.app` serves the workbench; `registry.`, `app.`, `portal.` and `api.` exist outside V0-07 or answer with errors |
| Search | Deferred |
| The book | Kept (V0-01 §11) |
| Archive of LAB files | 3,282 unique items (23.2 GB) uploading to Google Drive; being consolidated on LAB 512 |
| Google ADK | Not present |

---

## 2. Delta

### 2.1 I − C (to build)

| # | item | target |
|---|---|---|
| +1 | **Registry:** a migration without rows; the institutional API; the act log; the Foundation Act | V0-01 §2, §6 |
| +2 | **Identity:** bindings, admissions, acceptances; passwordless sign-in; the two gates; the OAuth 2.1 server | V0-01 §3 |
| +3 | **Content Store:** insert-only bucket, digest as key, server-side SHA-256, manifests, integrity sweep | V0-01 §4 |
| +4 | **The rebuild script and the story:** `tools/rebuild` and `story/` in `powerfarm/minivault`; the Identity, Registry, Minivault and Research chapters | V0-03 |
| +5 | **Minivault under the Registry:** the Registry as its authority; kinds as Object Type contracts; SHA-256 revision ids; undo as a new publication; on the substrate over the Content Store | V0-01 §5 |
| +6 | **Copies:** act log nightly and Content Store bytes on LAB 8GB; snapshots in Google Drive | V0-01 §9 |
| +7 | **External observer:** alive marks, a change-only e-mail, a weekly "still watching" | V0-01 §7.5 |
| +8 | **Antenna store** (Neon) with the Registry projection and the two views | V0-01 §7 |
| +9 | **Agents** named `powerfarm.app/agent/*`, writing to the Antenna store, one database role each | V0-01 §§7, 8 |
| +10 | **Coloured Places** at `places.powerfarm.app`: Registry authority, Antenna reads, live chat with approval cards | V0-02 |
| +11 | Tunnel hostname and access policy per agent for the chat | V0-02 |
| +12 | **Hostnames** of V0-07: the front door at `powerfarm.app`, `api.`, `vault.`; one passkey | V0-07 |
| +13 | **Engineer office** with the autonomy matrix; the precedent ledger read from agent events | V0-01 §2.8 |
| +14 | Protected `main` and an engineer identity on `powerfarm/places` and `powerfarm/minivault` | — |
| +15 | Host Runner per LAB | V0-02 |
| +16 | Experiment tickets with expiry; quarantine of services created outside the agent | V0-02 |
| +17 | Dependency discipline: one package store, shared build caches, clone deduplication, version policy | V0-02 |
| +18 | Google ADK in Engine Park, behind the Continuity compiler | V0-02 |
| +19 | **The drill:** a monthly rebuild into an empty project from the copies | V0-03 §6 |

### 2.2 C − I (to remove)

| # | item | disposition |
|---|---|---|
| −1 | The Registry made without the V0-01 design, and the frozen Airtable export in its bucket | `DELETE`, no archive: the rebuild script renames it out of the way and closes access; the Director drops it |
| −2 | The temporary observation schema in the substrate | `DELETE`, no archive, after +8 |
| −3 | Archived items on LAB 256 and LAB 8GB | `DELETE` (to the Trash) once the Drive upload and the LAB 512 consolidation are verified; items in use stay |
| −4 | The old Places endpoint and the unconfigured Vercel copy | `REPLACE` by +10 |
| −5 | Hostnames outside V0-07 (`registry.`, `app.`, `portal.`) | `DELETE` (DNS), after +12 |
| −6 | The old Antenna folder at the LAB 8GB root | `QUARANTINE_OR_DECIDE` |
| −7 | Loose credential files on the bench | `QUARANTINE_OR_DECIDE`; rotate if exposed |
| −8 | The earlier `powerfarm-registry` source on LAB 8GB | `KEEP_OUTSIDE_REGISTRY`; nothing migrates from it |
| −9 | Apple-first Registry test records in CloudKit | `DELETE`; CloudKit keeps only contract-owned app and engine databases |

---

## 3. Plan

| wave | steps | exit |
|---|---|---|
| **0 Close** | finish the LAB 512 consolidation; after the upload, −3; rotate exposed credentials | Drive and LAB 512 each hold the 3,282 items; −3 applied with receipts |
| **1 Identity and Registry** | +1, +2, +3 as migrations in `powerfarm/minivault`, tested on a throwaway Postgres; +4 with the Identity and Registry chapters; −1; the Director signs in at the Foundation Act | a second Foundation Act fails; the Registry answers what is current without GitHub; the script rebuilds an empty project from the act log |
| **2 Minivault and Research** | +5; the Minivault and Research chapters; +6; +7 | a program is published through the API, recognized as a version, and readable only when `may()` says so; the canon is recognized as `powerfarm.app/document/*` versions |
| **3 Eyes** | +8, +9, +10, +11, +12; −2, −4, −5 | the Director sees every LAB from a phone, labeled against the Registry; a stopped principal falls back to the reserve |
| **4 Engineer** | +13, +14; three observe-only runs; approvals in Places | an operation outside the granted rung is refused by the platform |
| **5 No forest** | +15, +16, +17 on LAB 256 first, then 512 and 8GB | zero services outside the agent, Host Runner, Manhattan, tunnels and vendors; disk does not grow from rebuildable folders |
| **6 Graphs** | +18 | a recognized graph runs on ADK, with traces carrying its content id |
| **7 Rebuild** | +19 | the drill passes with the primary substrate and one LAB offline |
| **8 Installer** | the LLM installer into a different provider setup (V0-03 §7) | the install passes; the second install needs less LLM work |

---

## 4. Decisions

**Decided:**

| decision | value |
|---|---|
| Rebuildable | a founding principle (PF-03 §3.3); story and script per V0-03 |
| Names | V0-07: `powerfarm.app/<type>/<name>`; services `<service>.powerfarm.app`; bytes `sha256:<hex>` |
| Fingerprint | SHA-256 only, Minivault revisions included |
| Undo in Minivault | a new publication of the earlier bytes; history only moves forward |
| Birth of institutional things | through acts only, never by seed |
| Earlier test state | not archived; dropped by the Director |
| Repositories | Registry + Minivault: `powerfarm/minivault`; agents + Places: `powerfarm/places` |
| Heartbeats | deterministic code, never a model |
| Copies | LAB 8GB and Google Drive; Cloudflare R2 if cheap |
| The book | kept |
| Offices | the Director (owner); engineers are LLM agents; autonomy per V0-01 §2.8 |
| Admission | the Director only |
| Observation store | Neon, owned by `powerfarm.app/service/antenna`, with the Registry as an API projection |
| MCP door | closed until the identity provider supports audience-bound tokens and public clients |
| Node | newest LTS |

**Open:**

| decision | recommendation |
|---|---|
| Initial rung per engineer operation class | OBSERVE or SUGGEST |
| Large bytes | outside the Content Store; a manifest inside |
| Exchange format for executable graphs | OWS 1.0.3 |
| Where the workbench lives, once `powerfarm.app` becomes the front door | to decide |
| Secret values sealed in the Content Store, opened only with the Director's key (today: references only, V0-01 §2.10) | to discuss |

---

## 5. Proofs

| proof | evidence | wave |
|---|---|---|
| P0 Nothing lost | the canon and the LAB archive in custody, with verified digests | 0–2 |
| P1 Born from the story | the Director signs in; the Registry reads as the story; a second Foundation Act fails | 1 |
| P2 Meaning under authority | a Minivault program published and read only through `may()` | 2 |
| P3 Eyes | Places on a phone showing what exists × what is recognized | 3 |
| P4 Engineer loop | three observe-only runs; a refused out-of-rung action | 4 |
| P5 No forest | a clean inventory on all LABs for a week | 5 |
| P6 Graph runs | a bundle executed with a traceable content id | 6 |
| P7 Rebuild | the drill's receipt (V0-03 §6) | 7 |
| P8 Installer | an install in a different world, with less effort each time | 8 |

---

## 6. Rules for engineers

1. Nothing destructive without the Director's approval. Removal means the Trash.
2. Never modify the book.
3. No secret values anywhere: references only.
4. Never touch remote-access tunnels or protected processes.
5. No services except the agent, installed by its installer.
6. The Director does not run commands; engineers do, and tell the Director where to click when a step is the Director's.
7. Every claim carries its evidence. "Done" means verified.
8. Outward actions (publishing, deploys, deletions) need the Director's explicit approval.
9. Institutional things are born only through acts (V0-03). Names follow V0-07.
