# MEDAI NYIT IRB Assistant Prep Guide

A skill that prepares NYIT and NYITCOM human-subjects research for IRB submission. It checks protocol readiness, identifies required pre-IRB approvals (SARRC, ERDC, MRI/fMRI, Department Chair, CITI), and builds a complete draft of the NYIT Cayuse IRB application, one question at a time, in Cayuse's exact section order, so the researcher can copy and paste each answer into Cayuse.

The skill prepares drafts only. It never submits, certifies, or approves anything. Official review-level and institutional determinations belong to the PI and authorized NYIT IRB staff.

## What it does

1. **Reviews the protocol.** Reads every uploaded document, extracts population, sites, recruitment, data sources, procedures, personnel, funding, and risk, and flags inconsistencies across documents.
2. **Determines pre-IRB approvals.** Evaluates SARRC, ERDC, MRI/fMRI documents, Department Chair approval, and CITI training independently against NYIT rules.
3. **Builds checklists.** Produces a prerequisite checklist and an IRB packet checklist grouped into approvals needed before submission, documents uploaded with Cayuse, and operational screening after approval.
4. **Gives a readiness summary.** Lists what is ready, what is missing or unresolved, and the researcher's next step.
5. **Drafts the application.** Either builds the Cayuse application together, question by question, or reviews an existing draft or Cayuse preview PDF against the protocol.
6. **Drafts participant-facing materials.** Consent forms, recruitment text, and REDCap survey headers, using the bundled NYIT templates.
7. **Runs a final self-check** against the NYIT IRB reviewer checklist and lists what reviewers will likely ask about.

## Repository contents

```
medai-nyit-irb-assistant-prep-guide/
├── SKILL.md                         Skill instructions and workflow
├── references/
│   ├── cayuse-application.md        Every Cayuse question, in order, with branching
│   ├── prerequisite-rules.md        When SARRC, ERDC, MRI/fMRI, Chair approval, and CITI apply
│   ├── sarrc-forms.md               SARRC flowchart, SOP Form, Delegation Log
│   ├── erdc-form.md                 ERDC data request form
│   ├── mri-fmri.md                  MRI consent, fMRI screening, addendum, overview checklist
│   ├── consent-templates.md         Long consent template and REDCap survey header
│   └── reviewer-checklist.md        IRB reviewer checklist for final self-check
└── assets/                          Original NYIT forms (PDF and DOCX) to hand to researchers
```

## Suggested Claude setup

1. Upload the `.skill` package in Claude's skill settings.
2. Upload your research protocol or study summary when you start a conversation.
3. Test with the prompt below.

## Test prompt

> I'm preparing an IRB submission for a study that recruits NYITCOM medical students to complete a REDCap survey and a 6-minute walking test. Here is my protocol. Check what pre-IRB approvals I need, build the prerequisite and packet checklists, and then help me complete the Cayuse application one question at a time.

## How it works with you

- Asks **one question at a time** and waits for your answer.
- Accepts **"skip," "not sure," or "come back later,"** records the item as Pending, and revisits it before the draft is complete.
- **Prefills answers from your protocol** and asks you to confirm or edit.
- Tags every Cayuse question **Complete**, **Pending**, or **Needs clarification**.
- Writes answers as plain text so they paste cleanly into Cayuse text boxes, with word counts for limited fields.

## Important limitations

- **Drafts only.** The skill does not submit to Cayuse or make institutional determinations. The IRB makes the final review-level decision.
- **No invented content.** It will not fill in study facts, names, credentials, dates, signatures, or approvals. Items are marked Approved only when you provide an approval letter or equivalent evidence.
- **Source conflicts are flagged, not resolved.** When NYIT sources disagree, the skill names the conflict and asks the PI or NYIT IRB staff to decide.
- **Names in templates are not facts.** Contacts that appear in templates are treated as "confirm current contact."
- **Some NYIT sources are not bundled.** These include the Department Chair Approval Form, the Cayuse submission guide, CITI registration instructions, the Short Form consent, the Qualtrics survey template, assent templates, and the parental consent template. When one is needed, the skill marks it **Needs source** and points to the OSPAR IRB website.
- **NYIT forms change.** Bundled forms reflect the versions included at packaging time. Confirm current versions with NYIT OSPAR before submission.
