# Requirement Source Fallback

Use this when the primary requirement source is incomplete, unavailable, or not machine-accessible.

## Source Priority

Use the highest-confidence source available:
1. Jira issue or epic
2. Confluence page linked from the issue
3. Local requirement, design, or architecture docs
4. User-provided text
5. Existing code behavior, only as current-state evidence and never as the requirement source by itself

## Non-Negotiable Rules

- State which authoritative source is missing
- Record the fallback source used
- Record retrieval time for every source snapshot
- Distinguish copied requirements from inferred requirements
- Do not invent acceptance criteria
- Do not treat existing code as proof of desired behavior unless the source says so

## What To Capture In The DD

Add a short provenance block:

```markdown
## Requirement Provenance
- Missing primary source:
- Fallback source used:
- Retrieved at:
- Confidence: High | Medium | Low
- Directly stated requirements:
- Inferred requirements that need review:
```

## Fallback Patterns

### Jira unavailable
- Ask for issue key export, pasted text, screenshot transcript, or linked local docs
- Record that live tracker fields such as current status or labels could not be verified

### Confluence unavailable
- Use the linked summary from Jira, local design docs, or user-provided excerpts
- Mark diagrams, rollout notes, or tables that could not be checked directly

### Only chat text is available
- Normalize the request into explicit acceptance criteria
- Mark all assumptions as pending review
- Require human approval before planning

### Source conflict
- Prefer the most recent authoritative business source
- Quote the conflict briefly in the DD
- Add an open question instead of resolving it silently

## Confidence Guide

- High: Jira or Confluence available, or exported source text is complete
- Medium: Local docs plus user confirmation cover the important behavior
- Low: Mostly reconstructed from chat or partial excerpts

Low-confidence DDs should not move into implementation until review closes the gaps.
