---
name: ai-classification-lab-setup-v2
description: |-
  Set up and validate a SharePoint learning environment for AI-assisted records classification with Copilot. Create the reference, lab, and results libraries, metadata, sample documents, and Markdown-results structure without classifying documents. The classification reference workbook is supplied separately and is never created by this skill.

  Use when the user says:
  - "set up an AI classification lab"
  - "create a records classification learning environment"
  - "prepare the classification reference and sample documents"
  - "validate or reset the AI classification lab"
---
# AI Classification Lab Setup

## When to use
Use this skill to create, configure, validate, reset, or explain a SharePoint learning environment for demonstrating AI-assisted records classification with Copilot.

Use it for setup only. Do not classify sample documents unless the user explicitly asks to run a separate classification workflow after setup.

## Inputs
- Target SharePoint site; default to the current site.
- Optional request to create, validate, reset, or explain the lab.
- A separately provided classification reference workbook for later review workflows.
- Optional user-provided sample documents or metadata requirements.

If the user doesn't provide source content, create clearly labelled fictional training material. Do not present it as an official retention schedule or real record.

## Steps
1. Inspect the target site for existing libraries, columns, and files before creating, updating, validating, or resetting anything. Reuse compliant components and don't create duplicates.
2. Create or configure these document libraries:
   - **Records Classification Reference** for reference materials supplied separately.
   - **Classification Lab** for sample documents and their later classification metadata.
   - **Classification Results** for human-readable Markdown reports and audit metadata.
3. Do not create, upload, replace, rename, or modify an `RDA.xlsx` workbook. Treat the classification reference workbook as separately provided outside this setup workflow.
4. If a reference workbook is available in the reference library, validate that it contains both `FunctionName` and `ClassDescription`. `FunctionName` is the exact class value used by later review workflows; `ClassDescription` is the authoritative semantic comparison text. If either is absent, report the workbook as incompatible for the classification-review workflow and identify the missing field. If no workbook is present, report that it must be provided separately; don't claim the lab is fully configured for classification review.
5. In **Classification Lab**, create `Retention Class` metadata plus supporting fields such as `Classification Confidence`, `Human Review Required`, `Classification Rationale`, and `Classification Status`. Use suitable types and make retention class filterable.
6. Add a small, varied set of clearly labelled fictional sample documents. Include distinct business purposes and at least one ambiguous example requiring human review.
7. In **Classification Results**, create audit metadata including `Source Document`, `Proposed Retention Class`, `Confidence`, `Human Review Required`, `Classification Status`, and `Decision Date`.
8. Create a Markdown result template or example containing source-document name and link, business-purpose summary, proposed class, alternatives, rationale and reference details, confidence and uncertainty, human-review requirement, and decision status, reviewer, and date.
9. Do not populate classification decisions during setup. Leave fields blank, `Not started`, or another clear setup-state value.
10. Validate all three libraries, required columns, any supplied reference workbook, sample documents, and the Markdown template. Report missing or partially configured components plainly. If a tool fails or returns empty, say so and don't claim the component exists.
11. For reset requests, inspect first and reset only components explicitly identified by the user. A broad request such as “recreate everything” does not authorize replacement or deletion of a separately provided reference workbook; ask for explicit authorization before changing it.

## Output format
Return both:

### Setup summary
- State whether the lab was created, updated, validated, reset, or explained.
- Link to each library, the sample-document set, and the Markdown template.
- State that the classification reference workbook is separately provided and was not created or modified.
- State the sample-document count and metadata created.

### Validation checklist
Use a checklist covering:
- Records Classification Reference exists
- A separately provided reference workbook is available, when required for classification review, and contains `FunctionName` and `ClassDescription`
- Classification Lab exists and has required metadata
- Sample documents exist and include an ambiguous review example
- Classification Results exists and has audit metadata
- Markdown classification-result template exists
- Sample documents have not been classified during setup

For failures, identify the missing item and next corrective action. Keep the response concise.

## Constraints
- Treat default content as training-only and fictional.
- Don't infer or publish official retention requirements.
- Don't create, upload, replace, rename, or modify the separately provided reference workbook unless the user explicitly requests a separate workbook-management task.
- Don't classify, assign final records classes, or overwrite user-provided reference content unless explicitly requested.
- Preserve an auditable, human-readable Markdown result format for later classification work.
