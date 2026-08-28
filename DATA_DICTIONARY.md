# Data Dictionary

This document defines every variable used in the "Is Capital Really Leaving China?" analysis (global → regional → local). Every dataset is classified as **PUBLIC** (published directly by an official source), **DERIVED** (compiled by this session from public sources), or **ESTIMATED** (third-party or secondary-cited figures).

**Data quality is uneven across the three tiers by design of the topic** — global and regional statistical agencies publish clean structured time series; Malaysia-specific figures had to be hand-compiled from a series of press releases, and are noticeably less complete. This is stated plainly rather than smoothed over.

**A separate "Why Is This Happening?" section at the end of each notebook adds qualitative context** — secondary-sourced explanations (news reporting, industry analysis) for the mechanism behind each quantitative finding below. That content is deliberately *not* classified PUBLIC/DERIVED/ESTIMATED like the datasets in this file, since it's explanatory reporting rather than a number this project is asserting — full citations are in [`references/SOURCES.md`](./references/SOURCES.md) under "Context / Secondary Sources."

---

## global_fdi_by_region.csv

**Source:** UNCTAD, *Global Investment Trends Monitor No. 50* (January 2026), Annex Table 1. Fetched and read directly from the primary PDF this session.
**Classification:** PUBLIC
**Coverage:** 2023–2025, by region/economic grouping
**Description:** FDI inflows in USD billions, for World, Developed economies, Developing economies, Asia, and Asia's sub-regions (East Asia, South-East Asia, South Asia, West Asia).

### Known limitations
- **2025 figures are UNCTAD's own estimates** ("2025*" in the source table), based on data through Q3 2025 — not yet final.
- **"East Asia" is not the same as "China."** East Asia includes China, Japan (as a developing-vs-developed classification nuance), South Korea, Hong Kong, and others. The report's own narrative text (not this table) states China's FDI specifically fell 8% in 2025 — see `china_fdi_inflows.csv`.
- **South-East Asia here is a UN region grouping, not identical to ASEAN's 11 member states** (UN South-East Asia excludes Timor-Leste from some classifications and uses different boundaries in places) — close enough for this analysis' purposes but not a perfect match to `asean_fdi_by_source.csv`'s ASEAN Secretariat definition.

## china_fdi_inflows.csv

**Source:** UNCTAD, *Global Investment Trends Monitor No. 50* (January 2026), narrative text (not a table)
**Classification:** PUBLIC
**Coverage:** 2025 only, with a directional claim about 2023–2025
**Description:** China's FDI inflows declined 8% in 2025 to an estimated $107.5 billion — UNCTAD states this is the third consecutive year of decline.

### Known limitations
- **Only one absolute value is available** (2025: $107.5B). The report states the *direction* for 2023 and 2024 (both also declines) but does not give their dollar values in this publication. This analysis cannot chart a full 2023–2025 China-specific trend line — only report the 2025 level and the stated multi-year decline.

## asean_fdi_by_source.csv

**Source:** ASEAN Secretariat – ASEAN FDI Database, via the ASEANstats Data Portal (data.aseanstats.org), indicator FDI.AMS.DES.INF.TOT
**Classification:** PUBLIC
**Coverage:** 2019–2025, annual, China/Japan/United States as source countries into ASEAN as a whole
**Description:** Inward FDI flows into ASEAN (all 11 member states combined) by source country, in millions of USD.

### Known limitations
- **This is ASEAN-aggregate, not Malaysia-specific.** It answers "is the region capturing a shift," not "is Malaysia specifically." See `malaysia_fdi_by_source.csv` for the local layer.
- **2025 data is marked "preliminary"** by ASEANstats as of the 1 July 2026 update, subject to revision.
- **Large year-to-year swings (e.g. US 2023 at $83.5B, more than double any other year) likely reflect one or a few very large deals**, not a smooth underlying trend — this analysis does not have deal-level detail to confirm what drove any single year's spike.

## malaysia_fdi_by_source.csv

**Source:** Compiled by this session from multiple MIDA (Malaysian Investment Development Authority) media releases: the FY2022, FY2023, FY2024, and Q1 2026 investment performance releases, and web-search-summarized figures for FY2023 H1. See `references/SOURCES.md` for each release's URL.
**Classification:** DERIVED — real published MIDA figures, hand-compiled across several separate releases (no single downloadable time series was accessible this session)
**Coverage:** Uneven — a mix of full-year (FY), first-half (H1), and first-quarter (Q1) periods, not a consistent annual series
**Description:** Malaysia's approved foreign investment (MIDA's "FI" measure — approved projects, not realized capital flows) by source country, in RM billions.

### Known limitations
- **This is the least consistent dataset in this case study, and that inconsistency is real, not a formatting choice.** Different rows cover different period lengths (full year vs. half year vs. one quarter) because that is what each MIDA release actually reported for that country in that period — padding this into a fake consistent annual series would misrepresent the source data.
- **MIDA's own "ultimate source" methodology was only formalized in December 2023** (explained in the Q1 2026 release). Earlier years' country attributions may reflect the immediate registered investor's country (e.g. a holding company in the Netherlands or Cayman Islands) rather than the ultimate parent's home country — explaining why the Netherlands and Cayman Islands topped Malaysia's 2023 source-country list ahead of the US and China, a result that looks anomalous next to 2022 and 2024 and is flagged as such in Notebook 03.
- **"Approved" investment (MIDA's FI) is a forward-looking indicator, not realized investment.** MIDA states 18–24 months typically elapse between approval and a project actually being implemented — this is a different concept from DOSM's FDI balance-of-payments measure, and the two should not be treated as interchangeable (MIDA states this explicitly in its own releases).
- **Where a country did not appear in a release's "top 5" list, no figure is recorded** (rather than assumed to be zero or estimated) — e.g. Japan's FY2022 and FY2024 figures are genuinely unknown from the sources available, not zero.
