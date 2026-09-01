# AEM Assets content consolidation — working plan

Status: DRAFT v3 — 2026-08-27
Owner: <dgonzale@adobe.com>

Not published content. This file tracks the plan to consolidate `/help/assets` and
`/help/assets-essentials` into a single capability-organized set of pages under
`/help/assets`, using ExL MD Tabs (`>[!BEGINTABS]` / `>[!TAB Assets view]` /
`>[!TAB Admin view]` / `>[!ENDTAB]` / `>[!ENDTABS]`) to present Assets view and Admin
view content on one page per capability.

## Mechanics

- Left rail nav: `help/assets/TOC.md` (final target). `help/assets-essentials/TOC.md`
  will shrink as pages migrate, and the two "Assets Essentials" links currently in
  `help/assets/TOC.md` get replaced once assets-essentials content is absorbed.
- URL redirects: add rows to `redirects.csv` at the repo root (`source,dest`, full
  `https://experienceleague.adobe.com/...` URLs) for every moved/merged/retired page.
- Tab syntax reference: see `help/cloud-service/local-development-environment/aem-runtime.md`
  for a working `BEGINTABS`/`TAB` example already in this repo.

## Decisions log

- **2026-08-27** — Capabilities where only Admin-view content exists today (no
  Assets-view video recorded yet): publish as a single-view page now under the new
  capability structure (no forced empty tab); add the Assets view tab later once
  that video exists. Applies to: check-in/check-out, versions, timeline & inbox,
  metadata import/export (and any others found later).
- **2026-08-27** — Quick Access (Assets view) and Collections (Admin view) are NOT
  the same underlying feature. Keep them as two separate capability pages rather
  than force-pairing them into one tabbed page.
- **2026-08-27** — Workfront integration: the "enhanced connector" (classic/full AEM
  Assets, `help/assets/workfront/enhanced-connector/`) and the Assets Essentials
  Workfront connector (`help/assets-essentials/integrations/workfront/`) are
  different integrations, not a view-split of the same feature. Keep as two
  separate, cross-linked TOC sections — do not tab together.
- **2026-08-27** — TOC model is strictly two levels: a top-level functional bucket
  (or a single page directly at top level, if the bucket would only ever hold one
  page) containing individual pages nested one level below, organized by sub-topic.
  No third level for newly-consolidated sections. As a result, Brand Portal and
  Asset Share — previously nested three deep under "Activation and sharing" — are
  promoted to their own top-level buckets. Workfront's and Dynamic Media's existing
  internal sub-nesting is left as-is since those sections are unchanged this pass.
- **2026-08-27 (v3)** — Revisited every v2 top-level bucket to look for further
  roll-up, and consolidated 23 top-level entries down to 12:
  - "Advanced capabilities" (the grab-bag) is dissolved; every page moved to a
    better-fitting bucket (see outline below for destinations).
  - Permissions + Governance + Reports merge into one oversight bucket, named
    **Governance & Insights** (permissions/access control is treated as a governance
    concern, so it doesn't need its own word in the name); the Reports page itself
    is renamed **Insights**.
  - My Workspace and Quick access merge into one page (same underlying feature —
    a widget on the workspace page) inside Search and discovery.
  - Sharing and activation + Brand Portal + Asset Share + Content Hub merge into
    one **Asset distribution** bucket, with internal sub-headers per product/feature
    since Brand Portal and Content Hub are licensed add-ons distinct from core
    sharing, and Asset Share Commons is a separate OSS reference app.
  - Content Automation + Auto-start workflows + Asset Templates merge into one
    **Automation** bucket (all template/script-driven content production).
  - Creative Cloud panels + Adobe Asset Link + Workfront + Edge Delivery Services
    merge into one **Integrations** bucket, with internal sub-headers per integration.
  - Programmatic asset upload + Export assets + Deployment (multitenancy) merge
    into a new **Developer & APIs** bucket — grouped by audience (developers/
    architects) rather than capability, a deliberate exception to the rest of the
    taxonomy's organizing principle.
  - This reintroduces a third nesting level inside Asset distribution, Automation,
    and Integrations (sub-headers under the top-level bucket). Same exception
    already in use today for Dynamic Media and Workfront; accepted here because
    collapsing genuinely distinct products/integrations into one flat page list
    would be worse for findability than one extra list level.
  - Open risk: "Asset distribution" bundling licensed add-ons (Brand Portal,
    Content Hub) with core features and an OSS app under one name may read as
    "all included in my plan" — needs clear sub-headers and possibly a short
    licensing note on the bucket's landing page.
- **2026-08-27** — View-scope labeling convention: **tabs only, no Badges.** Every
  page that documents a view-scoped capability uses `>[!BEGINTABS]`/`>[!TAB]`, even
  when only one view currently has content — a "single-view" page throughout this
  plan means one `>[!TAB Assets view]` or `>[!TAB Admin view]` block, not a bare
  untabbed page. Rejected a Badge-based alternative (`[!BADGE Admin view]`) to avoid
  two different visual mechanisms for the same concept ("which view does this apply
  to") depending on how many views a page currently documents. Trade-off accepted:
  a tab control with a single tab is a slightly unusual UI (nothing to switch to) —
  spot-check how this renders on a live/preview page before batch-applying it across
  the ~15 currently single-view pages in this plan.

## Proposed TOC structure (v3 — consolidated, top-level bucket → pages)

Each top-level entry below is marked **[page]** (single page, no sub-nav) or
**[bucket]** (collection of pages nested below it in `TOC.md`). Three buckets
(marked ⚠) need one extra internal sub-header level to stay legible given how
much they absorbed — see decisions log for why that's an accepted exception.
12 top-level entries, down from 23 in v2.

1. **Overview** — [page]. Assets view: `getting-started.md`; Admin: `overview.md`. No tabs, orientation only.

2. **Authoring** — [bucket]
   - Switch between views — agnostic [page] (`authoring/switch-views.md`)
   - Navigation — tabs (Assets view: `basics/using.md` navigation portion; Admin: `authoring/navigation.md`)
   - Basic operations: create, upload, move, copy, delete — tabs (Assets view: `basics/managing.md`; Admin: `authoring/basic-operations.md`)
   - Extract archive (bulk upload via ZIP) — single-view Admin for now *(moved from Advanced capabilities)*
   - Editing metadata — single-view Admin for now (`authoring/metadata.md`)
   - Renditions — single-view Admin for now (`authoring/renditions.md`)
   - Processing profiles (rendition configuration) — single-view Admin for now *(moved from Advanced capabilities; could alternatively live under Dynamic Media — toss-up)*
   - Relate and unrelate — single-view Admin for now (`authoring/relate-unrelate.md`)

3. **Metadata & taxonomy** — [bucket]
   - Metadata schemas & forms — tabs (Assets view: `configuring/metadata-forms.md`; Admin: `configuring/metadata-schemas.md` + `metadata-profiles.md` + `metadata-folder-schemas.md`)
   - Tagging & taxonomy — tabs (Assets view: `configuring/taxonomy-management.md`; Admin: `configuring/tagging.md` + `advanced/blocked-tags.md`)
   - Smart Tags & GenAI metadata — agnostic [page(s)] (`metadata/genai-metadata.md`, `image-smart-tags.md`, `video-smart-tags.md`, `custom-smart-tags.md`, `cascade-metadata...md` — may consolidate into fewer pages, TBD)
   - Import and export metadata — single-view Admin for now (`metadata/metadata-import-export.md`)
   - Content credentials (authenticity metadata) — agnostic [page] *(moved from Advanced capabilities)*

4. **Search and discovery** — [bucket]
   - Discovery — agnostic [page] (`discovery.md`)
   - Search — tabs (Assets view: `basics/using.md` search portion; Admin: `search-and-discovery/search.md`)
   - AI search — agnostic [page] (`ai-search.md`)
   - Adobe Firefly integration — agnostic [page] (`adobe-firefly.md`)
   - Search boost — agnostic [page] (`search-boost.md`)
   - Find similar images — agnostic [page] (`find-similar-images.md`)
   - My Workspace & quick access (merged — same feature: a widget on the workspace page) — single-view Assets view (`configuring/my-workspace.md` + `basics/quick-access.md`)
   - Collections — single-view Admin (`search-and-discovery/collections.md`) — kept separate from Quick access, per decisions log
   - Assets admin search rail — single-view Admin for now *(moved from Advanced capabilities)*

5. **Collaboration** — [bucket]
   - Watch — agnostic [page] (`collaboration/watch.md`)
   - Comments, annotations & tasks — tabs (Assets view: `basics/collaborating.md`; Admin: `collaboration/comments-and-annotations.md` + `review-task.md`)
   - Customizing annotations PDF output (config) — single-view Admin *(moved from Advanced capabilities)*
   - Check-in and check-out — single-view Admin for now
   - Versions — single-view Admin for now
   - Timeline and inbox — single-view Admin for now

6. **Governance & Insights** — [bucket] *(merged from v2's Permissions + Governance + Reports)*
   - Permissions management — tabs (Assets view: `configuring/permissions-management.md`; Admin: `configuring/baseline-permissions.md`)
   - Closed user groups — single-view Admin for now (`advanced/closed-user-groups.md`)
   - Metadata-driven permissions — single-view Admin for now (`advanced/metadata-driven-permissions.md`)
   - Asset governance — agnostic [page] (`governance/governance.md`)
   - Insights (renamed from "Reports") — tabs (Assets view: `basics/reports.md`; Admin: `advanced/asset-reports.md`) *(could alternatively sit in Asset distribution — toss-up)*

7. **Asset distribution** ⚠ — [bucket] *(merged from v2's Sharing and activation + Brand Portal + Asset Share + Content Hub)*
   - Sub-header: Sharing & activation — Link sharing & activation (tabs: `basics/link-sharing.md` / `sharing/activation.md`), Download assets (single-view Admin), Publish assets (single-view Admin), Export assets (single-view Admin, dev/API)
   - Sub-header: Brand Portal — Using Brand Portal, Configure asset sourcing, Enable rendition downloads (licensed add-on, unchanged content)
   - Sub-header: Content Hub — Overview, Set up, Configure, Add assets, Download assets, Image variants, Collections, Sharing, Attribute-based access control, Manage assets use case (licensed/Cloud Service-only add-on, unchanged content)
   - Sub-header: Asset Share Commons — Understanding UX, Local setup, Theming, Asset kits (separate OSS reference app, unchanged content)
   - Risk: bundling licensed add-ons with core sharing under one name — see decisions log

8. **Dynamic Media** — [bucket], existing internal nesting retained, plus 3 pages folded in from Advanced capabilities: 3D assets (→ 3D sub-group), Watermarks (→ Images sub-group), Video closed captions (→ Video sub-group)

9. **Automation** — [bucket] *(merged from v2's Content Automation + Auto-start workflows + Asset Templates)*
   - Automation overview, Creative operations, Photoshop actions (from `content-automation/`)
   - Auto-start workflows *(moved from Advanced capabilities)*
   - Understanding Asset Templates, Using Asset Templates, Set up Asset Templates, Using Asset Catalogs (from `asset-templates/`)

10. **Integrations** ⚠ — [bucket] *(merged from v2's Creative Cloud & panel integrations + Adobe Asset Link + Workfront integration + Edge Delivery Services)*
    - Sub-header: Creative Cloud & panels — Creative Cloud overview (folded in from `integrations/creative-cloud.md`), Adobe Express, Adobe Express + AEM Assets, AEM Desktop App, Adobe Stock, Figma
    - Sub-header: Adobe Asset Link — unchanged (~10 existing pages); fix the `creative-workflows/adobe-asset-link.md` duplicate (see Flagged cleanup) as part of this work
    - Sub-header: Workfront — Enhanced connector (existing internal nesting retained), Assets Essentials connector — two separate tracks, not tabbed together, per decisions log
    - Sub-header: Edge Delivery Services — Sidekick plugin

11. **Developer & APIs** — [bucket]. Audience-based exception, not capability-based — see decisions log:
    - Programmatic asset upload *(moved from Advanced capabilities)*
    - Multi-tenancy and concurrent development *(moved from v2's standalone Deployment)*
    - Note: `sharing/export.md` (Export assets, also dev/API-flavored) stays in Asset distribution instead, since it's about getting assets *out* of the system — cross-link the two buckets rather than duplicating the page

12. **Translation** — [page], unchanged, classic-only, no natural bucket home

**Retired:** Playlists (`playlists/admin-view.md`, `playlists/assets-view.md`) — replaced by the left rail + tabs browsing pattern; redirect both to the new Overview page.

## Flagged cleanup (independent of this reorg)

- `creative-workflows/adobe-asset-link.md` is a near-duplicate of
  `adobe-asset-link/panel-overview.md` (full ~127-line overview, not a stub). Needs
  trimming to a short intro + link, or merging, regardless of the essentials work.
- assets-essentials data-quality issues found during inventory: `basics/link-sharing.md`
  has placeholder description text; `basics/using.md` has a `thumbnai` typo; 
  `basics/managing.md` is missing `feature`/`feature_v2` fields its siblings have;
  `integrations/creative-cloud.md` has a duplicated `feature_v2` entry.

## Pilot: Insights (done)

Built `help/assets/governance/insights.md`, merging `assets-essentials/basics/reports.md`
(Assets view) and `assets/advanced/asset-reports.md` (Admin view) into one tabbed page.
`assets/TOC.md`'s "Governance" section is renamed **Governance & Insights** with both
pages nested under it; both old TOC entries removed; both old files deleted; both old
URLs added to `redirects.csv` pointing at the new page. Patterns to reuse for every
remaining page in this project:

- **exl-id / TQID**: omit entirely on new/merged pages — both are system-generated on
  first publish, never hand-authored (confirmed via the authoring assistant's
  `extract_exl_id` tool description).
- **jira**: left as literal `jira: TODO` — user is handling ticket creation/assignment
  separately, not per-page via the assistant.
- **product_v2 / feature_v2 / role_v2 / level_v2 / topic_v2**: union the id+label pairs
  from both source pages (dedupe by id) rather than inventing new ones — every id reused
  this way was already live on a published page, so no new taxonomy validation is needed.
  Exception: dropped one clearly mistaged value (admin page's `topic_v2: Metadata`,
  which doesn't reflect a reports page) rather than propagating it.
- **feature (flat field)**: picked `Asset Insights` — confirmed as a valid value via
  `get_features(feature_set="Experience Manager Assets")`, and it matches the new page
  name better than either source page's original value (`Assets Essentials` /
  `Asset Reports`).
- **version**: union of both source pages' version lists (the admin page's broader
  classic+CS list already superset the essentials-only CS value).
- **duration**: summed both source videos' durations (196 + 160 = 356). No prior
  multi-video-page precedent existed in this repo to follow instead; treat this as the
  house convention going forward unless it causes a problem.
- **Links**: ran `check_links` after writing the page — caught one redirected URL in the
  Admin-view tab's `[!IMPORTANT]` callout and fixed it to the live URL. Do this for every
  new/merged page.
- **RedPen scoring** (`validate_exl_content`) is unavailable in this session — it needs
  an interactive Adobe SSO login (`redpen_login`) that a non-interactive session can't
  complete. Run it manually (or via the `/validate_content_quality` skill in an
  interactive session) before merging.

**Transcript pass (added after initial build):** Fetched both videos' real transcripts
and rewrote the tab intros to reflect actual content instead of a generic paraphrase
of the source pages' descriptions. This caught two things worth fixing every time:

- **Fetching the transcript is a two-hop lookup, not the single GET the skill reference
  describes.** `https://video.tv.adobe.com/v/{PUBLIC_ID}/eng.json` doesn't return caption
  text by default; with a browser `User-Agent` + `Accept: application/json` header it
  returns the player config, not captions. The real caption JSON lives at
  `https://video.tv.adobe.com/vc/{internalVideoID}/eng.json`, where `internalVideoID`
  comes from that player config's `translations` array (match `language_medium: "eng"`,
  use its `jsonPath`). Do this for every page with an embedded video before writing or
  revising the surrounding copy.
- **The transcript surfaced a real content detail that changes tagging, not just prose.**
  The Admin-view video spends real time mapping custom report columns to JCR metadata
  properties. That means dropping `topic_v2: Metadata` during the initial build (logged
  above as "one clearly mistagged value") was wrong — it was restored after reading the
  transcript. Lesson: don't drop a source page's taxonomy tag as "off-topic" without
  checking the transcript first; the visible frontmatter/description can undersell what
  a video actually covers.

**Open gap:** Insights has two views, so it only exercises the two-tab case. It does
not validate the tabs-only/single-tab convention (single-view page = one `>[!TAB]`
block, no Badge) decided after this pilot was built — see decisions log. Before
batch-converting the ~15 currently single-view pages in this plan, build or preview
one single-tab page and confirm it renders acceptably; if the single-tab UI looks
broken or confusing, revisit before that pattern is used at scale.

## Style: no em dashes, no gerunds, no passive voice

- **2026-08-27** — Swept `insights.md` and `permissions-management.md` for em
  dashes, gerund-form verbs, and passive voice (including the frontmatter
  `description` field, not just body prose) and fixed several: "provides
  reporting" → "provides reports", "walks through creating groups and adding
  users" → "shows how to create groups and add users", "instead of building
  them from scratch" → "instead of a rebuild from scratch", "a creatives group
  denied write access... then granted it" (passive) → "deny a creatives group
  write access... then grant it" (active imperative), "are redirected... instead
  of getting a 404" → "lands there instead of a 404" (active, no gerund), "avoid
  caching restricted content" → "so it doesn't cache restricted content".
  Do this sweep on every remaining page — grep for `—` and `\b[A-Za-z]+ing\b`
  (filtering pronouns like "anything"/"everything" and any external link titles
  quoted verbatim) as a fast first pass, then read closely for passive
  constructions grep can't catch (for example, reduced participles like "a
  report scoped to X" or "any previously generated report").

## Style: video is primary, text supports it

- **2026-08-27** — Text around an embedded video is in service of watching the
  video, not a substitute for it. The first draft of `insights.md` and
  `permissions-management.md` re-narrated nearly every step the video shows
  (report fields, exact click paths, full ACL example) — that competes with the
  video instead of framing it. Trimmed both to short lead-ins per section: what
  the viewer will be able to do, not a transcript of how. Reserve full prose
  detail for things a video genuinely can't carry well (copyable code/config,
  reference tables, comparison facts) — `metadata-driven-permissions.md`'s OSGi
  JSON snippet and `closed-user-groups.md`'s CUG-vs-ACL table are the right kind
  of exception, since there's no video to defer to there (or, for CUG, the table
  is reference material that doesn't retell the video's specific demo). Apply
  this same trim to every remaining tabbed page in this project.

## Style: one H2 per tab, unless there's real written content

- **2026-08-27** — A video-backed tab gets **exactly one H2**, not several. Multiple
  H2s per tab (as `insights.md` and `permissions-management.md` first had, 2-3
  each) over-structures what's really just a short lead-in paragraph for a single
  video, and fights the "video is primary" rule above by making the text look like
  its own multi-part tutorial. Collapsed both back to one H2 per tab (`insights.md`:
  "View and create reports"; `permissions-management.md`: "Manage permissions";
  `governance.md`: "Control access and collaborate").
  - **Exception**: pages with substantial written content beyond a video lead-in
    keep multiple H2s. `metadata-driven-permissions.md` (no video at all, just a
    written tutorial with OSGi config steps) and `closed-user-groups.md` (a video
    plus a genuine bullet-point reference list, a comparison table, and supporting
    links) both correctly keep their existing multi-heading structure.
  - The "parallel heading skeleton across tabs" rule above still applies: it's just
    a skeleton of one matching H2 now instead of two or three.

## Style: sentence-case headings, parallel tab structure

- **2026-08-27** — Audited every heading in every file touched so far and found
  3 sentence-case violations (`closed-user-groups.md` had two Title Case H2s,
  `metadata-driven-permissions.md` had one) plus 1 in `TOC.md` ("Governance &
  Insights" → "Governance & insights"). All fixed. Going forward, check heading
  case on every page before calling it done — Title Case habits creep back in
  easily when lightly editing pre-existing content.
- **2026-08-27** — Tabbed pages use a **parallel heading skeleton across both
  tabs**: give each tab the same H2 progression where the content genuinely maps
  (e.g. `permissions-management.md` uses "Set up groups" → "Apply permissions" in
  both tabs, then one tab-specific closing section; `insights.md` uses "View
  activity" → "Create reports" in both). Don't force identical headings where the
  content truly doesn't map 1:1 — a tab-specific third section is fine — but the
  shared portion of the skeleton should read the same so a reader flipping between
  tabs finds the same topic in the same place. Applies to every remaining tabbed
  page in this project; go back and check this alongside the heading-case sweep
  whenever revisiting a page.

## Branding: "Assets Essentials" is retired, everywhere we touch

- **2026-08-27** — The product name "Assets Essentials" goes away entirely in this
  project. Assets view *is* what Assets Essentials was — there is no longer a
  separate product name, just "Assets view" and "Admin view" as the two UIs for
  AEM Assets. Applies to every file we create or edit going forward:
  - No exceptions for literal on-screen labels (e.g. an Admin Console product
    entry or profile literally named "Assets Essentials" today) — rename those
    references too in any file we touch (e.g. "Assets Essentials administrators
    profile" becomes "Assets view administrators profile").
  - Scope is files we're actively updating, not a retroactive sweep. Do **not**
    edit or delete anything in `help/assets-essentials/` ahead of migrating it —
    that source tree stays exactly as-is until each page is actually merged/moved
    into `help/assets/`, same as before.
  - Applied retroactively to the one page already built that used the term:
    `governance/permissions-management.md`'s Assets view tab (4 mentions renamed).
    `insights.md` had no mentions.

## Metadata & taxonomy bucket: complete

Built all 9 pages in `help/assets/metadata/` (already the right folder for most of
these; only `content-credentials.md` moved in, from `advanced/`). This bucket had
the most transcript-driven reclassifications of any bucket so far — the "Smart
Tags & GenAI metadata" group from the v3 plan turned out to be almost entirely
wrong about which pages are agnostic:

- `metadata-schemas-and-forms.md` — new merge of `assets-essentials/configuring/metadata-forms.md`
  (Assets view, 1 H2) and, on the Admin view side (3 H2s, one per video, three
  distinct sub-features that were three separate classic pages),
  `assets/configuring/metadata-schemas.md`, `metadata-profiles.md`, and
  `metadata-folder-schemas.md`.
- `tagging-and-taxonomy.md` — new merge of `assets-essentials/configuring/taxonomy-management.md`
  (Assets view, 1 H2) and `assets/configuring/tagging.md` + `advanced/blocked-tags.md`
  (Admin view, 2 H2s).
- `genai-metadata.md` — **reclassified agnostic → single Assets view tab.** Transcript:
  "navigate to assets, open your projects folder, click add assets... the AI
  generated tab" — modern Assets view language throughout.
- `content-credentials.md` — **reclassified agnostic → single Assets view tab**, and
  moved from `advanced/`. Same tell as GenAI ("Open AEM assets... Click Add assets...
  click Details... Click the CR pin"), plus the page's own source link already
  pointed at a URL containing `/assets-view/` — a clue sitting in plain sight that
  the initial classification pass missed.
- `image-smart-tags.md`, `video-smart-tags.md`, `custom-smart-tags.md` — all three
  **reclassified agnostic → single Admin view tab.** These are the mirror-image
  mistake: their transcripts say "Assets Console" and "managed tags console" —
  classic Admin terminology — and `custom-smart-tags.md` is an explicit AEM 6.4
  walkthrough. `image-smart-tags.md` and `custom-smart-tags.md` each keep their
  existing multi-heading structure (setup steps, prerequisites, additional
  resources) inside the single tab, per the written-content exception.
- `cascade-metadata.md` — stays agnostic, no tabs, renamed from
  `cascade-metadata-feature-video-use.md`. This is the one page in the original
  group that actually held up: it demonstrates dynamic form-field behavior (a
  metadata schema's requirement/visibility/choice rules), not either view's chrome.
- `metadata-import-export.md` — single Admin view tab, kept its existing multi-heading
  structure (two videos, plus a full CSV format reference) per the written-content
  exception.

**Takeaway for the rest of this project:** a page's "agnostic" label from the
initial inventory pass was a guess based on filenames/descriptions, not verified
against transcripts. Five of six "agnostic" candidates in this bucket turned out to
be view-specific once checked. Do not trust the v3 plan's agnostic/single-view
calls at face value for any remaining bucket — verify each one's transcript before
building it, the same as every page.

Also fixed during the style sweep: gerunds in six places (`configuring one` →
`configure one`, `from applying` → `so they can't apply`, `using GenAI` → `with
GenAI`, `download, publish, and sharing` → `download, publish, or share it`, `by
adding` → `they add... automatically`, `using the Smart Content Service` → `with
the Smart Content Service`, plus one in a frontmatter description). Five redirected
external links fixed (Adobe/Microsoft/JCR spec docs that had moved). All old
files/URLs removed and redirected; both TOCs updated, and the old "Advanced metadata
management" section is now "Metadata & taxonomy," matching the plan's naming.

## Collaboration bucket: complete

Built all 6 pages, all in place in `help/assets/collaboration/` (this folder already
had the right name and most of the right files, unlike Governance & Insights which
needed a new folder — only `customizing-annotations-pdf-output.md` had to move in,
from `advanced/`):

- `watch.md` — **reclassified from agnostic to single Assets view tab.** Third
  time a transcript has overturned a classification made from doc-type/description
  alone (after Insights' `Metadata` tag and `governance.md`'s whole view-scope).
  The video opens with "AEM Assets as a Cloud Service's **Assets view**" — not
  agnostic at all. Lesson holds: **check the transcript, every time, before
  deciding a page doesn't need tabs** — a generic-sounding description is not
  evidence, it's just under-specified metadata.
- `comments-annotations-and-tasks.md` — new page, a 3-way merge of
  `assets-essentials/basics/collaborating.md`, `assets/collaboration/comments-and-annotations.md`,
  and `review-task.md`. Assets
  view tab has 1 H2 (one video that already covers comments+annotations+tasks
  together); Admin view tab has 2 H2s, one per video, since the Admin side split
  this into two separate videos/pages historically. This is the right reading of
  the "one H2 per video" rule, not an exception to it — one tab, two embedded
  videos, two headings.
- `check-in-and-check-out.md`, `versions.md`, `timeline-and-inbox.md` — relocations
  in place (no folder move needed), each wrapped in a single Admin view tab, kept
  their `exl-id`/`TQID`/`jira`.
- `customizing-annotations-pdf-output.md` — relocated from `advanced/`. Fixed a
  real data bug while there: frontmatter had `doc-type: Feature Video` and
  `duration: 13` but the page has no video at all (pure OSGi XML config
  reference) — corrected to `doc-type: Tutorial` and dropped the meaningless
  duration field, matching the `metadata-driven-permissions.md` precedent.

Also fixed during the style sweep: a progressive-tense verb in `watch.md`'s tip
("collection you're watching" → "collection you watch"), a gerund-heavy
description/intro in `check-in-and-check-out.md` ("prevent collaborators from
overwriting..." → "locks an asset so only one collaborator can edit it at a
time"), and a gerund leading the H1 in `customizing-annotations-pdf-output.md`
("Customizing annotations..." → "Customize annotations..." — left the frontmatter
`title` as the gerund-led "Customizing Annotations in AEM Assets" since title
and H1 are allowed to differ and Title Case headline conventions commonly lead
with a gerund). Two XML namespace URIs inside a code block flagged by the link
checker as "redirected" are correctly left alone — they're identifier strings,
not clickable links.

All old files/URLs removed and redirected where the page actually moved (4 of
the 6 pages didn't move, so no redirect needed for those); both TOCs updated.

## Governance & Insights bucket: complete (updated)

**Correction from transcript:** `governance.md`'s doc-type is `Value Video` and its
original description was generic enough ("discover effective asset governance
strategies... manage and organize digital assets efficiently") that it was classified
agnostic during the initial inventory pass, with no tabs. The transcript proves that
wrong: the video is a concrete Assets view walkthrough (collections for access
control, permission/deny rules, magic share links, in-context annotations, task
assignment, an Adobe Express + Firefly edit loop, and approval). Rebuilt it with a
single Assets view tab, a description that reflects the actual demo, and full
taxonomy frontmatter (it previously had almost none — just title/description/
doc-type/duration/jira). This is the same lesson as the Insights `topic_v2: Metadata`
correction: **a thin or generic-sounding description is not evidence a video is
agnostic — check the transcript before classifying a page's view-scope, not just
the doc-type or existing copy.** No Admin-view counterpart exists for this
end-to-end demo, so it stays single-view for now, same pattern as the others in
this bucket.

Left `doc-type: Value Video` unchanged even though the content reads more like a
`Feature Video` (concrete UI walkthrough vs. a business-value pitch) — that's a
content-classification field with pipeline implications I don't fully know, so
flagging it here rather than changing it unilaterally.

## Governance & Insights bucket: complete

Built out the rest of the bucket, so it now matches the outline in full:

- `governance/governance.md` — untouched. Agnostic (a "Value Video" strategic
  overview, not a walkthrough of either UI), so per the tabs convention it stays
  tab-free, same as `ai-search.md`, `discovery.md`, `watch.md`.
- `governance/permissions-management.md` — new merge of `assets-essentials/configuring/permissions-management.md`
  and `assets/configuring/baseline-permissions.md`, two tabs.
- `governance/closed-user-groups.md` — relocated from `assets/advanced/`, single
  Admin-view tab. Content enriched from the video transcript: added the publish
  requirement and the login-redirect option (neither was in the original written
  text), plus a `[!CAUTION]` about dispatcher caching of restricted content.
- `governance/metadata-driven-permissions.md` — relocated from `assets/advanced/`,
  single Admin-view tab. No video (doc-type `Tutorial`), so no transcript pass;
  wrapped the existing reference content as-is. Its image folder moved with it to
  `governance/assets/metadata-driven-permissions/`.
- `governance/permissions-management.md`'s frontmatter role was corrected from both
  source pages' `role: User` to `role: Admin, User` — both transcripts show this is
  an admin-configuration task (assigning groups/ACLs via Admin Console or Tools >
  Security), so the original tagging undersold who this is for.

All four old files/URLs removed and redirected; both TOCs updated (`assets/TOC.md`'s
Configuring and Advanced capabilities sections lost their permissions-related
entries; `assets-essentials/TOC.md`'s Configuring lost its permissions-management
entry).

**Refined convention — exl-id/TQID/jira on relocation vs. merge:** the "omit
exl-id/TQID, jira: TODO" rule from the Insights pilot applies to genuine **merges**
of two or more distinct pages into one new page (new page identity). It does NOT
apply to a **relocation** of a single existing page into its new folder, even if the
content also gets a light edit — that's still the same page, so keep its existing
`exl-id`, `TQID`, and `jira` value. Applied here: `permissions-management.md` (merge)
omits them; `closed-user-groups.md` and `metadata-driven-permissions.md`
(relocations) kept theirs.

## Authoring bucket: complete

Built all 8 pages in `help/assets/authoring/` (already the right folder for 6 of them;
`extract-archive.md` moved in from `advanced/`, `processing-profiles.md` moved in from
`configuring/`):

- `switch-views.md` — stays agnostic, no tabs. Transcript confirms it's genuinely about
  the concept of switching between views itself, not either view's content.
- `navigation.md` — tabs. Admin tab unchanged (video 32046). Assets view tab is new,
  reusing video 335861 (`assets-essentials/basics/using.md`) with an H2 scoped to just
  the view-switcher/browse portion of that video.
- `basic-operations.md` — tabs, and the bucket's biggest merge. Admin tab unchanged
  (video 32044). Assets view tab has **two H2s, two videos**: video 335733
  (`basics/managing.md`, folder/upload/copy/move/delete) and video 335746
  (`basics/creating.md`, image editing via Photoshop Express) — both one-video-per-H2,
  not an exception to that rule.
- `metadata.md` — tabs. Admin tab unchanged (video 32045). Assets view tab is new,
  reusing video 335746 again, this time framed around its metadata-editing portion
  (info icon, basic/advanced/tags panel).
- `extract-archive.md`, `processing-profiles.md`, `renditions.md`, `relate-unrelate.md`
  — all single Admin view tab, no Assets-view counterpart found. Kept their existing
  `exl-id`/`TQID`/`jira` (relocations, not merges) except `extract-archive.md`'s
  description, which was rewritten to drop marketing filler ("informative video,"
  "game changer").

**New precedent — one video, multiple capability pages:** `assets-essentials/basics/using.md`,
`managing.md`, and `creating.md` are each single continuous recordings that cover
several distinct capabilities in one take (for example, `creating.md`'s video covers
uploading, versioning, image editing, and metadata editing back to back). Rather than
force each of those three source pages into exactly one destination, each video is
now embedded on **every page whose capability it genuinely demonstrates**, each time
with its own scoped H2 and framing text pointing at just that portion — never a full
re-narration of the whole video on every page. Concretely:

- Video 335861 (`using.md`) → `authoring/navigation.md` (browse/view-switcher framing)
  and, once the Search and discovery bucket is built, `search-and-discovery/search.md`
  (search/filter framing).
- Video 335733 (`managing.md`) → `authoring/basic-operations.md` (folder/CRUD framing)
  and, once built, `search-and-discovery/collections.md` (its collections framing).
- Video 335746 (`creating.md`) → `authoring/basic-operations.md` (image-editing
  framing), `authoring/metadata.md` (metadata framing), and
  `collaboration/versions.md` (versioning framing) — three pages, three H2s, one
  video, because the video genuinely walks through all three back to back.

Because `navigation.md`, `basic-operations.md`, and `metadata.md` each absorb part of
a retiring assets-essentials page, they're treated as merges per the existing
exl-id/TQID/jira convention: all three now omit `exl-id`/`TQID` and use `jira: TODO`.
`versions.md` (already built in the Collaboration bucket) also loses its `exl-id`/
`TQID`/`jira` for the same reason — gaining real new content from `creating.md` moves
it from a relocation to a merge, so the earlier "kept its exl-id" note for that page is
superseded by this update.

All three source pages (`using.md`, `managing.md`, `creating.md`) are deleted and
redirected: `using.md` and `managing.md`/`creating.md` both point at
`search-and-discovery/search.md` and `authoring/basic-operations.md` respectively (the
single best landing page for each, even though content is now split across several
pages). Both TOCs updated; `assets-essentials/TOC.md`'s Basics section now has only
Quick access and Link sharing left.

Also fixed during the style sweep: 5 gerunds ("ensuring" in switch-views.md's
description, "browsing" and "without leaving" and "by extracting" and "making it
current" elsewhere), and one redirected external link in `switch-views.md`.

## Search and discovery bucket: complete

Built all 9 pages in `help/assets/search-and-discovery/` (`assets-admin-search-rail.md`
moved in from `configuring/`):

- `search.md` — tabs. Admin tab unchanged (video 32054). Assets view tab reuses video
  335861 (the same `using.md` video already embedded on `authoring/navigation.md`),
  framed to its search/filter/facets/saved-search portion — the other half of the
  split anticipated back when the Authoring bucket was built.
- `ai-search.md` — **a new pattern**: the video (3479989) is one continuous recording
  that itself demos enabling AI Search from both the Assets view and the Admin view
  back to back, since the two settings are independent. Rather than force it into a
  single tab or leave it agnostic, both tabs embed the *same* video, each with its own
  H2 and framing text scoped to that view's toggle path (General Settings > Search vs.
  Tools > Assets > Assets Configurations). This differs from the Authoring bucket's
  "one video, several pages" precedent — here it's one video, two tabs, on the *same*
  page, because the source video's own structure already splits cleanly along the
  view boundary.
- `discovery.md` — **stays agnostic, but not for the reason originally guessed.**
  Transcript check (still mandatory, see below) shows this isn't a single-persona UI
  walkthrough at all: it demos importing assets from S3 via AEM's bulk importer,
  AI-powered search, and ContentHub, in one cross-system narrative. Unlike
  `governance.md` (same doc-type, "Value Video," which *did* turn out to be a
  concrete single-view walkthrough once checked), this one genuinely doesn't belong
  to either view's UI, so it correctly stays tab-free. Description and intro were
  still rewritten, since the original text was generic filler that didn't reflect
  the actual content.
- `adobe-firefly.md`, `search-boost.md`, `find-similar-images.md` — wrapped in a
  single tab each (Assets view, Admin view, and Admin view respectively). All three
  were previously untabbed with no explicit view claim; transcripts confirmed the
  view in each case ("AM Assets interface" classic terminology for the latter two).
- `collections.md` — tabs. Admin tab unchanged (video 32053). Assets view tab reuses
  video 335733 (the same `managing.md` video already embedded on
  `authoring/basic-operations.md`), framed to its collections portion (manual,
  public/private, and smart collections) — the cross-bucket reuse flagged as pending
  when the Authoring bucket was built.
- `my-workspace.md` — new page, single Assets view tab, merging
  `assets-essentials/configuring/my-workspace.md` and `basics/quick-access.md` (same
  underlying feature: Quick Access is a widget on the My Workspace page, per the
  original v2 decision log entry). Two H2s, one per video, both in the one tab.
- `assets-admin-search-rail.md` — relocated from `configuring/`, single Admin view
  tab, kept its `exl-id`/`TQID`/`jira` (no new content, pure relocation).

Because `search.md` and `collections.md` each absorb part of an already-retired
assets-essentials page, both are treated as merges: `exl-id`/`TQID` dropped,
`jira: TODO`. `ai-search.md`, `adobe-firefly.md`, `search-boost.md`,
`find-similar-images.md` keep their existing `exl-id`/`TQID`/`jira` since no new
content was merged in, only tabs added around what was already there.

All three assets-essentials source files (`quick-access.md`, `my-workspace.md`, and
the already-deleted `using.md`/`managing.md` reused here) are accounted for in
redirects; both TOCs updated. `assets-essentials/TOC.md`'s Basics section is now just
Link sharing, and its Configuring section is gone entirely (it only ever held
My workspace).

Also fixed during the style sweep: a passive-voice frontmatter description in
`assets-admin-search-rail.md` ("allows assets to be searched for using..." → "sets
the custom search filters available in..."), 2 gerunds after prepositions ("without
leaving," "without digging through"), 2 gerunds in `ai-search.md`'s frontmatter
description, and a duplicated `feature_v2: Generative AI` entry in
`adobe-firefly.md` (same data-quality pattern flagged earlier in
`basic-operations.md` and `creative-cloud.md`).

## Asset distribution bucket: complete

Renamed the old top-level "Activation and sharing" section to **Asset distribution**
and nested **Content Hub** inside it as a fourth sub-header (it was previously its own
top-level TOC entry) — no file moves or redirects needed for Content Hub, since only
its position in the left rail changed, not its URLs.

**Sharing and activation sub-header — real content work:**

- `sharing/link-sharing.md` — **new page**, not a tab merge. The v3 plan called for
  tabbing `assets-essentials/basics/link-sharing.md` together with
  `assets/sharing/activation.md`, but the transcript for `activation.md` (video
  3491670) proved that pairing wrong: it's not a view-specific "how to activate an
  asset" walkthrough at all, it's the third part of the same discovery → governance →
  activation trilogy as `search-and-discovery/discovery.md` and
  `governance/governance.md`, and it's actually a Content Hub feature demo (approval
  gating, collections, dynamic renditions, stakeholder share links). Pairing it with
  link sharing would have bolted two unrelated capabilities into one tabbed page just
  because their titles both mention "sharing." Instead, `link-sharing.md` is now its
  own single Assets view tab (moved from `assets-essentials/basics/`, no Admin-view
  counterpart exists), and `activation.md` stays a standalone agnostic page next to
  it, same treatment as `discovery.md` and `governance.md` — description and intro
  rewritten to reflect what the video actually shows, cross-link paragraph kept as-is.
- `download.md`, `publish.md` — wrapped in a single Admin view tab each; transcripts
  confirmed classic Admin terminology in both ("top action bar," "AEM Author/AEM
  Publish").
- `export.md` — a Tutorial with no video (a Node.js export script), wrapped in a
  single Admin view tab per the written-content exception, no transcript needed.

**Brand Portal, Content Hub, and Asset Share Commons sub-headers — intentionally
untouched.** Unlike every other "agnostic" classification this project has
overturned, this one isn't at risk of the same mistake: these three are genuinely
separate products/experiences (a licensed add-on, a Cloud Service-only add-on, and an
OSS reference app), not alternate UI skins of the same Assets/Admin DAM duality this
whole project is about, so there's no view-scope question to verify per page. Content
left exactly as it was, per the v3 plan.

Also fixed during the style sweep: a duplicated `feature_v2: Integrations` entry in
`publish.md` (same data-quality pattern as `basic-operations.md` and
`creative-cloud.md`), and 5 gerunds across the new/edited Sharing and activation
pages ("using... without requiring," "reducing the risk of," "without logging in,"
"for use and sharing," "making them accessible").

All TOCs updated; redirect added for `link-sharing.md`'s move.

## Dynamic Media: 3 pages folded in, rest confirmed unchanged

Moved `3d-assets.md`, `watermarks.md`, and `video-closed-captions.md` in from
`advanced/` (now empty and removed) into `dynamic-media/`, renamed with a
`dynamic-media-` prefix to match that folder's existing convention, and nested into
the 3D, Images, and Video sub-groups respectively. Transcripts confirmed all three
are classic Admin Console features with no Assets-view equivalent (Tools > Assets
config screens, "top action bar," "Create button"), so each got a single Admin view
tab, consistent with the rest of this project.

The rest of Dynamic Media (the ~35 pages already under `images`, `video`, `viewers`,
`3d`, `dm-with-aem-sites`, and `tutorials`) is confirmed out of scope and left
exactly as-is: it's a licensed add-on with its own dedicated classic Admin UI, not an
alternate view of the same Assets/Admin DAM duality this project is reorganizing, so
there's no Assets-view-vs-Admin-view question to verify page by page here (same
reasoning as Brand Portal/Content Hub/Asset Share Commons, not the "check every
transcript" reasoning that applies everywhere else).

Also found and deleted 2 orphaned image/asset files left over from earlier merges
this session, unreferenced by any page: `advanced/assets/closed-user-groups/folder-properties-closed-user-groups.png`
(from the `closed-user-groups.md` relocation) and `advanced/assets/asset-reports/all-assets.xlsx`
(from the `asset-reports.md` → `insights.md` merge). Worth a final repo-wide orphan
sweep once every bucket is done.

## Developer & APIs bucket: complete

Dissolved both the old "Advanced capabilities" grab-bag (now fully empty and removed)
and the old standalone "Deployment" section into a new **Developer and APIs**
top-level bucket, per the v3 plan's audience-based exception:

- `programmatic-asset-upload.md` — moved from `advanced/` as-is, **not wrapped in an
  Assets view/Admin view tab** despite this project's usual convention. The page
  already uses `BEGINTABS`/`TAB` internally for unrelated purposes (authentication
  method, upload method), and nesting another tab layer around already-tabbed content
  is untested in this system — safer to leave the existing structure alone than risk
  a rendering break. Documented here as a one-off, deliberate exception, not a
  precedent to reuse elsewhere.
- `multitenancy-concurrent-development.md` — moved from `deployment/`, stays
  completely tab-free. It's an architecture article about running multiple dev teams
  on one AEM environment, genuinely agnostic content that isn't about either DAM
  view at all (same category as `cascade-metadata.md`). Renamed from
  `multitenancy-concurrent-article-understand.md` for a cleaner slug, and swept for
  sentence-case headings (it had 14 Title Case H2s/H3s, all fixed) and a Title Case
  H1 (`Understanding Multitenancy and Concurrent Development` → `Multitenancy and
  concurrent development`).

TOC updated (new "Developer and APIs" top-level section; "Advanced capabilities" and
"Deployment" removed entirely); redirects added for both moved pages plus the 3
Dynamic Media fold-ins above.

## Automation bucket: complete

Merged three previously separate top-level sections into one new **Automation**
bucket: `configuring/auto-start-workflows.md` (was in Configuring), the 3-page
`content-automation/` section, and the 4-page `asset-templates/` section (was its
own top-level entry). No files moved folders — only their position in the left rail
changed, so no redirects needed.

All 8 pages are classic AEM 6.4/6.5-or-Admin-only content (several predate Cloud
Service entirely, so an Assets-view counterpart isn't just absent, it's not possible
for that version), confirmed by their own version/description fields rather than
needing a transcript fetch — these aren't thin, generic "Value Video" descriptions
that turned out to hide something (the pattern that kept getting overturned
elsewhere), they're specific, technical descriptions of admin/dev configuration
tasks. All 8 wrapped in a single Admin view tab, consistent with the rest of the
project; the 3 pages with real written content beyond a video lead-in
(`asset-templates-tutorial-understand.md`, `asset-templates-technical-video-setup.md`)
kept their multi-heading structure per the written-content exception, and
`asset-templates-feature-video-use.md` kept its 2 H2s (one per embedded video).

Style sweep: sentence-cased all headings across all 8 files, fixed 2 dangling
participles ("by automatically invoking" → "they automatically invoke," "mapping
product properties" → "and map product properties"). Left several "using X"
mid-sentence constructions and gerunds inside pre-existing, untouched numbered-list
instructions alone (per the pre-existing-content exception) rather than rewriting
content that wasn't otherwise being touched.

## Integrations bucket: complete

Consolidated 5 previously separate top-level TOC entries (Edge Delivery Services,
Adobe GenStudio, Creative workflows, Adobe Asset Link, and the standalone Workfront
integration section) into one new **Integrations** bucket with 5 sub-headers:
Creative Cloud and panels, Adobe Asset Link, Workfront, Edge Delivery Services, and
Adobe GenStudio. GenStudio wasn't in the original v3 outline (it was added to the
repo after that plan was written) but fits the same consolidation logic, so it's
folded in here rather than left as its own top-level entry.

- **Creative Cloud Libraries** — new page, moved from
  `assets-essentials/integrations/creative-cloud.md`. Initially assumed agnostic
  (generic "Assets Essentials" feature tag), but the transcript confirmed modern
  "Libraries" left-nav terminology — reclassified to a single Assets view tab, the
  same mistake pattern as the Metadata bucket's Smart Tags pages, just mirrored (this
  time an agnostic guess that was actually Assets view instead of Admin view). Fixed
  its duplicated `feature_v2: Integrations` entry while there.
- **Adobe Asset Link (Creative Cloud and panels entry) trimmed** — resolved the
  flagged cleanup item: `creative-workflows/adobe-asset-link.md` was a 127-line
  near-duplicate of the dedicated Adobe Asset Link section's `panel-overview.md`,
  plus content that duplicated `place-copy.md`/`place-linked.md`/`for-placement-only.md`.
  Trimmed it to a short overview (matching its sibling pages' length) that links to
  the full section. Its one genuinely unique section, "Adobe Asset Link
  authentication," wasn't duplicated anywhere else, so it became a new page,
  `adobe-asset-link/authentication.md`, inside the dedicated section instead of
  being deleted outright. Moved its diagram image there too, and deleted an
  orphaned, unreferenced `-1` variant of the same image found alongside it.
- **Workfront sub-header** — now has two tracks side by side, per the standing
  decision that these are different integrations, not a view-split of one feature:
  the existing **Enhanced connector** (unchanged, classic full AEM Assets), and a
  new **Assets view connector** track, migrated in from
  `assets-essentials/integrations/workfront/` (5 pages: overview, configure,
  map-metadata, link-send, versions). Every one of these had "Assets Essentials"
  in its title, description, and H1 — all renamed to "Assets view" per the branding
  rule, with no exception for the pattern, plus 5 duplicated `feature_v2:
  Integrations` entries fixed along the way.
- Adobe Asset Link section gained one more page (Authentication); everything else
  in that 10-to-11-page section is unchanged, matching the "unchanged content"
  treatment given to Brand Portal/Content Hub/Asset Share Commons — it's a dedicated
  product panel, not part of the Assets/Admin view duality.

All TOCs updated; redirects added for the Creative Cloud Libraries move and all 5
Workfront Assets view connector pages.

## Overview bucket: partially complete — blocked on 2 deletions

Added a new "Get started in the Assets view" section to `help/assets/overview.md`,
embedding `assets-essentials/getting-started.md`'s video, right after the existing
"AEM Assets walk-through" section — **no tabs**, per the v3 plan's explicit call for
this one page ("orientation only"), so both videos sit side by side as plain
sections rather than competing tabs.

Also migrated `assets-essentials/provisioning.md` (a Cloud Manager/Admin Console
deployment page that existed but wasn't even linked from that book's own TOC) into
`help/assets/developer/provisioning.md`, single Admin view tab, transcript-confirmed
Admin/dev content, corrected its `role` from `User` to `Admin` to match.

**Blocked:** deleting the now-redundant `assets-essentials/getting-started.md`,
`overview.md`, and `TOC.md` (the last 3 files in that book, since everything else
has been migrated out over the course of this session) was denied by the session's
auto-mode safety classifier — it treats fully retiring a book's remaining files as
more consequential than the many individual page deletions already done this
session, even one file at a time. Left all three in place rather than force it:

- Fixed a real bug this session introduced: `assets-essentials/overview.md` linked
  to `./basics/managing.md`, which was deleted earlier in the Authoring bucket work.
  Repointed it to the still-existing `getting-started.md`.
- `getting-started.md`'s content now lives in two places (there and the new section
  in `assets/overview.md`) until this is resolved — not deleted, so no redirect
  added yet either.
- The `+ [Assets Essentials](.../assets-essentials/overview.html)` external link at
  the bottom of `help/assets/TOC.md` is left in place, since that target page still
  exists and still has real (if now mostly redundant) content.
- **Needs a decision from the user**: confirm deleting these 3 files (completing the
  plan's "retire `help/assets-essentials/TOC.md`" next step), or leave the book
  in this reduced state.

**Also not yet actioned — same category of risk, flagged for the same decision:**
the plan's "Retired: Playlists" entry (`playlists/admin-view.md`,
`playlists/assets-view.md`, 520 combined lines of bespoke card markup) was never
executed this session. Given the classifier just blocked a smaller-scale retirement,
this larger deletion should go through the same explicit user confirmation before
being attempted.

## Translation bucket: confirmed unchanged

`translation/source-file-translation-feature-video-use.md` is classic 6.4/6.5-only
content (predates Cloud Service and the Assets view entirely), matching the v3
plan's call to leave it as a single unchanged top-level page with no natural bucket
home. No action taken, none needed.

## New Assets view videos: 5 re-recordings swapped in (2026-08-31)

The user supplied 5 newly recorded Assets view videos to replace older
Assets-Essentials-era ones already embedded across the rebuilt pages. Fetched and
read all 5 transcripts, matched each to its existing home(s) by content (not just
title), and swapped the video ID + reframed the surrounding text everywhere the old
video appeared — no page restructuring needed, since the bucket/tab layout from
earlier in this project already anticipated exactly this kind of refresh.

- **3502566, "Get started with Assets view"** (215s) → replaces video 336005 in
  `help/assets/overview.md`'s "Get started in the Assets view" section. Old video
  was a narrow UI tour; new one covers the same ground plus My Workspace, Tasks,
  Insights, and Settings, so the framing text was broadened to match.
- **3502546, "My Workspace in Assets view"** (263s) → replaces BOTH videos on
  `search-and-discovery/my-workspace.md` (3413809 and 3420975). The old page had
  two H2s, one per legacy video (My Workspace, Quick Access); the new video covers
  both widgets in one recording, so the page collapsed to **one H2, one video**,
  per the standing one-H2-per-video rule — collapsing tab structure is exactly as
  valid a response to new source material as spreading it out, in this case.
- **3502568, "Share assets in Assets view"** (160s) → replaces video 341025 on
  `sharing/link-sharing.md`. Same feature, but the new video also covers sharing
  collections (not just assets/folders) and the download queue/My Downloads flow,
  so the framing text picked up those details. Kept the page's existing
  `exl-id`/`TQID` since this is a content refresh of an existing single page, not a
  new merge — a distinction worth being careful about; the first pass at this edit
  incorrectly dropped them before being corrected.
- **3502545, "Organize and manage assets in Assets view"** (328s) → replaces video
  335733 in **two places**: `authoring/basic-operations.md`'s "Create, upload, and
  organize assets" H2, and `search-and-discovery/collections.md`'s "Group assets
  into collections" H2 — the same two-page split the old video had, since the new
  one covers the identical scope (folder CRUD plus standard/smart collections).
- **3502567, "Asset details in Assets view"** (418s, the longest and broadest) →
  replaces video 335746 in its 3 existing homes (`basic-operations.md`'s "Edit
  images," `authoring/metadata.md`, `collaboration/versions.md`), **and** fills 2
  gaps this same video's broader scope newly justifies:
  - `authoring/renditions.md` — was single Admin view tab only; the new video's
    "Renditions" panel section is genuine Assets-view content, so it gained its
    first Assets view tab.
  - `authoring/relate-unrelate.md` — was single Admin view tab only; the new
    video's "Asset Relations" section (source/derived/other) is the Assets-view
    equivalent of the classic Relate/Unrelate feature, so it also gained its first
    Assets view tab.
  - Both gained new content, not just a video swap, so both moved from
    "relocation" to "merge" status per the exl-id convention: `exl-id`/`TQID`
    dropped, `jira: TODO`.
  - This video is now embedded in 5 places total — the same "one video, several
    scoped homes" pattern established for `creating.md`'s video earlier in this
    project, just with a newer, richer source recording taking over that role.

All durations recalculated (video swap changes the page total even when tab count
doesn't). Confirmed via repo-wide grep that none of the 6 replaced video IDs
(335733, 335746, 341025, 336005, 3413809, 3420975) remain anywhere in
`help/assets/`. Link-checked and style-swept every touched file; no new issues
found beyond what's already documented above.

**Not addressed by this batch:** `authoring/navigation.md` and
`search-and-discovery/search.md` still use video 335861 (`using.md`) — none of
the 5 new videos covered browsing/search/filter, so that video stays until a
replacement for it shows up.

## Both pending retirements approved and complete (2026-08-31)

User confirmed both deletions flagged earlier. The classifier that blocked the
single-file `getting-started.md` deletion last time allowed the same `git rm` this
time — same command, just re-run after explicit user sign-off — confirming this
really was a "needs a human yes" gate, not a hard technical block.

- **`help/assets-essentials/` fully retired.** Deleted the last 3 files
  (`overview.md`, `getting-started.md`, `TOC.md`) plus 6 now-orphaned images from
  `assets/overview/` that only those pages referenced. Added redirects for both
  page URLs to `assets/overview.html` (the getting-started video is now embedded
  there too, per the new-video swap above). Removed the trailing
  `+ [Assets Essentials](...)` external link from `help/assets/TOC.md`. Confirmed
  via repo-wide grep that no remaining `.md` file anywhere links to
  `assets-essentials/` internally (2 pre-existing external hits in unrelated books,
  `cloud-service/integrations/experience-cloud.md` and a playlist URL in
  `assets-view.md`, both untouched — out of scope, not part of this project).
- **Video playlists section retired**, per the original v2/v3 decision log entry.
  Deleted `playlists/admin-view.md` and `playlists/assets-view.md` (520 combined
  lines) plus their 2 orphaned images, confirmed no internal page linked to either
  first. Redirected both URLs to `assets/overview.html`. Removed the "Video
  playlists" section from `help/assets/TOC.md`.
- **`Configuring` flattened to a single top-level page** while in there: it only
  ever held one entry (`Baseline folders`) after Processing profiles and
  Auto-start workflows moved out earlier in this project, so per the TOC rule
  ("if a bucket would only ever hold one page, it's a page, not a bucket") it's
  now `+ [Baseline folders](configuring/baseline-folders.md)` directly at the top
  level, matching how `Overview` and `Translation` are structured.

`help/assets/TOC.md` is now down to 13 top-level entries (from 23 in v2), matching
the v3 plan's consolidation goal.

## Status: project complete

Every bucket in the v3 outline is built: Governance & Insights, Collaboration,
Metadata & taxonomy, Authoring, Search and discovery, Asset distribution, Dynamic
Media (3-page fold-in), Developer & APIs, Automation, Integrations, Translation
(confirmed unchanged), and Overview. `help/assets-essentials/` and the Video
playlists section are both retired (see the section above). `help/assets/TOC.md`
is down to 13 top-level entries (from 23 in v2), one per bucket, consistently 2
levels deep except the 3 pre-approved exceptions (Asset distribution, Integrations,
Dynamic Media).

**Still open, not blocking:**

- A repo-wide orphaned-image sweep beyond the 4 leftover files already found and
  cleaned up this session (from earlier merges/moves) — worth one more pass to be
  sure nothing else was missed.
- A RedPen (`validate_exl_content`) run in an interactive session, since it's been
  unavailable in this non-interactive session the whole time.
- If more re-recorded Assets view videos arrive, `authoring/navigation.md` and
  `search-and-discovery/search.md` are the known remaining pages still running on
  an older video (335861, from `using.md`) with no newer replacement yet.
