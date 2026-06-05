# Validation

## Validation Goal

The validation goal was to prove that the adapted personality charter reached runtime behavior through the correct identity path.

The observed workflow succeeded at three levels:

- file-level validation;
- prompt-level validation;
- behavioral validation after restart.

## Config Audit

The audit found a `personality` field under display settings in `~/.hermes/config.yaml`.

That field was not retained as the injection point. The documentation treats it as a false lead because display configuration is not the same as prompt identity.

## Code Audit

The code audit showed that `SOUL.md` is the primary identity file. It also showed that `SOUL.md` replaces the default identity and loads automatically.

This audit established the correct injection surface.

## Injection Point Decision

The winning decision was to inject the adapted charter into:

```text
~/.hermes/SOUL.md
```

The display-only configuration field was left alone.

## Adapted Charter Injection

The personality content came from an adapted public charter. It was not copied raw.

The local charter emphasized:

- action-first behavior;
- governed memory;
- safety and security;
- explicit validation at critical boundaries;
- continuity;
- Ubuntu terminal protocol.

## File-Level Evidence

Marker strings confirmed that the adapted charter was present in `SOUL.md`.

Representative markers:

```text
HERMES_PERSONALITY_CHARTER_V0_1
HERMES_ACTION_FIRST
HERMES_TERMINAL_UBUNTU_PROTOCOL
HANDOFF_COMPLETE
```

## Prompt Inspection

Offline prompt inspection confirmed that the same markers were present in the final system prompt for a fresh session.

The prompt-size and prompt-inspection workflow did not require a network call.

## Restart Requirement

An initial behavior test did not fully reflect the new personality.

After restart, behavior aligned with the charter. The documentation therefore treats restart-aware validation as part of the observed method.

## Successful Final Status

```text
HERMES_SOUL_INJECTED=1
HERMES_FINAL_PROMPT_MARKERS_PRESENT=1
HERMES_PERSONALITY_CHARTER_V0_1_ACTIVE_FOR_FRESH_SESSION=1
HERMES_ACTION_FIRST=1
HERMES_TERMINAL_UBUNTU_PROTOCOL=1
HANDOFF_COMPLETE=1
```

## Evidence Handling

This public validation page summarizes evidence. It does not publish raw private logs, real names, full private paths, secrets, tokens, or private identifiers.

Signature sentence: the method works because it checks the file, the prompt, and the restarted behavior.
