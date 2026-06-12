# 007 - Context Engineering for Codex CLI

Status: MVP 7

This note documents a governed Codex CLI workspace with one canonical spine,
reversible derived views, and human validation as the final authority.

It is the seventh note in the `ai-agent-field-notes` series and is published
as a GitHub-ready operating document derived from the validated ULTIMA mission
report and the final playbook for the Context Engineering chantier on NUMENOR.

Source reports:

- [ULTIMA mission report](../OUTPUTS/ultra-rapport-context-engineering-codex-cli-2026-06-12.md)
- [Final playbook](../OUTPUTS/context-engineering-playbook-final-2026-06-12.md)

Default license recommendation: MIT, unless Mahonheim chooses another
license. This is not legal advice.

## Tested Environment

- Windows 11 local Codex workspace on NUMENOR
- Canonical recovery chain present: `START_HERE.md`, `AGENTS.md`,
  `rules/MEMORY_GOVERNANCE.md`, `tasks/last_session.md`,
  `tasks/last_session.json`
- Mission 2 capture and Vortex promotion already validated in the source
  workspace
- Publication target: `Abdel-MOUHTAJ/ai-agent-field-notes`

## Security Notice

This note contains no secrets, tokens, credentials, or private operational
data. It describes a governed workflow, not a live secret-bearing system.

Any future publication or update to the repository should remain
validation-gated and should never widen scope beyond the approved note
content.

## Executive Summary

The project packages a governed Codex CLI operating model for Context
Engineering. The core idea is simple:

- keep one canonical spine;
- derive all other views from that spine;
- validate durable decisions explicitly;
- use Vortex as navigation, not as an authority layer;
- keep Git as proof.

The practical win is that Codex can recover quickly, keep context explicit,
and publish readable operational documentation without turning the workspace
into a hidden second canon.

## Problem Statement

Long-running Codex work degrades when a workspace depends on:

- stale conversation memory;
- unstructured context;
- ambiguous recovery paths;
- too many derived notes;
- promotion without traceability;
- a knowledge layer that becomes noisy or authoritative by accident.

This note solves that by separating recovery, capture, promotion, and proof.

## Method

The workflow used to produce the source material was:

1. Bootstrap the workspace from local canonical files.
2. Read the canonical recovery chain before any project-state judgment.
3. Capture substantive work with Mission 2 markers.
4. Promote only durable knowledge into Vortex.
5. Verify the health and divergence state locally.
6. Keep human validation as the final authority.

## Result

The resulting operating model is a governed, GitHub-friendly document that:

- explains how recovery works;
- explains how capture works;
- explains how promotion works;
- explains why Vortex stays non-sovereign;
- gives a clear publication-ready summary of the Context Engineering chantier.

## Lessons Learned

1. Canonical evidence beats conversation memory.
2. Human validation matters more than apparent automation.
3. Derived views are useful only if they are reversible.
4. Git proof matters when durable claims are being made.
5. A small, explicit operating model is easier to maintain than a broad
   narrative doc.

## Sanitization / Governance

- No secrets or credentials are included.
- No hidden hooks are required.
- No durable decision is asserted without validation.
- No local absolute path is required for the public version.
- The note should remain focused on workflow, governance, and reproducibility.

## Final Verdict

This MVP is ready for publication as a public field note.

It is concise enough to use, strict enough to trust, and specific enough to
audit.

## Signature Sentence

Context Engineering for Codex CLI works when the workspace stays governed,
the canon stays singular, and every durable decision remains human-validated.
