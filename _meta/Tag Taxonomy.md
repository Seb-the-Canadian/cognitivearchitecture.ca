---
created: 2025-10-15
last_tended: 2026-01-30
type: effort
tags: [meta, metadata]
up:
  - "[[cognitivearchitecture_ca]]"
---
## Status-Based Publication Tags

| Status     | Description                                                                                                                                                                                                     |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| #sprout    | Early published thinking - concepts that are emergent.                                                                                                                                                          |
| #sapling   | Developing published content - work that I'm seeing more connection in and have nurtured beyond its early stages, the result of noticing some patterns in my thinking or where my curiosity starts to take off. |
| #evergreen | Stable published content, long-form thoughts as well as structural notes for the garden.                                                                                                                        |
## Activity/Lifecycle Tags
| Canonical Tag | Aliases                              | Description                                    | Status |
| ------------- | ------------------------------------ | ---------------------------------------------- | ------ |
| #tending      | active, working, developing          | Currently being actively worked on             | active |
| #dormant      | stable, static, archived             | Not currently in active development            | active |
| #connecting   | linking, relating, synthesizing      | Actively seeking connections to other notes    | active |
| #reviewing    | evaluating, assessing, transitioning | Under evaluation for status or content changes | active |
### Activity Tag Usage Guidelines

### #tending
- **Use When**: Note is receiving regular attention, frequent updates expected
- **Combine With**: Content tags relevant to what's being developed
- **Duration**: Remove when note reaches stable state or work pauses
- **Example**: tags: [knowledge-work, tending]
### #dormant
- **Use When**: Note is complete enough for current purposes, infrequent changes
- **Combine With**: Any content tags, especially for reference materials
- **Duration**: Persistent state, remove when active work resumes
- **Example**: tags: [meta, dormant]
### #connecting
- **Use When**: Actively seeking relationships with other notes or concepts
- **Combine With**: Content tags to indicate connection domains
- **Duration**: Remove when sufficient connections are established
- **Example**: tags: [philosophy, ai, connecting]
### #reviewing
- **Use When**: Evaluating note for status change, major revision, or archiving
- **Combine With**: Current content tags
- **Duration**: Temporary state, remove after review completion
- **Example**: tags: [data-culture, reviewing]

---
## Content Tags
| Canonical Tag           | Aliases                                        | Description                                           | Status |
| ----------------------- | ---------------------------------------------- | ----------------------------------------------------- | ------ |
| #knowledge-work         | knowledge-architecture, cognitive-architecture | Systems and practices for intellectual labor          | active |
| #data-culture           | data-literacy, data-fluency                    | Organizational data capabilities and practices        | active |
| #ai                     | artificial-intelligence, AI, machine-learning  | Artificial intelligence applications and implications | active |
| #digital-transformation | digitization, tech-adoption                    | Organizational technology change initiatives          | active |
| #governance             | oversight, policy, framework                   | Governance structures and decision-making systems     | active |
| #capability-development | skill-building, training, enablement           | Human capability and competency development           | active |
| #human-capability       | human-centered, human-first                    | Human-centered approaches to technology               | active |
| #infrastructure         | systems, architecture, platform                | Technical and organizational infrastructure           | active |
| #philosophy             | theory, conceptual, thinking                   | Philosophical foundations and conceptual work         | active |
| #concept                | definition, idea, framework                    | Conceptual definitions and frameworks                 | active |

## Domain-Specific Tags
| Canonical Tag | Aliases                        | Description                               | Status |
| ------------- | ------------------------------ | ----------------------------------------- | ------ |
| #about        | bio, personal, author          | Personal and biographical information     | active |
| #publish      | publication, release, public   | Content publication and sharing processes | active |
| #audit        | review, assessment, evaluation | Evaluation and assessment content         | active |

---
## Tag Formatting Rules

- **Case**: Always lowercase
- **Separators**: Use hyphens, not underscores or spaces
- **Scope**: Prefer specific over generic (e.g., #knowledge-work over #work)
- **Consistency**: Use singular forms unless plural is more natural
- **Activity Tags**: Use present participle forms for lifecycle states ( #tending not #tend)

---

%%
## Tag Lifecycle Process

### Adding New Tags
1. **Need Assessment**: Is there sufficient content (5+ notes) to warrant a new tag?
2. **Category Check**: Does it fit existing structural/content/activity categories?
3. **Name Check**: Does it conflict with existing tags or aliases?
4. **Activity Consideration**: Is this better served by an activity tag?
5. **Update Documentation**: Add to appropriate table above
### Deprecating Tags
1. **Usage Analysis**: Review actual usage vs. intended purpose
2. **Migration Path**: Define clear replacement (tag, status, or removal)
3. **Batch Update**: Change all affected notes simultaneously
4. **Archive**: Move to Deprecated Tags table with clear migration notes
### Tag Consolidation
When multiple tags serve similar purposes:
1. **Semantic Analysis**: Which name better captures the concept?
2. **Usage Patterns**: Which has more established, consistent usage?
3. **Alias Strategy**: Convert less-used tag to alias of primary
4. **Content Audit**: Ensure no meaning is lost in consolidation
---
## Quality Guidelines

### Tag Selection Criteria
- **Discoverable**: Would someone reasonably search for this term?
- **Consistent**: Applied consistently across similar content?
- **Specific**: Narrow enough to be useful for filtering?
- **Persistent**: Likely to remain relevant over time?
- **AI-Friendly**: Clear semantic meaning for automated processing?
### Anti-Patterns to Avoid
- **Over-tagging**: More than 6-8 tags per note reduces effectiveness
- **Temporal Tags**: Avoid year/date tags (use created field instead)
- **Redundant Tags**: Don't duplicate information in status/navigation fields
- **Personal Tags**: Avoid tags that only make sense to you
- **Micro-Tags**: Avoid hyper-specific tags used on only 1-2 notes
## Review Schedule
- **Monthly**: Review activity tags for stale assignments
- **Quarterly**: Assess tag usage analytics and consolidation opportunities
- **Semi-Annually**: Full deprecated tag cleanup
- **Annually**: Complete taxonomy review for strategic alignment
## Implementation Notes
- **Linter Integration**: Configure Linter to enforce lowercase, hyphenated format
- **Activity Tag Rotation**: Regularly review and update activity tags during note maintenance
- **Cross-Reference**: Always check navigation fields when assigning content tags
- **Migration Priority**: Handle deprecated tags before adding new ones
%%