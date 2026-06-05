# Product

## What Hermes SOUL Is

Hermes SOUL is a documentation MVP for a minimal personality layer in local AI agents. It describes a reproducible pattern built around a primary identity file named `SOUL.md`.

The project is a public-facing case study and operational specification. It does not ship runtime code, package installers, hosted services, or universal adapters.

## What It Solves

Hermes was already operational. It had a CLI, persistent memory, built-in memory provider, profile files, configuration, and a security guidance plugin. It still lacked a formal identity layer.

Hermes SOUL solves the documentation and operating-method problem: how to make agent personality explicit, audit-friendly, and verifiable without confusing display settings with prompt identity.

## Who It Is For

Hermes SOUL is for:

- local agent operators;
- maintainers who need auditable identity changes;
- documentation owners writing public case studies;
- teams that want prompt-layer governance without claiming a full framework.

It is not for users who need a plug-and-play runtime package.

## Why A Personality Layer Matters

A local agent can run commands, use memory, and expose tools while still acting like a generic assistant. A personality layer defines how the agent should work: role, tone, action style, safety rules, security posture, memory discipline, continuity, and closure.

For Hermes, the validated personality emphasized action-first behavior, governed memory, safety and security, explicit validation at critical boundaries, continuity, and an Ubuntu terminal protocol.

## Minimal Viable Personality Layer

In operational terms, a minimal viable personality layer has:

- one primary identity surface;
- an adapted charter;
- searchable markers;
- file-level validation;
- prompt-level validation;
- restart-aware behavioral validation;
- documentation of scope and limits.

## What Was Validated

The observed case validated:

- `SOUL.md` is the primary identity file in the observed runtime;
- `SOUL.md` replaces the default identity and loads automatically;
- an adapted charter can be copied into `SOUL.md`;
- markers can confirm file-level presence;
- offline prompt inspection can confirm final prompt presence;
- behavior aligned with the charter after restart.

## Out Of Scope

Hermes SOUL does not validate:

- every local agent runtime;
- every memory provider;
- every Hermes deployment;
- hosted execution;
- package installation;
- automatic mutation of identity files.

Signature sentence: Hermes SOUL is a method for proving identity injection, not a claim that every runtime behaves the same way.
