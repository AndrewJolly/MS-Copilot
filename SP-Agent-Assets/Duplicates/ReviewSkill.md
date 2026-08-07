````markdown
# Duplicate Content Assessment Skill

## Name

duplicate-content-assessment

---

## Description

Analyses SharePoint, OneDrive, Teams, file share, migration inventory, content assessment and storage analysis data to identify, categorise, and explain potential duplication patterns within an information estate.

This skill does not automatically determine what content should be deleted.

Instead, it helps users understand:

- Where duplication may exist
- What type of duplication is present
- Why duplication may exist
- Whether duplication is intentional or accidental
- The risks associated with removing duplicate content
- Opportunities to improve information governance
- Potential impacts on migrations, search, storage optimisation and AI readiness

This skill should be used whenever users ask to:

- Find duplicate files
- Identify duplicate content
- Assess duplication prior to migration
- Reduce storage consumption
- Consolidate content repositories
- Identify content quality issues
- Assess Copilot readiness
- Locate potential Single Sources of Truth
- Understand why duplicate content exists
- Determine whether duplicate content can be safely removed

---

## Purpose

The purpose of this skill is to support informed decision-making regarding duplicate content.

Duplicate content should not be treated solely as a technical issue. Duplication often exists because of business requirements, compliance obligations, user behaviour, system architecture, operational processes, or information management practices.

The skill must help users understand duplication through multiple perspectives:

- Information Governance
- Information Architecture
- Records Management
- Compliance and Regulatory Requirements
- Business Operations
- Search and Findability
- Storage Optimisation
- Content Ownership
- Data Quality
- AI and Copilot Readiness

The skill must never assume that all duplicates should be removed.

---

## Guiding Principles

### Principle 1: Duplicates Exist for Different Reasons

Not all duplicates are accidental.

Some duplicates exist intentionally to support:

- Compliance
- Business operations
- Data resilience
- Accessibility
- System performance
- Records management
- Legal requirements

### Principle 2: Context Matters

The same duplicate may be low risk in one context and high risk in another.

The skill must always consider:

- Business purpose
- Ownership
- Usage patterns
- Governance requirements
- Regulatory obligations

### Principle 3: Risk-Based Assessment

Assessment effort should be proportional to risk.

The skill should focus attention on duplicates that may cause:

- Conflicting decisions
- Information confusion
- Regulatory breaches
- Poor customer outcomes
- AI grounding issues
- Search quality degradation

### Principle 4: Deletion Is Not the Goal

The goal is not total duplicate elimination.

The goal is:

- Understanding duplication
- Reducing harmful duplication
- Improving information quality
- Improving information governance
- Supporting better business outcomes

---

# Duplicate Classification Framework

When analysing content, classify findings into one of the following duplicate categories.

---

## Type 1: Exact Duplicates

### Description

Files with identical content, file names and metadata.

### Examples

- Multiple copies of the same report
- Duplicate migration outputs
- Repeated file copies stored in separate folders

### Typical Causes

- User copying behaviour
- Poor file management practices
- Historical migrations

### Recommended Treatment

- Review for business value
- Consolidate where appropriate
- Establish authoritative copy

### Risk Rating

Low

---

## Type 2: Content Duplicates with Different Metadata

### Description

Files containing identical content but differing metadata.

### Examples

- Same document stored in multiple locations
- Same content with different modified dates
- Same document owned by different teams

### Typical Causes

- Cross-team sharing
- Relocation of content
- Multiple repository structures

### Recommended Treatment

- Compare metadata
- Identify authoritative version
- Review usage patterns before consolidation

### Risk Rating

Low to Medium

---

## Type 3: Near Duplicates

### Description

Files that are substantially similar but not identical.

### Examples

- Draft versions
- Minor revisions
- Presentations tailored for different audiences

### Typical Causes

- Collaboration
- Independent editing
- Project development lifecycle

### Recommended Treatment

- Assess business significance of differences
- Validate version history
- Determine whether multiple versions remain necessary

### Risk Rating

Medium

---

## Type 4: Logical or Functional Duplicates

### Description

Files that serve the same purpose despite existing in different formats or structures.

### Examples

- PDF and Word versions of the same document
- Spreadsheet and PDF outputs containing equivalent information
- Published and working versions of a report

### Typical Causes

- Accessibility requirements
- Publishing processes
- Audience-specific consumption needs

### Recommended Treatment

- Retain where required
- Define authoritative source
- Improve publishing governance

### Risk Rating

Medium

---

## Type 5: Duplicate Names with Different Content

### Description

Files sharing the same name but containing different information.

### Examples

- Budget2026.xlsx existing in multiple locations
- BusinessPlan.docx owned by separate business units

### Typical Causes

- Decentralised content ownership
- Inconsistent naming practices
- Parallel work activities

### Recommended Treatment

- Investigate business context
- Review ownership
- Improve naming standards

### Risk Rating

High

---

## Type 6: Redundant Backup Copies

### Description

Duplicates intentionally retained for backup or recovery purposes.

### Examples

- Weekly backup snapshots
- Archived exports
- Recovery copies

### Typical Causes

- Business continuity requirements
- Disaster recovery procedures

### Recommended Treatment

- Validate retention requirements
- Review backup schedules
- Remove copies that exceed approved retention periods

### Risk Rating

Low

---

## Type 7: Systematic or Structural Duplicates

### Description

Duplicates intentionally created to support system functionality, replication, performance, or resilience.

### Examples

- Geographic replicas
- System-generated copies
- Replicated datasets

### Typical Causes

- Platform architecture
- High availability requirements
- System integration processes

### Recommended Treatment

- Document ownership and purpose
- Review governance controls
- Avoid removal without technical validation

### Risk Rating

Medium to High

---

## Type 8: Unintentional User-Created Duplicates

### Description

Duplicates created accidentally through daily user behaviour.

### Examples

- Downloaded copies
- Email attachment copies
- OneDrive synchronisation copies
- Repeated saving into different locations

### Typical Causes

- User habits
- Limited awareness
- Convenience-based behaviours

### Recommended Treatment

- Promote better file sharing practices
- Consolidate where practical
- Improve user education

### Risk Rating

Low

---

## Type 9: Compliance or Regulatory Duplicates

### Description

Copies retained to meet legal, contractual, regulatory or policy obligations.

### Examples

- Contracts retained in multiple business locations
- Legal record copies
- Audit copies

### Typical Causes

- Regulatory requirements
- Policy obligations
- Records management controls

### Recommended Treatment

- Preserve as required
- Validate retention requirements
- Ensure controlled management

### Risk Rating

Very High

---

# Decision Framework

Before recommending remediation, evaluate the following questions.

### Governance Questions

1. Why does this duplicate exist?
2. What purpose does it serve?
3. Who owns the content?
4. Is there an authoritative version?
5. Does an approved Single Source of Truth exist?

### Operational Questions

6. Is the duplicate causing confusion?
7. Is the duplicate being actively used?
8. Are users relying upon separate copies?
9. Would removal affect business processes?

### Compliance Questions

10. Is retention required?
11. Is the duplicate part of a compliance process?
12. Is the duplicate required for legal or regulatory purposes?

### Information Quality Questions

13. Does the duplicate create conflicting information?
14. Does it introduce search noise?
15. Does it undermine content trustworthiness?

### AI Readiness Questions

16. Could Copilot retrieve conflicting content?
17. Are multiple versions competing for authority?
18. Are stale or superseded copies present?
19. Is ownership unclear?
20. Could duplication affect response quality?

---

# AI and Copilot Readiness Assessment

When duplicate content is identified, assess potential impacts on AI quality.

Consider whether duplication may contribute to:

- Retrieval of outdated information
- Multiple competing versions
- Conflicting business guidance
- Ambiguous ownership
- Stale content exposure
- Poor search relevance
- Reduced trust in AI-generated responses

Where applicable, identify opportunities to:

- Establish authoritative content locations
- Reduce obsolete content
- Improve metadata quality
- Improve ownership accountability
- Improve content lifecycle management

---

# Storage Optimisation Assessment

When the user's primary objective is reducing storage consumption, assess:

### Version Growth

Evaluate whether excessive version history may contribute more to storage consumption than duplicate files.

### Content Redundancy

Identify:

- Obsolete content
- Trivial content
- Exact duplicates
- Legacy migration artefacts

### Governance Opportunities

Consider:

- Version retention limits
- Lifecycle policies
- Archived content
- Unused workspaces

The skill should explain that storage reduction may be achieved more effectively through version management than aggressive duplicate removal.

---

# Single Source of Truth Assessment

Where possible, identify:

- Potential authoritative repositories
- Master content locations
- Published content sources
- Records repositories

Highlight opportunities to establish or strengthen:

- Single Sources of Truth
- Publishing processes
- Content ownership models
- Information governance controls

---

# Output Structure

Return findings using the following format.

```markdown
# Duplicate Content Assessment

## Executive Summary

Summarise the overall duplication landscape.

## Key Findings

### Finding 1

Duplicate Type:
Risk Level:
Business Impact:
Recommended Action:

### Finding 2

Duplicate Type:
Risk Level:
Business Impact:
Recommended Action:

## Potential Single Sources of Truth

Identify authoritative content locations.

## Governance Considerations

Describe governance implications.

## AI and Copilot Considerations

Describe impacts on search, retrieval and AI grounding.

## Storage Optimisation Opportunities

Identify version management and storage reduction opportunities.

## Areas Requiring Business Validation

Highlight findings requiring business review.

## Final Recommendation

Provide a balanced risk-based recommendation.
```

---

# Important Constraints

The skill must:

- Never recommend deletion solely because content appears duplicated.
- Never assume all duplicates are problematic.
- Always explain why duplication may exist.
- Always consider governance, compliance and operational context.
- Apply a risk-based assessment approach.
- Prioritise understanding before remediation.
- Treat duplicate identification as an information management challenge rather than purely a technical problem.

The objective of this skill is not to eliminate duplication. The objective is to help organisations understand duplication, reduce associated risk, improve information quality, and make informed governance decisions.
````
