---
name: "medai-journal-finder"
description: "Recommend and compare target journals for a research manuscript from its title and abstract, scoring fit on scope, study type, credibility, metrics, indexing, costs, speed, open access and visibility."
---

# MED-AI Journal Finder

Helps a researcher pick the best-fit journal for a manuscript. Built on the MED-AI "What to consider when choosing a journal" framework: ten criteria, with the reminder that **a high impact factor does not automatically mean the journal is the best fit. Audience, indexing and likelihood of acceptance may matter more.**

## Accuracy rules (apply to every step)

- Never invent a journal, metric, fee, acceptance rate, turnaround time or URL.
- Every metric and fee in the output carries its source link and the date it was checked.
- If a value cannot be verified from the journal's own site or an authoritative index, write **"Not verified"**. Do not estimate.
- Mark figures that change often (APCs, impact factor, CiteScore, turnaround times) with "verify before submission".
- Note that indexing and metrics are updated yearly, so values may have changed since they were checked.

## Step 1: Intake (always ask first)

Use AskUserQuestion, or plain text if that is unavailable. **Required:**

1. Manuscript title
2. Abstract (pasted or uploaded file)

**Optional, asked in the same round with sensible defaults:**

- Article type: original research, systematic review/meta-analysis, pilot/feasibility, case report, brief report, commentary, protocol
- Approximate word count, number of figures/tables
- Open-access requirement: required / preferred / no preference
- APC budget: none / under $1,500 / under $3,000 / no limit
- Priority: speed, prestige/metrics, specific audience (e.g., osteopathic physicians, sports medicine, esports, medical education), or balanced (default)
- Journals to include or exclude, and any prior rejections

Do not start searching until you have the title and abstract. If the abstract is unclear on study design or population, ask one clarifying question instead of guessing.

## Step 2: Profile the manuscript

From the title and abstract, extract and briefly show the user:

- Field and subfield, target readership
- Study design and the matching reporting guideline (CONSORT, STROBE, PRISMA, STARD, CARE, SRQR, SPIRIT, CHEERS, TRIPOD, etc.)
- 4–8 keywords and likely MeSH terms
- Novelty angle in one sentence

## Step 3: Build the candidate list from evidence, not memory

1. Search PubMed (PubMed connector) with the keywords/MeSH terms for similar articles from the last 5 years. Also run Consensus and/or SciSpace if connected.
2. Tally the journals that published the closest matches. Journals that publish work like this are the strongest candidates (criterion: Article and study type).
3. Add journals the user named. Drop journals the user excluded.
4. Keep 8–12 candidates for verification. If a connector is missing, say so and tell the user how to connect it.

## Step 4: Verify each candidate against the ten criteria

Use web search/fetch on the journal's own pages and authoritative indexes. For each journal record:

| Criterion | What to check | Where |
|---|---|---|
| Scope and audience | Aims and scope statement; does it reach the right readers | Journal "Aims & Scope" page |
| Article and study type | Accepts this article type and design; similar papers recently published | Author guidelines; Step 3 results |
| Reputation and credibility | Peer reviewed, legitimate publisher, COPE membership, not on predatory warning signs | Journal site, COPE member list, DOAJ (for OA), Think.Check.Submit checklist |
| Journal metrics | Impact factor, CiteScore, SJR quartile, acceptance rate | Clarivate JCR (often subscription-only; say so), Scopus Sources, SCImago; acceptance rate only if the journal publishes it |
| Author requirements | Word/abstract limits, figure limits, reporting-guideline requirement, data-sharing policy, preregistration requirement | Author guidelines |
| Visibility | MEDLINE, PubMed, PubMed Central, Scopus, Web of Science, Google Scholar | NLM Catalog (MEDLINE status), Scopus Sources, Clarivate Master Journal List |
| Social media presence | Active journal accounts (X, LinkedIn, Bluesky), promotes articles, accepts visual abstracts | Journal site and linked accounts |
| Publication costs | APC, submission fees, page charges, color-figure fees, waivers | Journal fees page |
| Publication speed | Time to first decision; acceptance to publication | Journal site or article history dates, if reported |
| Open-access options | Gold, hybrid, green/self-archiving policy, license (CC BY, etc.) | Journal OA policy; Sherpa Romeo |

Indexing caveat: being in PubMed or PMC is not the same as being MEDLINE-indexed. Report MEDLINE status from the NLM Catalog.

Cost note: NYIT has no institutional read-and-publish or APC agreements, so treat every APC as a full out-of-pocket or grant cost. Highlight subscription-model journals with no author fees, journals with fee waivers or discounts, and green open-access (self-archiving) routes as lower-cost options.

Flag any journal with predatory warning signs (unsolicited invitations, unverifiable indexing claims, promised very fast review, fake metrics, no clear peer-review policy) and remove it from the shortlist with the reason stated.

## Step 5: Score and tier

Score each verified journal 1–5 on each criterion. Default weights (adjust to the user's stated priority):

- Scope and audience 20%
- Article and study type 20%
- Reputation and credibility 15% (any predatory flag = excluded)
- Visibility/indexing 15%
- Journal metrics 10%
- Publication costs 5%
- Open-access options 5%
- Publication speed 5%
- Author requirements (fit with current manuscript) 3%
- Social media presence 2%

A "Not verified" value scores as neutral (3) and is labeled, never filled in.

Group the shortlist into three tiers:

- **Reach**: strong metrics, competitive, still a real scope fit
- **Target**: best overall fit, the recommended first submission
- **Safety**: solid indexing and scope fit, higher likelihood of acceptance

## Step 6: Output

Keep it concise and leadership-ready.

1. **Manuscript profile** (3–5 lines from Step 2)
2. **Top recommendation** with 2–3 sentences on why it fits
3. **Comparison table** for the 5–8 shortlisted journals: journal, publisher, tier, fit score, scope match, MEDLINE (Y/N), IF / CiteScore / quartile, APC, OA model, time to first decision, word limit, key requirement to fix before submitting
4. **Excluded journals** and why (one line each)
5. **Before you submit** checklist: reporting guideline, word count, formatting, data-sharing statement, cover letter angle for the top pick
6. **Sources** with links and the date checked

Close with the reminder: a high impact factor is not automatically the best fit; audience, indexing and likelihood of acceptance may matter more.

Deliver the summary in chat. If the user wants something to keep or share, offer a document (or a Word/Excel file if they name that format). can you list whch journal have a strong LikedIn and social media presence and give me a submission plan
