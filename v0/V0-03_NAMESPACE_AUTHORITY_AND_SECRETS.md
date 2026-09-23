# V0-03 - Namespace, Authority and Secrets

**Status:** PROPOSED until merged to `main`  
**Scope:** identity, naming, authority and secret-reference rules for V0.

## Namespace

Powerfarm institutional identities use stable semantic names. Names identify the thing; they do not encode a temporary filesystem path, provider account or database row id.

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

Existing stable PFIDs remain valid where already recognized. V0 should not rename an identity merely to make spelling prettier.

## Authority

Physical possession is not authority.

Authority is derived from recognized identities and explicit relationships, including:

- principals;
- grants;
- contracts;
- recognized artifact versions;
- placement/topology declarations;
- approval evidence where required.

V0 adopts the rule:

> grants are revocable, scoped authority; apps and agents do not infer permission from being able to reach a service.

Human, machine, application and agent identities remain distinguishable.

## Principals

V0 expects at least these principal classes:

- Director / human principal;
- LAB machine principals;
- Host Runner principals;
- application/service principals;
- agent principals where an agent can act institutionally.

A provider identity such as Apple, GitHub, Supabase or an OAuth subject is a binding to a Powerfarm principal, not the principal itself.

## Secrets

This public repository MUST NEVER contain live secret values.

The Registry records only secret metadata/references, for example:

```yaml
id: pf.secret.supabase.service-role
owner: pf.identity
consumers:
  - pf.app.host-runner
provider: supabase
location_ref: <non-secret locator>
rotation: on-compromise-or-policy
sensitivity: credential
```

The exact secret value belongs in an adopted secrets substrate or platform keychain, never in Git history, Airtable projection, Search indexes, receipts or content-addressed archives.

## Secret lifecycle

Each material secret should have:

- stable secret id;
- owner;
- provider/system;
- allowed consumers;
- storage substrate;
- creation/rotation policy;
- revocation path;
- last verification date;
- replacement/migration state.

The V0 cleanup delta may identify loose credentials by **name/location only**. Rotation precedes deletion when compromise or historical exposure is possible.

## Current bootstrap note

LAB 8GB currently has a protected local secret source organized under `~/.powerfarm/secrets`. This is bootstrap state, not the final V0 secrets architecture.

Its presence is not a license to copy secret material into this repository or into the Registry.

## Provider bindings

Provider-specific identities remain bindings:

- Apple/CloudKit account identity -> Powerfarm principal binding;
- GitHub account/app identity -> Powerfarm principal binding;
- Supabase Auth/service identity -> Powerfarm principal binding;
- machine certificates/tokens -> machine/service principal binding.

Changing provider credentials should not require renaming the institutional principal.

## Approval

Destructive machine change, grant issuance, adoption of Ideal Registry V0 and other consequential effect changes require explicit authorization according to the adopted contract.

Approvals bind to the exact proposed effect or immutable plan/version where practical. A materially changed plan requires new approval.

## V0 exit criteria

1. Every admitted app/machine/agent that can act has a principal or justified binding.
2. Every material privilege is explainable through a grant/contract.
3. No live secret value exists in public Git, Airtable, Search or content-addressed archives.
4. Secret references are stable enough that implementation providers can be replaced without rewriting application identity.
