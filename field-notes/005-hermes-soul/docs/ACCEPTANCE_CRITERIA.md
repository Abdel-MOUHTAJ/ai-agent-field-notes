# Acceptance Criteria

"Status: these criteria define the publication gate; validated items must be checked only after review."

## File-Level Validation

- [x] The target identity file is identified before modification.
- [x] `SOUL.md` is confirmed as the observed primary identity file.
- [x] The adapted charter is present in `SOUL.md`.
- [x] Required markers appear in `SOUL.md`.
- [x] The process does not write into display-only configuration fields.

## Prompt-Level Validation

- [x] Prompt inspection runs offline.
- [x] The final system prompt for a fresh session contains the same markers.
- [x] The validation summary avoids raw prompt dumps.
- [x] Evidence distinguishes file presence from prompt presence.

## Restart Behavior

- [x] The documentation states that the initial behavior test did not fully reflect the new personality.
- [x] The documentation states that behavior aligned after restart.
- [x] The workflow treats restart as part of observed validation.
- [x] The docs avoid claiming every runtime requires or avoids restart.

## GitHub Readability

- [x] README can be understood in under two minutes.
- [x] Headings use a clear hierarchy.
- [x] Paragraphs stay compact.
- [x] Internal links are relative.
- [x] Repository layout matches created files.

## Privacy Protection

- [x] No real person names appear.
- [x] No personal account names appear.
- [x] No full private paths appear.
- [x] No secrets, API keys, tokens, credentials, or private identifiers appear.
- [x] No long raw logs appear.

## Scope Boundaries

- [x] The project is framed as a case study and operational specification.
- [x] The project does not claim package status.
- [x] The project does not claim universal compatibility.
- [x] Unverified points appear as limitations or future work.

## Mermaid Renderability

- [x] Diagrams use GitHub-compatible `flowchart TD` or `stateDiagram-v2`.
- [x] Node labels avoid unsupported syntax.
- [x] Diagrams explain architecture, lifecycle, validation, or governance.
- [x] Diagrams are not decorative.

## Final Status Markers

- [x] `HERMES_SOUL_INJECTED=1`
- [x] `HERMES_FINAL_PROMPT_MARKERS_PRESENT=1`
- [x] `HERMES_PERSONALITY_CHARTER_V0_1_ACTIVE_FOR_FRESH_SESSION=1`
- [x] `HERMES_ACTION_FIRST=1`
- [x] `HERMES_TERMINAL_UBUNTU_PROTOCOL=1`
- [x] `HANDOFF_COMPLETE=1`

Signature sentence: acceptance means the method is readable, private, scoped, and verifiable.
