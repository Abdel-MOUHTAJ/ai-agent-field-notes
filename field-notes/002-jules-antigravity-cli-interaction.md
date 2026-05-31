# Project Tesla Field Note — MVP 2

## Making Google Jules Actually Report Back Through Antigravity CLI

**From remote diff generation to governed agent interaction**

Author: **Abdellah MOUHTAJ**  
Professional title: **Ops Consultant — AI Agents, CLI Workflows & Local Governance**

Tagline:

> Testing, stabilizing, and documenting real-world AI agent integrations: bridging the gap between experimental tools and secure, governed developer workflows.

Status: **MVP 2 field documentation — sanitized public version**

---

## Tested Environment

| Item | Value |
|---|---|
| Field validation date | 2026-05-28 |
| Machine | Ubuntu workstation |
| OS | Ubuntu 24.04.4 LTS |
| Local workspace | Antigravity CLI project, codename `Tesla` |
| Local project root | `/home/[USERNAME]/antigravity-workspace` |
| GitHub repository | Dedicated private repository |
| Jules CLI version observed | `v0.1.42` |
| GitHub CLI version observed | `gh 2.45.0` |

---

## Important Security Notice

This document is a **sanitized field note**.

It intentionally omits:

- OAuth callback links
- one-time authorization codes
- tokens
- private credentials
- raw logs
- secret files
- personal local paths that are not required to reproduce the integration pattern

---

## 1. Executive Summary

The first MVP proved that Google Jules could be connected to a local Antigravity CLI workflow through GitHub.

That was necessary.

But it was not enough.

Once Jules was connected, the next operational question became more important:

> Can I actually interact with Jules through the Antigravity CLI workflow in a usable, auditable, and governed way?

In other words:

- Can Jules receive a real task?
- Can Jules create a remote session on the correct repository?
- Can I retrieve the result without applying it automatically?
- Can Jules report what it did?
- Can the local Antigravity CLI workflow display that report without speaking in Jules’ place?
- Can apply, commit, push, and merge remain under explicit human control?

This second MVP documents the transition from:

> “Jules is connected.”

to:

> “Jules can participate in a governed remote-agent workflow.”

Final validated pattern:

- Jules receives a bounded mission.
- Jules creates a remote session on the intended GitHub repository.
- The local workflow retrieves the result in read-only mode.
- The local repository remains unchanged until explicit apply.
- Jules writes its own report inside the delivered result.
- The local interface displays the raw Jules-authored result.
- Apply, commit, push, and merge remain separate human-controlled steps.

The key lesson:

> A remote AI coding agent is not operationally useful if it only produces a diff. It must also report back clearly.

---

## 2. Why MVP 1 Was Not Enough

The first MVP solved the infrastructure problem.

It validated:

- Jules Web access;
- GitHub App repository authorization;
- Jules CLI repository visibility;
- local Git remote configuration;
- GitHub CLI authentication;
- first controlled push;
- local wrapper governance;
- Git porcelain-based cleanliness checks.

That MVP was about connection and trust boundaries.

The second MVP starts after that.

The new question was not:

> Can Jules see the repository?

The new question was:

> Can Jules work in a real controlled loop with Antigravity CLI?

Connecting an agent is one thing.

Interacting with it safely is another.

---

## 3. Target Interaction Model

The desired model was:

Mermaid diagram, plain text version for safe drafting:

    flowchart TD
        A[Human Operator] --> B[Local Antigravity CLI Workflow]
        B --> C[Governed Jules Wrapper]
        C --> D[Jules Remote Session]
        D --> E[Read-only Result Retrieval]
        E --> F[Local Audit]
        F --> G{Human Validation}
        G -->|Approved| H[Apply Patch]
        H --> I[Commit]
        I --> J[Push]
        G -->|Rejected| K[Do Not Apply]
        B -. supervises .-> C
        C -. no auto-merge .-> J
        C -. no autonomous push .-> J
        F -. inspect before apply .-> G

Governance principle:

- Jules is a delegated remote agent.
- The local workflow remains the operational supervisor.
- The local Git repository remains the source of controlled truth.
- The human operator remains the final decision-maker.

---

## 4. First Real Jules Mission: The Smoke Test

The first real mission was intentionally minimal.

The objective was to create exactly one documentation file.

Expected file:

    docs/JULES_SMOKE_TEST.md

Expected markers:

    JULES_REAL_SMOKE_TEST=1
    ONLY_DOCS_FILE_EXPECTED=1
    NO_MEMORY_CHANGE_REQUESTED=1
    NO_SECRET_ACCESS_REQUESTED=1
    NO_MAIN_PUSH_REQUESTED=1
    Done_By=Jules
    MAIN_RENDUE_A_MAHONHEIM=1

This was not designed to test Jules’ coding ability.

It was designed to test the remote-agent workflow:

- mission creation;
- remote execution;
- result retrieval;
- local audit;
- controlled apply;
- controlled commit;
- controlled push.

The task was deliberately small because the governance model mattered more than the output complexity.

---

## 5. Problem 1 — Wrong Repository Resolution

The first attempt failed.

The error pattern was:

    the repo unknown/Antigravity either doesn't exist on GitHub or is not connected to Jules

This was a critical discovery.

Jules did not correctly resolve the local project as the intended GitHub repository.

The local wrapper was relying on an implicit repository reference.

The result was:

    unknown/Antigravity

instead of the intended GitHub repository.

This was not the original GitHub App permission issue anymore.

It was a command and wrapper issue.

The repository needed to be passed explicitly.

---

## 6. Solution 1 — Use the Explicit Repository

The fix was to stop relying on implicit local repository resolution.

Conceptual correction:

Before:

    jules remote new --repo . --session "..."

After:

    jules new --repo "OWNER/REPOSITORY" "bounded mission prompt"

Result:

- Jules created the remote session on the intended repository.
- The previous `unknown/Antigravity` failure was resolved for mission creation.
- The local repository remained unchanged.
- No apply, commit, or push happened automatically.

Lesson:

> For governed AI-agent workflows, do not rely on local folder inference when the remote agent must operate on a GitHub repository. Pass the repository explicitly.

---

## 7. First Positive Result — Remote Session Created

After the explicit repository fix, the real smoke mission successfully created a Jules remote session.

The session completed.

The result could be retrieved in read-only mode.

The proposed diff created only the expected file:

    docs/JULES_SMOKE_TEST.md

The file contained the expected safety markers.

The local repository remained unchanged until the operator explicitly allowed apply.

After audit, the patch was applied, committed, and pushed through separate controlled steps.

This proved the first real end-to-end Jules flow:

    mission
    remote session
    completed result
    read-only retrieval
    audit
    explicit apply
    targeted commit
    controlled push

But another problem remained.

Jules had produced a file.

Jules had produced a diff.

The interaction was still not good enough.

---

## 8. Problem 2 — A Diff Is Not a Conversation

After the smoke test, the main weakness became obvious.

Jules had completed the task, but the local interface did not yet provide a clear operational answer from Jules.

The human operator still needed to reconstruct:

- what Jules did;
- which file Jules created;
- whether Jules respected the constraints;
- whether anything else was touched;
- what the next human decision should be.

That is not acceptable for a professional workflow.

A remote agent should not only generate a patch.

It should report back.

The problem was not execution.

The problem was interaction quality.

---

## 9. Design Decision — The Local Workflow Must Not Speak for Jules

One possible solution would have been to create a local command that summarized Jules’ result.

This was rejected.

Why?

Because the local supervisor must not pretend to be Jules.

If the report is authored locally, accountability becomes unclear.

The correct model is:

- Jules writes its own report in the delivered result.
- The local workflow retrieves the result.
- The local workflow displays the raw Jules-authored result.
- The local workflow does not rewrite or simulate Jules’ response.
- The human operator audits and decides.

This preserves accountability.

Jules signs what Jules did.

The local workflow supervises.

The human validates.

---

## 10. Test 2 — Asking Jules to Report in Its Result

A second test was created.

Objective:

Ask Jules to create a documentation file that includes both:

1. technical markers;
2. a clear human-readable report to the local workflow.

The goal was to test whether Jules could write its own operational report inside the result it delivered.

This was a conceptual shift.

Instead of only asking:

> Create a file.

The mission asked:

> Create a file and include your own report inside it.

This pattern is important because it allows the local interface to display Jules’ output without speaking on Jules’ behalf.

---

## 11. Problem 3 — Boundary Weakness in the First Report Attempt

The first self-report attempt showed promise, but it was not accepted as the final pattern.

Jules produced a report.

However, the report claimed that Jules had read or used files outside the intended ultra-bounded scope, including governance or memory-related files.

Even if no sensitive content was exposed, this was not acceptable for the test objective.

The mission was supposed to be narrow.

The reported scope was too broad.

Decision:

> Do not integrate this result as final.

Reason:

A governed workflow must not only look at what changed.

It must also look at what the agent claims it read, used, or relied on.

This is a crucial lesson.

In AI-agent workflows, output files are not the only audit surface.

The agent’s own report is also an audit surface.

---

## 12. Problem 4 — Sensitive-Term Filter Blocked the Next Prompt

The next attempt tried to be more explicit about what Jules must not touch.

The prompt mentioned sensitive or restricted areas directly.

The local wrapper blocked the mission before it reached Jules.

The block was intentional.

The wrapper detected sensitive terms and returned a fail-closed signal.

This was not a Jules failure.

It was the local governance layer working as designed.

The issue was more subtle.

A human may write:

> Do not read secrets.

But a simple fail-closed filter may only see the word:

> secrets

It cannot reliably infer whether the mention is an instruction to avoid something or an attempt to access something.

This creates a design challenge.

Security filters must be strict enough to block dangerous prompts.

But they must also eventually distinguish between:

- unsafe access requests;
- negative safety instructions;
- documentation;
- governance language.

For this MVP, the decision was:

> Do not weaken the wrapper immediately.

Instead, rewrite the mission using a positive allowlist.

---

## 13. Solution 2 — Positive Allowlist Prompting

The successful solution was to avoid naming sensitive areas in the mission prompt.

Instead of saying:

> Do not read X, Y, Z.

The mission used a positive allowlist:

- create only one file;
- use only the content needed for that file;
- do not modify anything else;
- report only on the requested task;
- include the required markers;
- return a self-contained report.

This allowed the mission to pass through the wrapper without weakening the security layer.

The broader pattern:

> When working with strict local governance wrappers, prefer positive allowlists over long lists of sensitive forbidden terms.

Positive allowlist prompting is cleaner, safer, and easier to audit.

---

## 14. Final V2 Pattern — Jules Writes Its Own Report

The final successful V2 test asked Jules to create one documentation file containing its own report.

Expected file:

    docs/JULES_INTERFACE_RESPONSE_TEST_V2.md

Expected content pattern:

- technical markers;
- session status;
- what Jules did;
- files created or modified;
- files not read or touched beyond the allowed scope;
- safety confirmation;
- result;
- next action for the human operator;
- final verdict;
- signature by Jules.

The result validated the desired model.

Jules wrote its own report.

The local workflow could display the raw result.

The local workflow did not speak on behalf of Jules.

The delivered file confirmed:

    JULES_INTERFACE_RESPONSE_TEST_V2=1
    ONLY_DOCS_FILE_EXPECTED=1
    JULES_WRITES_OWN_REPORT_IN_RESULT=1
    TESLA_DISPLAYS_RAW_JULES_RESULT=1
    NO_MEMORY_READ_REQUESTED=1
    NO_MEMORY_CHANGE_REQUESTED=1
    NO_SECRET_ACCESS_REQUESTED=1
    NO_MAIN_PUSH_REQUESTED=1
    Done_By=Jules
    MAIN_RENDUE_A_MAHONHEIM=1

This was the important MVP 2 result.

Not that Jules could create a file.

That was already known.

The important result was:

> Jules could report back in a governed, auditable way.

---

## 15. Read-Only Retrieval Rule

A new operational rule was validated.

After a mission is explicitly requested by the human operator, the local workflow may retrieve the Jules result in read-only mode and display it.

This does not require a second explicit validation.

Why?

Because read-only retrieval does not modify the local repository.

It only allows the operator to inspect the agent’s output.

Allowed automatically after an explicit mission request:

- list sessions;
- retrieve Jules result without apply;
- display raw result;
- inspect proposed diff;
- inspect Jules-authored report.

Still forbidden without explicit validation:

- apply patch;
- modify local files;
- git add;
- commit;
- push;
- merge;
- git pull;
- auto-merge.

This separation improves usability without weakening control.

---

## 16. Apply / Commit / Push Remain Human-Controlled

The final workflow deliberately separates four stages:

1. Mission creation
2. Read-only result retrieval
3. Local apply
4. Commit and push

Only read-only retrieval can be automatic after a human-requested mission.

Everything that changes durable state remains under explicit validation.

This matters because it prevents the agent workflow from collapsing into uncontrolled automation.

The human operator remains responsible for the final state of the repository.

The local Git history remains intentional.

No autonomous push to main is allowed.

No auto-merge is allowed.

---

## 17. Final Validated Workflow

The validated MVP 2 workflow is:

1. Human operator requests a bounded Jules mission.
2. The local wrapper sends the mission with an explicit GitHub repository.
3. Jules creates a remote session.
4. Jules completes the session.
5. The local workflow retrieves the result in read-only mode.
6. The local workflow displays the raw Jules-authored result.
7. The human operator audits the diff and the report.
8. The human operator explicitly validates apply.
9. The patch is applied locally.
10. The human operator audits the local change.
11. The human operator explicitly validates commit and push.
12. Git history records the change.

Final governance markers:

    READONLY_DISPLAY_AUTO_ALLOWED=1
    JULES_WRITES_REPORT_IN_OWN_RESULT=1
    TESLA_DISPLAYS_RAW_RESULT=1
    APPLY_REQUIRES_EXPLICIT_VALIDATION=1
    COMMIT_REQUIRES_EXPLICIT_VALIDATION=1
    PUSH_REQUIRES_EXPLICIT_VALIDATION=1
    MERGE_REQUIRES_EXPLICIT_VALIDATION=1

---

## 18. Problems / Solutions / Results Matrix

| Problem | Cause | Solution | Result |
|---|---|---|---|
| Jules mission resolved to `unknown/Antigravity` | Implicit local repository resolution | Pass the GitHub repository explicitly | Remote session created on intended repository |
| Jules produced a diff but not a clear interaction | The result lacked a Jules-authored report | Ask Jules to write its own report inside the delivered file | The local interface could display the raw report |
| The local workflow risked becoming Jules’ voice | A local summary would blur accountability | Display the raw Jules-authored result | Clear responsibility: Jules reports, local workflow supervises, human validates |
| First report attempt appeared too broad | Jules claimed it used files outside the ultra-bounded scope | Reject that result and create stricter V2 mission | Stronger boundary discipline |
| Sensitive-term filter blocked a safety prompt | Wrapper detected sensitive terms without semantic interpretation | Use positive allowlist prompting | Mission passed without weakening the wrapper |
| Read-only retrieval was too friction-heavy | Retrieval was treated too similarly to apply | Allow read-only retrieval after explicit mission request | Better usability without durable modification |
| Risk of uncontrolled local modification | Remote result could be applied too quickly | Separate read-only retrieval, apply, commit, and push | Human-controlled repository state |

---

## 19. Command Patterns

Public warning:

The following commands are conceptual and sanitized.

Replace placeholders before use.

Do not publish private repository URLs, session URLs, tokens, credentials, or raw authentication logs.

Check connected repositories:

    tesla-jules repos

List remote sessions:

    tesla-jules sessions

Create a bounded mission:

    tesla-jules mission "Create exactly one documentation file and include a Jules-authored report in the result."

Retrieve a result in read-only mode:

    tesla-jules pull SESSION_ID

Apply only after explicit validation:

    jules remote pull --session SESSION_ID --apply

Audit local changes:

    git status --short --branch --untracked-files=all
    git diff --stat
    git diff --check

Commit only expected files:

    git add EXPECTED_FILE
    git commit -m "docs: add Jules result"

Push only after final validation:

    git push origin main

---

## 20. Recommended Jules Mission Template

Use this type of structure for future governed missions:

    You are Jules acting as a delegated remote agent.

    Mission:
    Create exactly one file:
    docs/EXAMPLE_RESULT.md

    Scope:
    Only create or modify the file explicitly listed above.

    Required report:
    Inside the delivered file, include a section named:

    JULES_RESPONSE_TO_TESLA

    That section must explain:

    - what you did;
    - which file you created or modified;
    - which limits you respected;
    - whether you changed anything else;
    - what the human operator should do next.

    Required markers:

    ONLY_EXPECTED_FILE_CHANGED=1
    JULES_WRITES_OWN_REPORT_IN_RESULT=1
    TESLA_CAN_DISPLAY_RAW_RESULT=1
    NO_MAIN_PUSH_REQUESTED=1
    NO_AUTO_MERGE_DONE=1
    Done_By=Jules
    MAIN_RENDUE_A_MAHONHEIM=1

    Do not push to main.
    Do not merge.
    Do not request secrets.
    Do not perform any action outside the allowed file.

Note:

In strict wrapper environments, prefer positive allowlists over long lists of sensitive forbidden paths.

---

## 21. Security Model

The security model did not change.

This MVP 2 did not remove governance.

It improved interaction while preserving control.

Security rules:

- Jules is a delegated remote agent.
- The local workflow remains the supervisor.
- The local repository remains authoritative.
- Human validation remains mandatory for durable changes.
- Read-only retrieval is allowed after an explicit mission request.
- Apply is not automatic.
- Commit is not automatic.
- Push is not automatic.
- Merge is not automatic.
- Sensitive paths and secrets must not be exposed.
- Raw authentication artifacts must not be published.
- Session URLs should not be republished without review.

Public documentation rule:

> Publish the pattern, not the secrets.

---

## 22. Lessons Learned

1. **Connection is not interaction.**

MVP 1 proved that Jules could be connected.

MVP 2 proved that Jules could become usable in a governed loop.

2. **Do not trust implicit repository resolution.**

Remote agents should receive the repository explicitly when the workflow depends on GitHub-backed execution.

3. **A diff is not enough.**

A professional AI-agent workflow needs a clear agent-authored report.

4. **The agent must report in its own result.**

If the local workflow writes the report for Jules, accountability becomes blurred.

5. **Read-only retrieval should be easier than apply.**

Inspecting a result should not require the same level of friction as modifying local state.

6. **Apply, commit, and push must remain separate.**

Each durable step must remain human-controlled.

7. **Positive allowlists are safer than long negative prompts.**

Strict wrappers may block sensitive terms even when used in safety instructions.

8. **Agent self-reports are audit material.**

The report should be audited just like the diff.

9. **Reject imperfect agent outputs.**

The first successful-looking report was not integrated because its declared boundaries were not clean enough.

10. **Governance is what makes experimental agents operational.**

The value is not only that Jules can work.

The value is that Jules can work inside a controlled process.

---

## 23. Public-Facing Summary

In the first MVP, I documented how I connected Google Jules to a local Antigravity CLI workflow through GitHub.

In this second MVP, I tested the next question:

> Can Jules actually interact with the local workflow in a useful and governed way?

The answer is yes, but only after solving several practical issues.

The first real mission failed because Jules resolved the repository as `unknown/Antigravity`.

The fix was to pass the GitHub repository explicitly.

Then Jules successfully produced a remote result, but a new weakness appeared:

> A diff alone is not enough.

The agent must also report what it did.

The final pattern was:

- Jules writes its own report inside its delivered result.
- The local workflow retrieves and displays that raw result.
- The local workflow does not speak on behalf of Jules.
- Read-only retrieval is allowed after a human-requested mission.
- Apply, commit, push, and merge remain under explicit human control.

This turns Jules from a connected remote tool into a governed remote-agent workflow.

---

## 24. Final Conclusion

This MVP 2 proves that a Google Jules + Antigravity CLI integration can go beyond authentication and repository visibility.

It can support real remote-agent interaction.

But the workflow only becomes operationally credible when it includes:

- explicit repository targeting;
- bounded missions;
- read-only result retrieval;
- Jules-authored reports;
- local audit;
- human-controlled apply;
- human-controlled commit;
- human-controlled push;
- no autonomous merge;
- no uncontrolled access to sensitive context.

Final principle:

> Connection is infrastructure. Interaction is workflow. Governance is what makes the workflow safe.

---

## 25. Call to Action

I am documenting real-world failure modes and stabilization patterns for emerging AI developer tools.

This second MVP focuses on what happens after the agent is connected:

- How do we make it report back?
- How do we keep local control?
- How do we separate inspection from execution?
- How do we avoid turning agent workflows into uncontrolled automation?

If you are testing Jules, Antigravity CLI, GitHub-backed AI agents, or local governance wrappers, I would be glad to compare notes.

Let’s build reliable runbooks for AI-agent operations.

---

## Sanitization Checklist

This public field note intentionally avoids publishing:

- OAuth URLs;
- one-time authorization codes;
- access tokens;
- API keys;
- private repository URLs;
- private session URLs;
- private local paths;
- raw authentication logs;
- secret files;
- unredacted screenshots;
- private cache/state directories;
- internal transcripts.

The purpose is to publish the reproducible operational pattern, not private operational material.
