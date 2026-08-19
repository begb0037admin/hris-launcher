# RESUME.md — hris-launcher

**Purpose:** durable state record for this repo. It did not exist before 19 August 2026 — this repo had `CLAUDE.md`/`README.md`/`CONSTITUTION.md`/`AGENT_MODEL.md` but no per-session handover file. Created because a session touched this repo for the first time from outside its own normal governance (see below) and a future session, cold, needs to know what changed and why without reconstructing it from commit messages alone.

**Read this first**, then `CLAUDE.md` for orientation, then `BRANDING.md` from `begb0037admin/command-centre` before any further visual change (per `CLAUDE.md`'s own Bootstrap Order).

---

## Current State — 19 August 2026

**Who did this and why:** this session was run by Adam, Kevin's dedicated agent for `begb0037admin/hr-fa-knowledge-base`. `hris-launcher` is normally outside Adam's scope entirely — Kevin explicitly authorized touching this repo for this one task only, as a one-off exception, not a standing scope change. `AGENT_MODEL.md`'s repo table (Section 8) still lists `hris-launcher` as governed directly by Claude Code / the acting operator, not by any dedicated per-repo agent; that has not changed as a result of this session.

**What changed, in `index.html`:**
1. Removed 9 dead nav-links from the "Services" sidebar section: all 8 entries under "Service Catalogue" (PeopleXD Service, HR Reporting Service, Internal Jobs List, Childcare Database, Staff Immigration Case Management, Health & Safety (IRIS), BizTalk Integration, Survey Advice) plus "Reward | Personnel Services" from "Other Teams." All 9 use domains (`services.it.ox.ac.uk`, `www.admin.ox.ac.uk`) that fail to resolve via Oxford's own authoritative DNS resolver (`resolver0.dns.ox.ac.uk`, 3 consecutive "Non-existent domain" responses, confirmed by a linked session working on `hr-fa-knowledge-base`, which mirrors this sidebar's content). The now-empty "Service Catalogue" nav-group was dropped entirely (header + wrapper) rather than left as a dead toggle with no items.
2. Added a new "Oxford IT Sign-In Directory" nav-group (53 entries) to the same "Services" section, using this file's existing static `nav-group`/`nav-group-toggle`/`nav-link` HTML pattern exactly — no new CSS, no new JS. Source data: `begb0037admin/hr-fa-knowledge-base`'s `data/oxford-signin-directory.json`, embedded as a static snapshot (not a live fetch — see reasoning below).
3. "Other Teams" now has 3 entries (HR Analytics Team, Payroll | Finance Division, Pensions | Finance Division). "Data Protection" unchanged (2 entries, both confirmed live with real `200`s).

**Why static embedding, not a live fetch of the KB's JSON:** this file's `CLAUDE.md` states "no framework, no build step," and every other nav-link in the file (79 total after this change) is static HTML. Adding a runtime `fetch()` to another repo's data file would be a first-of-its-kind architectural pattern here and a silent cross-repo failure point (breaks if the KB's file moves or CORS-blocks it). Matching "this file's own existing visual style/structure as closely as possible" was read as including its *architecture*, not just its CSS — so the data was embedded statically instead.

**Commit:** `04b8d545b483fbdb3fadf84d2d1d6ff82cc4a998`. **Restore point (pre-change):** `index.html` @ `071eaa9b874b3a4d0356b9d6757ed4c3f6fc649d`, `main` HEAD @ `295cd3ea021147c536e9310512312cebadcf967f`.

**Verification performed, and what it did *not* cover:**
- Local diff against the pre-change file confined to exactly 2 hunks, both inside the "Services" sidebar block — nothing else touched.
- Structural checks: `nav-group`/`nav-group-items` div-open/close counts balanced (5 groups, matching the pre-change count since Service Catalogue was replaced 1-for-1 by the new Sign-In Directory group), `<aside>` balanced, Oxford crest `<img>` reference (`images/oxford-crest.jpg`) confirmed still present and untouched — this is a hard rule in `CLAUDE.md` ("NEVER embed the Oxford crest as base64").
- Pushed via `gh api .../contents/index.html -X PUT` (base64 content from a file on disk), then re-fetched via the git blob API and diffed byte-for-byte against what was tested locally — identical.
- This repo's `pages build and deployment` Actions run (`32281435422`) polled via `gh run view` to actual `completed`/`success` (~18 seconds — this repo's Pages `build_type` is `legacy`, i.e. classic branch-source Pages, but still triggers a real dynamic Actions run that can be polled the same way as `hr-fa-knowledge-base`'s).
- Live `https://pxd.lelitte.co.uk/` fetched directly with a cache-busting query string and a browser User-Agent — matched the pushed content's byte count on the first attempt, and a full diff against the tested local copy was byte-for-byte identical.
- **What was NOT verified:** no Playwright/browser-automation tool was available this session. Everything above is data/HTML-level verification (structural checks, byte-for-byte diffs of the raw HTML), not a rendered-DOM screenshot. **Kevin has not yet seen an actual screenshot of the rendered sidebar and has not approved this visually** — that is still outstanding. Per this repo's own `CONSTITUTION.md` Section 11 (mockups/visual design should go through a Claude Artifact before repo commit) versus the actual instruction this session was given (build directly, get screenshot approval after — same order of operations already used on `hr-fa-knowledge-base`'s own SERVICES build), Section 6's own source-of-truth hierarchy (current operator instruction outranks the constitution's standing default) was used to resolve the tension in favour of proceeding, stated here explicitly rather than silently either ignoring Section 11 or blocking on it.

**What a future session should do with this:**
- If Kevin has since seen and approved a screenshot, note that here (or in a new dated entry) and this item is closed.
- If Kevin asks for further "Services" sidebar changes, this file's existing pattern (static `<a class="nav-link">` per entry, one `nav-group` per logical grouping) is the one to keep matching — don't introduce a data-loading layer without a fresh explicit reason.
- This repo still has no per-repo dedicated agent (unlike `hr-fa-knowledge-base`/Adam). Check `begb0037admin/agent-commons/AGENT_DIRECTORY.md` for current routing before assuming who owns follow-up work here.

---

## Update — 19 August 2026 (same day, follow-up)

Kevin looked at the live result above and asked for two changes: (1) drop the redundant "- sign in" suffix from every title, (2) stop treating the 53 entries as one flat list — reorganize by actual function, folding some into existing groups (Support Tools/Other Teams/Data Protection) where they genuinely fit, and creating new groups where nothing existing fit. Explicit instruction: "don't be so rigid to stick to the only directories we have."

**What changed:** the single "Oxford IT Sign-In Directory" nav-group was replaced by 10 new nav-groups (HR & Case Management, Microsoft 365 & Communication, Network/Devices & Remote Access, Finance & Research Costing, AI Tools, Research & Scholarly Systems, Learning & Teaching, Student/Careers & Academic Records, Library & Digital Scholarship, Facilities & Procurement), decided by reading all 53 entries individually rather than a mechanical rule. Five entries judged to fit the pre-existing "Support Tools" group better than any new one were appended there instead (BeyondTrust Remote Support, Chorus Phone Management, Clarity, Mosaic Website Management, My Sign-ins). Two exact-URL duplicates against pre-existing Support Tools entries were dropped rather than kept redundantly: "Teams (Nexus365)" (same URL as "MS Teams") and "IT Self Service (OSM)" (same URL as "Oxford Service Manager (OSM)"). All 53 source entries verified programmatically accounted for before writing any HTML (51 placed across the new groups + Support Tools additions, 2 duplicates dropped).

Result: 14 nav-groups total (up from 5), 75 nav-links total, 0 remaining "- sign in" title suffixes. Commit `2f1221e6`. Verified: structural checks (balanced nav-group/items counts, crest intact) → pushed → re-fetched via git blob API, byte-for-byte identical → this repo's Pages deployment (run `32297650742`) polled to `completed`/`success` → live `pxd.lelitte.co.uk` fetched directly, byte-for-byte identical, all 14 group names confirmed present.

The same title-cleanup + categorization was also applied to `hr-fa-knowledge-base/data/oxford-signin-directory.json` (all 53 records retained there — no equivalent pre-existing groups to dedupe against, so the 5 "Support Tools"-style entries got their own category, "IT Support & Admin Tools," instead) for consistency across both sites showing this data. Full detail in `hr-fa-knowledge-base/HANDOVER.md` → session 7, Part 3.

**Still outstanding:** the visual/screenshot approval from the original entry above is still open, now against this updated version of the sidebar.

---
