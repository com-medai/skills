# Add a skill to Microsoft 365 Copilot

**NYIT MED-AI / Skills Quick Guide**

Use this guide to upload a MED-AI skill ZIP, test it, and reopen your agent in Copilot.

## 1. Open Agent Builder

### Get your skill ZIP ready

If you downloaded only `SKILL.md`, compress the file into a ZIP. Open the ZIP and check that `SKILL.md` is visible at the top level.

```text
nyit-irb-prep.zip
└── SKILL.md
```

Keep any required companion files in the ZIP. The `SKILL.md` header must include the skill’s name and description.

### Start a new agent

Sign in to [Microsoft 365 Copilot](https://m365.cloud.microsoft/) with your NYIT work account. In the left sidebar, select **Agents** (also called **Agents & Skills**), then **New agent**.

![The arrow points to Agents in the Copilot sidebar.](copilot-skill-images/01-agents-menu.png)

![The arrow points to New agent in the Agents menu.](copilot-skill-images/02-new-agent.png)

If you already have an agent, open it for editing and select **Configure**.

## 2. Upload the skill ZIP

### Open Configure

On the **Build your own specialist agent** screen, select **Skip** (or **Skip to configure**) to open the configuration tab.

![The arrow points to Skip on the Agent Builder welcome screen.](copilot-skill-images/03-skip-to-configure.png)

### Add the ZIP under Skills

In **Configure**, scroll to **Skills** and select **Add**. Choose the ZIP in the upload dialog. The skill’s name should appear in the list.

![The arrow points to Add in the Skills section before the upload.](copilot-skill-images/04-add-skill.png)

![The arrow points to nyit-irb-prep in the Skills section after the upload.](copilot-skill-images/05-skill-added.png)

If **Skills** or **Add** is missing, ask NYIT IT to check your Copilot access and organization settings.

## 3. Set up and test the agent

### Give the agent a name and instructions

Use the pencil to rename **New Agent** (A), fill in **Describe your agent**, and tell Copilot when to use the uploaded skill in **Instructions** (B).

![A points to the rename pencil, B to Instructions, C to Preview, and D to Create.](copilot-skill-images/06-agent-builder-controls.png)

### NYIT IRB Prep example

Use the text below or adapt it for your own skill.

**Name**

> NYIT IRB Prep

**Description**

> Helps NYIT and NYITCOM researchers check IRB readiness and draft Cayuse application responses.

**Instructions**

> Use the nyit-irb-prep skill for NYIT or NYITCOM IRB preparation. Ask for missing study details before drafting. Flag approvals that need confirmation and mark Cayuse responses as drafts for researcher review.

### Preview, then create

Open **Preview** (C), also called **Try it**, and use the fictional prompt below. If the agent asks for missing details, select **Create** (D) or **Update** for an existing agent.

> I’m planning an anonymous survey of NYITCOM medical students about sleep habits. What information do you need before drafting my Cayuse application?

## 4. Open your agent again

Return to [Microsoft 365 Copilot](https://m365.cloud.microsoft/) with the same work account. Open **Agents** and choose **NYIT IRB Prep** or the name you gave your agent.

![One arrow points to NYIT IRB Prep in the Agents menu. A second arrow points to More agents.](copilot-skill-images/07-open-saved-agent.png)

If the agent is missing from the sidebar, choose **More agents** (or **All agents**). In the Agent Store, look under **Your agents**, select **See more** if needed, then choose your agent and select **Open**.

In the agent’s chat, try this request.

> Help me check whether my study is ready for NYITCOM IRB submission.

## Microsoft Learn references

- [Add skills in Agent Builder](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-add-skills)
- [Build and test agents](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-build-agents)
- [Find and manage your agents](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-share-manage-agents)

*November 2026*
