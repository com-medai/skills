/README.md
MED-AI Academic Literature Search Coach

This Claude skill guides transparent academic and biomedical literature searches. It searches Consensus, SciSpace, and PubMed when those connectors are connected. When any are missing, it tells the user how to connect them and provides ready-to-paste searches for those platforms instead.

Suggested Claude setup
Upload the .skill package in Claude's skill settings.
Connect Consensus, SciSpace, and PubMed through Claude's connector directory, if permitted by your institution.
Test with a focused research question.

The skill checks connector status at the start of every search and reports which sources were searched live and which were handed off.

Every output that includes articles ends with an Article summaries and gap analysis section: a short summary of each article, an overall evidence summary, a structured gap analysis table, and the top 3 research priorities.

Test prompt

Conduct a structured literature search on changes in sleep reported among adults using GLP-1 receptor agonists. Start by refining the question, then search the connected scholarly sources. Create a PubMed strategy and a SciSpace-ready prompt. Verify citations and produce a search log and evidence matrix.

Important limitation

The skill does not use web search and includes only peer-reviewed journal articles (no preprints, conference abstracts, or grey literature). It searches only the Consensus, SciSpace, and PubMed connectors and any files the user provides. It can only search sources that Claude can access in the current account and conversation. It must disclose unavailable sources rather than imply they were searched.
