# V0-03 — Rebuild: the Story and the Script

**Status:** WORKING V0
**Canon:** PF-03 §3.3 ("Everything institutional is rebuildable") and PF-03 §16, rule 16

> **Anything Powerfarm cannot rebuild from what it has preserved, it does not really have.**

Installing Powerfarm and rebuilding Powerfarm are the same thing: running its story. This document defines the story, the script that runs it, the steps that belong to the Director, and the drill that proves it works.

---

## 1. What is rebuilt, and from what

| state | rebuilt from | proved by |
|---|---|---|
| **Institutional:** Registry, Identity structure, Content Store catalog, Minivault recognitions, canon documents | the **act log** (V0-01 §6.1) replayed over the **Content Store bytes** | the hash chain verifies; names, counts and digests match |
| **Schema:** tables, rules, API functions | migrations in `powerfarm/minivault`, each sealed by hash in a lock file | the applied migrations match the lock |
| **Code:** Minivault kernel, API, agents, Coloured Places | Git repositories at recorded commits | builds and tests pass |
| **Provider configuration:** Auth settings and hooks, OAuth server, bucket, Edge Functions, schedules, hostnames | script steps (§4) | reading the configuration back gives what was declared |
| **Operational:** Antenna store, agent queues | the owner's copy (V0-01 §9) | restored, or the loss is declared |
| **Secrets** | never restored: issued again by the Director from the references (V0-01 §2.10) | every reference is bound to a working value; no value appears anywhere in the rebuild |
| **Logins** | the person entities and admissions come back with the story; each person signs in again | the gates admit exactly the admitted people |

Private content (e-mail addresses in admissions, contract documents that are not public) lives in the Content Store, never in Git. The story refers to it by digest.

---

## 2. The story

**The story is the ordered sequence of Powerfarm's institutional acts.** Read from the beginning, it tells how the company came to be: which kinds of contract exist, which types of things, which offices, who holds them, what was recognized and when.

It exists in two forms:

| form | where | holds |
|---|---|---|
| **`story/`** | `powerfarm/minivault`, one file per act, in order | the acts of birth: the Foundation Act and the first chapters |
| **the act log** | the Identity substrate, exported nightly (V0-01 §9) | every act that has actually happened, hash-chained |

At birth, the script writes `story/` into the act log, one act at a time, through the API. After that, every new act (a contract recognized, an agent inscribed, a version published) is appended by the API. **A rebuild replays the act log.**

### 2.1 Chapters

| chapter | acts |
|---|---|
| **1. Identity** | the substrate answers; sign-in, gates and the OAuth server are configured |
| **2. Registry** | the Foundation Act: *Contract Type*, *Entity Type*, *Object Type*, *Action Type*, the contract types office and mandate, the entity type person, the Director's action types, the office `powerfarm.app/contract/director`, the first person, the mandate, the admission. Then the other types, the Engineer office and its matrix, machines, agents, Host Runners, stores, apps, services and secret references |
| **3. Minivault** | `powerfarm.app/app/minivault-web` and its store-authority contract; every Minivault kind recognized as an Object Type contract with its schema |
| **4. Research** | the book as a Research reference; the canon files as `powerfarm.app/document/*` versions |

No entity, contract or grant is ever created by a seed. The migration creates empty tables; the story fills them.

---

## 3. The script

`tools/rebuild` in `powerfarm/minivault` walks the chapters in order. It installs a new Powerfarm and rebuilds a lost one with the same steps.

### 3.1 Every step describes itself

| field | meaning |
|---|---|
| **says** | one sentence a person reads: what the step does and why |
| **needs** | earlier steps, and anything only the Director can give |
| **check** | read-only: is it already done, and done the same way? |
| **do** | the act, through the API or the provider's API |
| **verify** | proof that it worked |
| **receipt** | the act recorded in the act log |

### 3.2 Rules

1. A step that is already done the same way is skipped.
2. A step that was done differently stops the run and reports the difference.
3. A step that needs the Director waits and says exactly what is needed and where to click. The Director is never asked to type commands.
4. Every step leaves a receipt.
5. The script reads secrets only through their references and never prints, stores or copies a value.

Because every step describes itself, a guided onboarding interface can later present the same steps one by one. It adds a face, not a second procedure.

---

## 4. The steps

| # | step | who |
|---|---|---|
| 0 | **Substrate.** The provider project answers. The provider access token is created once by the Director in the provider's dashboard and kept in the LAB Keychain | script; the token is the Director's |
| 1 | **Clear the way.** Only when earlier state occupies the substrate: it is renamed out of the way and closed. Nothing is exported. Dropping it is the Director's | script; the drop is the Director's |
| 2 | **Schema.** Apply the migrations (empty tables, rules, functions; no rows), each checked against the lock | script |
| 3 | **Identity.** Passwordless sign-in, the two gates, the OAuth 2.1 server | script |
| 4 | **Content Store.** The insert-only bucket. On a rebuild, the bytes come back from the copy, each re-hashed against its name | script |
| 5 | **API.** Functions and Edge Functions deployed; `api.powerfarm.app` and `id.powerfarm.app` answer | script |
| 6 | **Foundation Act.** Act number 1. The Director signs up with the e-mail chosen at Foundation; the gate finds the admission, and the account is born bound to the person entity | script, then the Director |
| 7 | **Registry chapter.** At birth from `story/`; on a rebuild from the act log | script |
| 8 | **Minivault chapter.** Same | script |
| 9 | **Research chapter.** Same | script |
| 10 | **Secrets.** For each reference, in the recorded order, the Director issues a new value in the provider's dashboard; the script binds it and verifies it works | the Director, then the script |
| 11 | **Prove.** The checks of §6. The receipt is an act, and its content is in the Content Store | script |

---

## 5. What only the Director does

- Creates the provider access token (step 0).
- Signs up at the Foundation Act (step 6).
- Issues new secret values (step 10).
- Approves what the contracts gate, and drops earlier state (step 1).
- **Uses the offline signing key.** The Director's signing key lives on offline media in a safe. A step that needs it waits; the Director inserts the media, confirms, and removes it. The script never reads, copies or transmits the key, and no LLM ever sees it. Its public half is a recognized object, so anyone can verify what it signed.

---

## 6. The drill

The drill rebuilds Powerfarm into an empty project from the copies alone, and checks:

1. the act log's hash chain verifies from act 1 to the last act;
2. all content in the Content Store re-hashes to its name;
3. Registry names and counts match the source;
4. `may()` gives the same answers to a fixed set of questions;
5. Minivault's current versions match, digest for digest;
6. the applied migrations match the lock;
7. no secret value appears anywhere in the rebuilt project;
8. the receipt records what passed and any declared loss.

The drill runs at least once a month and after any material change to the script or the story. **A rebuild that has never been run is not a rebuild.**

---

## 7. Different worlds

A rebuild may land on a different provider, machine or substrate (PF-03 §3.3). Where a step's provider differs, an LLM may adapt that step as a proposal: a new adapter, a configuration for the new provider. The same checks verify it.

**The LLM may build anything a check verifies, and never anything that is the check.** The checks, the act log, the names, the digests and the Director's approvals are never written by an LLM. Steps adapted twice become ordinary steps of the script.
