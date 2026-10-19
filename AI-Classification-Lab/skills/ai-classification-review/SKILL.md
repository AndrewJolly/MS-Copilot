---
name: ai-classification-review
description: |-
  Classify selected Classification Lab documents against Records Classification Reference/RDA.xlsx, recommend or apply an exact retention class, and create a Markdown result with populated Classification Results metadata.

  Use when the user says:
  - "classify this selected document"
  - "recommend a records classification"
  - "update the Retention Class metadata"
  - "create a classification report"
---
# AI Classification Review

## When to use
Use this skill to classify one or more selected documents from **Classification Lab** against **Records Classification Reference/RDA.xlsx**. Use it when asked to recommend a records classification, explain reasoning, update **Retention Class**, or create a Markdown classification report.

Classify from the document's business purpose, primary activity, transaction or decision evidenced, and context. Never classify from a filename, title, folder path, library name, isolated keyword, or existing metadata alone.

## Inputs
- One or more selected source documents, normally in **Classification Lab**.
- **Records Classification Reference/RDA.xlsx**, preferably worksheet **RDA**.
- Required reference fields: `FunctionName` and `ClassDescription`.
- Optional reference field: `Local Application Guidance`.
- **Classification Results** library with fields: `Source Document`, `Recommended Class`, `Confidence`, `Review Required`, `Retention Class Update Result`, and `Classification Status`.

The Classification Lab should have a single-line text field named `Retention Class`.

## Steps

### 1. Validate each selected source document
Process each selection separately. Capture its name, URL, type, library, existing Retention Class, and whether its content can be read.

Do not classify folders, document sets, links, unsupported files, unreadable files, empty files, or files with insufficient usable content. Do not force a class or update source metadata for these items. Create a result report where possible, recording why classification couldn't be completed.

### 2. Locate and validate the reference
Locate `Records Classification Reference/RDA.xlsx`. Prefer worksheet `RDA`; use another worksheet only if it contains both required fields.

Read usable rows only. Each usable row must have nonblank `FunctionName` and `ClassDescription`. Ignore explanatory, About, blank, and malformed rows. Do not modify RDA.xlsx, add classifications, rewrite descriptions, or invent missing values.

If `Local Application Guidance` is present, read its nonblank values for usable rows. Use it as supplementary organisational interpretation to resolve ambiguity or apply local rules. It must never replace, override, or become a substitute for the authority's `FunctionName` or `ClassDescription`.

If RDA.xlsx, the relevant worksheet, or either required column can't be accessed, do not use general knowledge or filenames to classify. Don't update the source document. Record the blocked outcome in the report and Results metadata.

### 3. Understand the document
Determine the document's apparent purpose, primary business function, activity, transaction or decision, intended audience, parties, process stage, evidential value, and completeness.

When several activities appear, distinguish the primary activity from supporting, incidental, and contextual references. Classify the primary transaction or activity evidenced.

### 4. Compare against RDA
Compare substantive document meaning with every plausible `ClassDescription`. Apply this order of importance:
1. Document purpose
2. Primary business activity
3. Transaction or decision evidenced
4. Meaning of the `ClassDescription`
5. Relevant `Local Application Guidance`, when present
6. Evidential value, process stage, and context
7. Title, filename, and keyword overlap

Identify at most three plausible candidates. For each, state the exact `FunctionName`, relevant `ClassDescription`, relevant local guidance if any, why it applies, and why it isn't necessarily the best match. Don't add candidates only to fill the list.

### 5. Make the recommendation and confidence decision
Recommend a class only when there is a reasonable semantic relationship to an RDA description. The recommendation must be the exact associated `FunctionName`; never abbreviate, combine, rewrite, or substitute a `ClassDescription` or local guidance.

Use High only when purpose and primary activity are clear, one class is substantially stronger, and no significant contradiction or competitor exists. Use Medium when one class is most likely but context is incomplete or an alternative has limited plausibility. Use Low when content is incomplete, the primary activity is unclear, candidates are similarly plausible, no reliable match exists, or specialist judgement is needed.

Set `Review Required` to No only for High confidence with no material ambiguity. Set it to Yes for Medium or Low confidence, multiple plausible classes, incomplete content, inaccessible reference, or consequential uncertainty.

If no reliable match exists or two classifications can't be distinguished, leave the recommendation blank, use Low confidence, require review, and don't update source metadata.

### 6. Update the source only when justified
Write the exact recommended `FunctionName` to the selected source document's `Retention Class` only when the result is High confidence and human review isn't required.

Don't overwrite an existing source value when confidence is Medium or Low, the document is unreadable, the reference is unavailable, or the classification is ambiguous. State whether the update was `Applied`, `Not applied`, `Skipped`, or `Failed`, with a short reason.

### 7. Create a Markdown result and populate Results metadata
Create one human-readable Markdown report per source document in **Classification Results**. Also populate the corresponding Classification Results library item metadata for every outcome, including completed, ambiguous, unreadable, and reference-unavailable cases.

Use these mappings:

| Field | Value |
|---|---|
| Source Document | Source document name or link |
| Recommended Class | Exact recommended `FunctionName`; blank only when no reliable recommendation exists |
| Confidence | `High`, `Medium`, or `Low` |
| Review Required | `Yes` or `No` |
| Retention Class Update Result | `Applied`, `Not applied`, `Skipped`, or `Failed`, with a short reason where useful |
| Classification Status | `Completed`, `Needs review`, `Unable to classify`, or `Reference unavailable` |

Never leave an applicable outcome field blank except `Recommended Class` when no reliable recommendation exists. Metadata and Markdown must state the same outcome.

Use `Completed` only when a reliable recommendation was made. Use `Needs review` for Medium or Low confidence, ambiguity, or incomplete content. Use `Unable to classify` for unreadable, unsupported, empty, or insufficient-content documents. Use `Reference unavailable` when RDA.xlsx or its required data can't be read.

## Output format
For each selected document, provide a concise report:

```markdown
# Classification Result — <source document name>

## Source
- Document: <name>
- Existing Retention Class: <value or blank>
- Readability: <readable / unreadable and reason>

## Assessment
- Primary business activity: <assessment>
- Recommended Class: <exact FunctionName or No reliable recommendation>
- Confidence: <High / Medium / Low>
- Human review required: <Yes / No>

## Candidate comparison
1. **<FunctionName>** — <ClassDescription>; <relevant Local Application Guidance or none>; <why it fits or does not fit>
2. **<FunctionName>** — <optional alternative and why it is less suitable>

## Local Application Guidance
- Available: <Yes / No>
- Effect: <how it affected the candidate comparison or recommendation; or not used>

## Reasoning
<Brief explanation grounded in the document's primary activity and RDA ClassDescription, including uncertainty.>

## Retention Class update
- Result: <Applied / Not applied / Skipped / Failed>
- Value applied: <exact FunctionName or none>
- Reason: <reason>

## Classification Results metadata
- Source Document: <value>
- Recommended Class: <value or blank>
- Confidence: <value>
- Review Required: <value>
- Retention Class Update Result: <value>
- Classification Status: <value>
```

For an inaccessible reference, unreadable document, or no reliable match, clearly state that no classification was forced, no source metadata was updated, and human review is required. If a tool fails or returns empty, say so plainly and don't invent a result.
