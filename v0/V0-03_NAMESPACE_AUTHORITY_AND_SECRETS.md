# V0-03 - Namespace, Authority and Secrets

**Status:** WORKING V0  
**Recognition baseline:** `6438c55a20e82e922322d26561487f91761a6e3a`  
**Scope:** stable names, authority, secret references and approvals.

## Stable identity

Powerfarm names identify institutional things, not temporary provider objects, filesystem paths or database rows.

Preferred forms include:

```text
pf.<system>
pf.lab.<name>
pf.app.<name>
pf.engine.<name>
pf.repo.<name>
pf.store.<name>
pf.search-source.<name>
pf.secret.<name>
pf.contract.<name>
```

Existing recognized PFIDs remain valid. V0 does not rename identities merely for cosmetic consistency.

Provider identities are bindings to Powerfarm identities:

```text
Powerfarm principal / store / repo
          ↓ binding
Apple · GitHub · Supabase · machine credential · OAuth subject
```

Replacing a provider must not require redefining the institutional thing.

## Authority

Physical possession is not authority.

Powerfarm derives authority from recognized relationships such as:

- principals;
- grants;
- contracts;
- recognized artifact/repository versions;
- placement declarations;
- explicit approval evidence where required.

Human, machine, application and agent principals remain distinguishable.

At minimum V0 expects:

- Director/human principal;
- LAB machine principals;
- Host Runner principals;
- application/service principals;
- agent principals where an agent may act institutionally.

Grants are scoped and revocable. Network access, account possession, filesystem ownership or Park placement never implies permission.

## Secrets

The Registry stores secret **references and metadata**, never live credential values.

A material secret reference should identify:

- stable secret id;
- owner;
- provider/system;
- allowed consumers;
- storage substrate/location reference;
- rotation policy;
- revocation path;
- last verification date;
- replacement/migration state.

Live secret values MUST NOT enter:

- public Git history;
- Registry rows;
- Airtable/Search projections;
- receipts;
- ordinary content-addressed archives.

The current protected local secret source under `~/.powerfarm/secrets` on LAB 8GB is bootstrap state, not a final V0 secrets architecture.

Cleanup may record loose credentials by **name and location only**. Rotation precedes deletion when exposure is possible.

## Approval

Consequential effects require explicit authorization under the governing contract, including destructive machine change, grant issuance and adoption of Ideal Registry V0.

Where practical, approval binds to the exact immutable plan/effect. A materially changed plan requires new approval.

## Exit criteria

V0 authority is coherent when:

1. every admitted actor has a principal or explicit provider binding;
2. every material privilege is explainable through a grant/contract;
3. secret references are stable and provider-replaceable;
4. no live secret value exists in public Git, Registry, Airtable, Search, receipts or ordinary immutable archives.
