# AI Classification Lab - Copilot in SharePoint

**A hands-on learning experiment for records and information management professionals.**

This repository provides two reusable Copilot in SharePoint skills designed to help you explore how AI-assisted records classification behaves. The goal is **not** to provide a production records management solution. It is to help you test recommendations, inspect explanations, challenge assumptions and learn how instructions and classification references influence results.

Read the accompanying article: **[Exploring AI Classification in SharePoint]([Linked In]([https://au.linkedin.com/in/andrewjolly](https://lnkd.in/p/gA6k5DjH))**.

> **Learning environment only.** Use a separate test SharePoint site and fictional or appropriately authorised documents. Do not rely on this demonstration to determine retention, disposal or regulatory compliance obligations.

## What you'll explore

- How a document's **business purpose and primary activity** influence a proposed classification.
- Why a document can appear to fit more than one retention or disposal class.
- How a skill can express uncertainty and request **human review** rather than force a class.
- What a generated classification rationale does — and does **not** — tell you.
- How changing **Local Guidance**, the reference schedule or the skill instructions can change an output.
- How reusable SharePoint skills are structured as Markdown and used in Copilot.

## What's included

The intended repository structure is:

```text
README.md
skills/
  ai-classification-lab-setup/
    SKILL.md
  ai-classification-review/
    SKILL.md
sample-data/
  RDS.xlsx
```

**Skill 1 — AI Classification Lab Setup** prepares the SharePoint libraries, columns and fictional training content, and checks that the environment is ready. It should not classify documents during setup.

**Skill 2 — AI Classification Review** examines selected documents against the reference RDS, compares plausible classes, records a recommendation and produces a Markdown report. Where justified by its rules, it can update the source document's `Retention Class` metadata.

### About the sample classification reference

The planned `RDS.xlsx` consolidates classification classes drawn from the **National Archives of Australia (NAA) Administrative Functions Disposal Authority (AFDA) Express Version 2**, published online across its administrative functions. It provides real-world classification descriptions to experiment with, rather than a short list of classes invented for the demonstration.

- **Original source:** [National Archives of Australia — AFDA Express Version 2 functions](https://www.naa.gov.au/information-management/records-authorities/types-records-authorities/afda-express-version-2-functions).
- **Compilation:** The workbook is a user-prepared consolidation for this learning lab; it is not an official NAA workbook or a substitute for consulting the individual published authorities.
- **Application:** Although descriptions originate from published authorities, the compiled workbook is **not an authoritative retention and disposal schedule for your organisation**. Verify jurisdiction, applicability, original class wording, versions and disposal authorisations independently before using any classification for real records.
- **Sample documents:** These should be fictional or appropriately authorised; they are distinct from the real-world source descriptions in the workbook.

The workbook is intended to be included in the repository once finalised. Check that it is actually present before following the installation steps. The uploaded skills reviewed for this draft still refer to `RDA.xlsx` and must be updated to `RDS.xlsx` before the documented setup is run.

### Before using these instructions

**Align the two supplied skills first.** As reviewed, both skills use `RDA.xlsx`; the classification skill calls the optional column `Local Application Guidance`, while this README uses the intended name `Local Guidance`. The two skills also use different names for some result metadata columns. The README describes the **intended aligned version**, not a claim that these changes have already been made. See [Check skill consistency before testing](#check-skill-consistency-before-testing).

## Prerequisites

You will need:

1. An active **Microsoft 365 Copilot** licence and access to **Copilot in SharePoint** on the target site.
2. A SharePoint site dedicated to testing, with sufficient permissions to create and configure libraries and site skills. Microsoft documents **Edit** permissions to create site skills and **View** permissions to run them; creating libraries or metadata may require additional site permissions.
3. The two Markdown skill definitions and a sample `RDS.xlsx` from this repository.
4. A small set of fictional or non-sensitive documents that you can use for classification experiments.

Feature availability can vary during service rollout. Everyday Copilot in SharePoint capabilities are included with a Microsoft 365 Copilot licence; some advanced or large-scale operations use Copilot Credits and usage-based billing. Check your organisation's licensing, governance and spending controls before proceeding.

Microsoft references:
- [Extend Copilot in SharePoint with skills](https://learn.microsoft.com/en-us/sharepoint/copilot-in-sharepoint-skills)
- [Get started with Copilot in SharePoint](https://learn.microsoft.com/en-us/sharepoint/ai-in-sharepoint-get-started)

## How the lab is organised

| SharePoint library | Purpose |
| --- | --- |
| **Records Classification Reference** | Stores `RDS.xlsx`, the classification reference used by the review skill. |
| **Classification Lab** | Stores sample documents and source classification metadata, including `Retention Class`. |
| **Classification Results** | Stores one human-readable Markdown assessment for each document processed, with supporting result metadata. |

Once aligned, the review skill uses `FunctionName` (the exact value it will recommend or write) and `ClassDescription` (the substantive text it compares to the document) from the reference workbook. An optional `Local Guidance` column can provide supplementary organisational interpretation, but must not override the original class descriptions. See [Use your own schedule or classification scheme](#use-your-own-schedule-or-classification-scheme).

The lab distinguishes **classification recommendations** from **retention enforcement**. Updating `Retention Class` is a metadata action. These skills do not, by themselves, apply Microsoft Purview retention labels, declare records or perform disposition.

## Set up the lab

### 1. Download and inspect the materials

Download the repository and read both `SKILL.md` files. Review their names, required library and column names, references to `RDS.xlsx`, and the conditions under which the review skill can update metadata.

Review the sample workbook before using it. It should contain at least:

| Column | Purpose |
| --- | --- |
| `FunctionName` | Exact proposed retention class name. |
| `ClassDescription` | Description against which the document's business activity is compared. |
| `Local Guidance` | Optional supplementary context for an organisation or exercise. |

The sample workbook and **both** skill definitions must agree on the workbook name, worksheet and field names. The field names are literal references in the skills; they are not dynamically discovered mappings. If a workbook uses different headings, change the skill instructions accordingly (see below).

**Check the class value:** `FunctionName` is currently treated by the review skill as the exact value to write to `Retention Class`. Confirm it identifies the classification at the level you want to record. If several disposal classes share a function name, a function name alone may be too broad or ambiguous; use an appropriate uniquely identifiable class value and consistently revise the skills and associated report fields before running the experiment.

### 2. Check skill consistency before testing

Before setting up or invoking the skills, make these edits consistently in **both** `SKILL.md` files:

1. Replace `RDA.xlsx` with the supplied `RDS.xlsx` in the front matter, inputs, validation, processing steps, report templates and output checklists. Verify the worksheet name too; the review skill currently prefers a sheet called `RDA`.
2. Agree on the required workbook columns: `FunctionName` (value to return) and `ClassDescription` (text to compare), or consistently substitute different headings as explained in the next section.
3. If using the optional guidance field, change `Local Application Guidance` to `Local Guidance` everywhere the review skill reads, compares or reports it. Add any expected-column validation to the setup skill if you want the optional field checked during setup.
4. Align the result-library columns. In the uploaded setup skill these include `Proposed Retention Class` and `Human Review Required`, whereas the review skill expects `Recommended Class` and `Review Required` (plus `Retention Class Update Result`). Decide which names you want and use them consistently in library creation, report mapping and review outputs.
5. Check that source columns created by setup are actually populated by the review skill if you expect to demonstrate them. The uploaded review skill explicitly writes the source `Retention Class` for high-confidence, no-review outcomes; it does **not** explicitly instruct Copilot to populate every additional source field listed in the setup skill.
6. Test on a fresh site and verify the workbook, all libraries, fields, source updates and result Markdown rather than relying solely on Copilot's completion message.

These are **pre-publication checks**, not automatic modifications performed by this README.

### 3. Create the skills on your test SharePoint site

From the test site's **Copilot in SharePoint** chat, use the built-in skill-creation experience to create **site skills** for the setup and classification workflows. Make sure each saved skill uses the supplied Markdown instructions rather than an AI-generated approximation.

Microsoft stores site skills as Markdown files under:

```text
/Agent Assets/Skills/<skill-name>/SKILL.md
```

If the creation experience generates an initial skill definition, review and, where you have the appropriate permissions, edit its `SKILL.md` file to match the corresponding definition from this repository. Preserve the skill's Markdown format and metadata. Follow your organisation's normal change-control requirements.

Site skills run within the user's existing SharePoint permissions; they do not confer additional access or execute arbitrary custom code.

### 4. Make the sample RDS available

Place the provided `RDS.xlsx` so the ai-classification-review site skill can access it in the **Records Classification Reference** library that was create by the Lab set up skill.

If prompted do not let the setup process silently fabricate or replace an authoritative RDS. The downloadable example is intended to keep everyone's starting point consistent.

### 5. Run the setup skill

Suggested prompt:

> Set up the AI Classification Lab on this test SharePoint site. Create or validate the three lab libraries and their metadata, prepare fictional sample documents, but do not classify anything yet. Report what succeeded and what needs attention, i'll upload the `RDS.xlsx` separately.

Check that the three libraries exist, the workbook is readable and the sample files are available. Inspect the columns before running any classification.

### 6. Classify one sample document

Open **Classification Lab**, select one readable sample document and invoke the **AI Classification Review** skill in Copilot in SharePoint.

Suggested prompt:

> For the selected item, run AI Classification Review, explain the recommended class, alternatives and uncertainty, and create the report in Classification Results. Don't force a classification if the evidence is insufficient.

Copilot should report whether it completed the assessment and whether it updated source metadata. **Verify the actual SharePoint item and report** rather than assuming that a chat response means every action succeeded.

### 7. Review the result

Open the corresponding Markdown file in **Classification Results** and examine:

- The document's apparent business purpose and primary activity.
- The recommended exact class, or why no reliable recommendation was made.
- Alternative classes considered, where appropriate.
- The reported confidence level and need for human review.
- The rationale and any missing or contradictory context.
- Whether the source `Retention Class` metadata was actually updated.

In the current skill design, **High**, **Medium** and **Low** are qualitative confidence categories — **not** calibrated percentages. Source `Retention Class` is intended to be updated only for high-confidence results that do not require human review. Medium/Low or ambiguous outcomes should be left for review, not forced into a class.

## Use your own schedule or classification scheme

You are not limited to the AFDA Express V2-based sample workbook. You can also experiment with an organisation's own **retention and disposal schedule** or a **business classification scheme**, provided you are entitled to use the material and understand what its classifications represent. For a business classification scheme, treat the result as organisational classification metadata, **not** an automatically determined retention or disposal requirement.

### Map your reference columns deliberately

The uploaded classification skill currently expects the following headings in the Excel reference. These names are part of the `SKILL.md` instructions — not a one-off chat preference.

| Expected skill field | What it must contain | Example of a different workbook heading |
| --- | --- | --- |
| `FunctionName` | The **exact classification value** Copilot may recommend and write to SharePoint. Confirm that it is sufficiently specific and unambiguous. | `Class Code`, `Classification`, or `Activity` |
| `ClassDescription` | The **substantive description** of the function, activity or class against which a document's purpose is assessed. | `Scope Notes`, `Description`, or `Business Activity Description` |
| `Local Guidance` *(optional; planned name)* | Supplementary organisational context to assist interpretation without replacing or contradicting the authoritative descriptions. | `Internal Examples` or `Business Rules` |

For example, if your workbook calls its classification value `Class Code` and its descriptive text `Scope Notes`, update both skills so **every occurrence** expecting `FunctionName` uses `Class Code`, and every occurrence expecting `ClassDescription` uses `Scope Notes`. Revise the instructions specifying what exact value should be recommended and written to `Retention Class`, including the output report template.

**Telling Copilot once in chat which columns to use is not enough.** The skills contain explicit reference-field expectations, validation rules, class-selection rules and output mappings. Those instructions may override or conflict with an ad hoc prompt if left unchanged.

A practical mapping workflow:

1. Inspect your workbook and identify the worksheet, the **exact classification value**, and the descriptive text. Check for duplicate values, blank rows and cases where multiple classes share a parent function name.
2. Update the setup skill's workbook validation and field definitions; update the review skill's front matter, inputs, validation, candidate comparison, classification selection, metadata update and Markdown report template.
3. Update the workbook name, target library/path and worksheet references if they differ from `Records Classification Reference/RDS.xlsx`.
4. Decide whether the SharePoint `Retention Class` column still makes sense for the experiment, particularly if testing a non-retention business classification scheme. Change that column and all skill mappings consistently if appropriate.
5. Validate with a straightforward document and an ambiguous one; compare the returned exact values with the source workbook, not just the conversational explanation.

### Add optional Local Guidance

To explore how organisational context influences classification, add a column named **`Local Guidance`** to your Excel reference, with short, relevant guidance on individual rows. For example, you might explain that externally received event programmes held only as general reference material differ from records documenting an organisation's own event coordination, decisions or approvals — **but only if that interpretation is supportable under your schedule**.

- The guidance is **optional**: blank values are acceptable, and the core comparison still depends on the classification value and substantive class description.
- Add the exact heading to the workbook and ensure the review skill reads it, uses it *after* the authoritative class descriptions, and identifies its influence in the Markdown report.
- If you rename this field, change the name in every related instruction; the uploaded review skill currently says `Local Application Guidance`, not `Local Guidance`.
- Do not use local guidance to create unauthorised disposal classes, alter official retention requirements or simply steer the model towards a preferred answer.
- Run the same test **before and after** adding guidance and compare the recommendation, competing candidates and explanation. Record whether the guidance improved the quality of the decision, not merely whether the answer changed.

An AI-generated rationale should be treated as an explanation to evaluate, **not** proof of the model's internal thought process or proof that the assigned classification is correct.

## Experiments to try

For each exercise, **write down your expected classification before running the skill**. Then capture the actual recommendation, plausible alternatives, review status and what you learned. If you repeat a test, reset or isolate its previous outputs so the comparison is meaningful.

### Experiment 1 — The straightforward case

**Try:** A fictional document with one clear business purpose and an obvious match in the sample RDS.

**Look for:** Does the recommended class match the actual activity evidenced by the document, not just its title? Is the explanation specific enough to check against the schedule?

### Experiment 2 — The misleading filename

**Try:** Give a document a title that suggests one class while its content clearly evidences a different activity.

**Look for:** Does the skill follow the substance of the document rather than the filename? If not, where did its assessment go astray?

### Experiment 3 — Two plausible classes

**Try:** Use a document that contains multiple related activities or could reasonably match two RDS descriptions.

**Look for:** Does it compare candidates fairly, recognise uncertainty and require review where appropriate? Can you explain which evidence would resolve the ambiguity?

### Experiment 4 — Can Local Guidance change the answer?

**Try:** Run an ambiguous document, record the outcome, then add carefully worded `Local Guidance` to the relevant class, update the skills to read that column, and repeat the test.

**Look for:** Did the explanation improve? Did the recommendation change? Did the guidance clarify legitimate organisational context — or simply steer the model towards your preferred answer?

**Important:** Do not change the authoritative `FunctionName` or `ClassDescription` merely to force the outcome you want.

### Experiment 5 — Change the classification reference

**Try:** Use another appropriately authorised retention and disposal schedule **or business classification scheme**. Follow the mapping instructions above and update **both** skills to match the workbook before running the test. Start with fictional or otherwise suitable documents.

**Look for:** Does a similar document receive a different recommendation? Which differences in class descriptions or local context account for the change? Is the new recommendation supportable under the applicable schedule?

**Important:** The original *RIMPA Live 2025 event programme → Ephemeral* example discussed in the article used a **different** reference. The supplied sample RDS is **not** expected to reproduce that result.

## Record your observations

A short observation log is enough to make the experiments more useful:

| Document / experiment | My expected class | AI recommendation | Confidence | Review required? | Evidence supporting or challenging the result | What changed? |
| --- | --- | --- | --- | --- | --- | --- |
| Example 1 | | | | | | |

Try to distinguish **agreement with your expectation** from **correctness under the actual schedule**. An explanation that sounds plausible may still misinterpret the document or the reference.

## Limitations and safeguards

- **Educational, not production-ready.** This lab does not address enterprise-scale throughput, operating costs, system integration, repeatability, assurance or deployment governance.
- **Not a retention engine.** It does not apply Purview retention labels, establish legal retention periods for your organisation or authorise disposal.
- **Human judgement remains essential.** Review ambiguous and consequential cases against the authoritative RDS and organisational context.
- **Confidence is not accuracy.** High/Medium/Low represent the skill's qualitative decision rules, not measured probabilities. Do not assume that “High” means a particular percentage likelihood of being correct.
- **Rationales require scrutiny.** A generated explanation is useful for review but is not a guaranteed record of the model's internal process.
- **Permissions and capabilities apply.** SharePoint skills can only use supported Copilot in SharePoint operations and the current user's permissions. Operations can fail or be unavailable.
- **Use safe test data.** Avoid placing personal, confidential or protected records into a publicly shareable demonstration or GitHub issue. Observe your organisation's data-handling policies.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Skill isn't available | Confirm Copilot in SharePoint availability, licence, the current site, and site-skill creation/permissions. |
| Reference not found | Check library name, workbook location, filename and worksheet, including any older `RDA.xlsx` references left in either skill. |
| No classification recommended | Inspect document readability, required field names and mapping (`FunctionName` / `ClassDescription` unless deliberately changed), ambiguity and relevance of candidate classes. |
| No source metadata update | Check the confidence/review outcome, `Retention Class` field, user permissions and any reported operation error. |
| No Markdown result | Confirm **Classification Results** exists, its columns match the review skill, and the skill reported successful creation. |
| Setup and review produce different column names | Align their expected workbook, source and result fields; do not rely on a one-off prompt to reconcile differing schema instructions. |

## Modify the skills and contribute

The two skills are deliberately readable and editable. Experiment with their instructions, edge cases, evidence requirements and reporting structure, then re-run controlled test cases.

Suggestions, reproducible test observations and improvements are welcome through GitHub issues or pull requests. Please **do not include confidential documents, personal information, or third-party schedules you do not have permission to redistribute**.

If you adapt the lab, consider sharing what changed in the instructions, the reference material and the resulting assessment. Those details are often more useful than the result alone.

## Disclaimer

This repository is an independent educational demonstration, not an official Microsoft product or records management standard. Outputs must be independently assessed before use in any organisational process. Microsoft 365 licensing, Copilot in SharePoint functionality and service limits may change; refer to Microsoft's current documentation.
