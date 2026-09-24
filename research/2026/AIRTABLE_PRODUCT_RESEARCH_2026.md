# Airtable Product Research for Powerfarm Search — September 2026

**Status:** RESEARCH, not canon  
**Derived from:** `POWERFARM_SEARCH_SPEC v0.1` by Kimi plus validation against current Airtable documentation on 24 September 2026.  
**Purpose:** preserve dated vendor/product research without confusing Airtable implementation facts with Powerfarm architecture.

## Research conclusion

Airtable is attractive as the human projection for Powerfarm Search because it combines:

- a mature relational/table surface;
- Interface Designer;
- a usable native iOS application;
- search, quick/tab filters, dashboards, record detail and AI surfaces;
- a programmable API suitable for rebuilding a disposable projection.

None of those properties make Airtable authoritative.

The durable architectural conclusion is:

```text
authoritative sources
        ↓
Powerfarm Search read model
        ↓
Airtable projection
```

Airtable may be replaced without changing an institutional fact.

## Claims validated against current Airtable documentation

### API limits

Current Airtable documentation states:

- 5 API requests/second per base;
- 50 requests/second across traffic using one user/service-account token;
- batch create/update supports up to 10 records/request;
- after a per-base 429, Airtable documents a 30-second wait before requests succeed again.

These are vendor limits, not Powerfarm invariants. Connectors must read current provider limits rather than canonizing the numbers.

### Automation limits

Current Airtable documentation states:

- up to 50 automations/base;
- up to 25 actions/automation.

Again, these are capacity facts, not architecture.

### iOS interface constraints

Current Airtable mobile documentation supports these interface layouts on iOS:

- List
- Kanban
- Calendar
- Gallery
- Record overview/detail
- Overview/Homepage
- Dashboard
- Form
- Grid
- Navigation
- Record review / Inbox in current interface surfaces

Current mobile documentation does not support:

- Timeline
- Swimlanes/Roadmap
- Blank layouts
- legacy Record Review

iOS also currently lacks end-user grouping and general end-user filtering/sorting, while search and quick/tab filters are supported.

Therefore mobile-critical Powerfarm Search views should ship required slices instead of expecting ad-hoc user filtering.

### Mobile performance

Airtable warns that its mobile applications may slow or fail to load with tens of thousands of records.

The original draft's proposed 10k working-set target is therefore a reasonable engineering hypothesis, but **not** an Airtable-documented hard limit.

## Important 2026 documentation ambiguity

Airtable's own current help pages are not perfectly consistent on all mobile actions.

For example, one mobile-interface support page currently marks External URL buttons unsupported in record-detail/query-container contexts, while the broader desktop/mobile feature matrix marks some External URL actions supported on iOS.

Therefore Powerfarm MUST test mobile-critical behavior on a physical iPhone before relying on it.

Provider documentation ambiguity is evidence for a test requirement, not a reason to choose one page as permanent truth.

## Useful design hypotheses from the Kimi research

The following are good design proposals but remain Powerfarm decisions, not Airtable facts:

- semantic-key upsert instead of Airtable record IDs;
- payload digests for change detection;
- closed-world connector field maps;
- schema-as-data rather than one Airtable table per source table;
- connector snapshots and sync events;
- curated mobile working sets;
- source-side exclusion of sensitive fields;
- backfill as the rebuild mechanism;
- one connector/gatekeeper per source.

These may be adopted in V0 only where they solve an actual Powerfarm need.

## Ideas not adopted by this research note

The Kimi draft explored possible Search sources including:

- GitHub;
- Cloudflare telemetry.

That exploration does **not** make those sources part of V0.

The currently recognized V0 sources are defined by `V0-06_POWERFARM_SEARCH.md`.

Likewise, proposed domain tables, lint engines, drift observatories, AI-generated summaries, Omni usage, interface count, plan tier and third-party sync products are implementation/product hypotheses until explicitly adopted.

## Research methodology rule

For vendor-dependent behavior:

1. date the observation;
2. preserve the vendor source;
3. classify it as current provider behavior, not canon;
4. prefer executable acceptance tests for behavior that matters;
5. re-check before implementation if the observation is older than the implementation work.

## Sources checked 24 September 2026

- Airtable Help Center — Mobile interfaces in Airtable
- Airtable Help Center — Airtable desktop and mobile feature differences
- Airtable Help Center — Managing API call limits in Airtable
- Airtable Help Center — Getting started with Airtable automations
- Airtable Help Center — Interface Designer / layout documentation

The original Kimi proposal remains useful as the richer exploration from which this research note was distilled.
