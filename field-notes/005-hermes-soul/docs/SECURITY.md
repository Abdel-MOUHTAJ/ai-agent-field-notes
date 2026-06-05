# Security

## Security Posture

Hermes SOUL is local-first and documentation-first. It does not require public logs, cloud calls, account disclosure, or secret exposure.

The observed prompt-size and prompt-inspection workflow was offline and did not require a network call.

## No Secrets In Documentation

Public documentation must not include:

- API keys;
- tokens;
- credentials;
- passwords;
- private identifiers;
- private account names;
- long raw logs;
- raw prompt dumps that contain private data.

## Private Path Redaction

Use neutral path examples:

```text
~/.hermes/SOUL.md
docs/...
<local workstation>
<private home>
<project-root>
```

Do not publish full private local paths.

## Human Validation At Critical Boundaries

The operator must explicitly validate actions involving:

- secrets;
- passwords;
- API keys;
- tokens;
- sensitive personal data;
- deletion;
- irreversible modification;
- destructive action;
- payment;
- external accounts;
- cloud services;
- public publication;
- legal decisions;
- security decisions;
- ambiguous authority.

## Local-First Reasoning

Local-first does not mean risk-free. It means the method prefers local files, local audits, local prompt inspection, and local validation records before any public claim.

## Documentation As Governance

Documentation quality is a governance control because it prevents accidental overclaiming. It also protects the operator by separating observed facts from assumptions.

Every public document should answer:

- What was verified?
- What was not verified?
- What is out of scope?
- What private data was removed?
- What requires human validation?

Signature sentence: security starts when the documentation refuses to publish what the agent should protect.
