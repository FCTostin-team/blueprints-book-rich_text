# Contributing Guide

First off, thanks for investing your time into this project. If you’re here, you’re already helping us keep the blueprint tooling fast, reliable, and actually useful for the Factorio builder crowd.

This document is the contributor playbook for `blueprints-book-rich_text`: how to ask questions, report issues, shape enhancements, and ship PRs that get merged without unnecessary back-and-forth.

## Introduction

We welcome contributions from everyone: bug hunters, feature builders, docs contributors, and folks doing cleanup/refactors.

What we value most:

- Reproducible bug reports.
- Small, focused pull requests.
- Respectful collaboration.
- Code that preserves existing behavior unless a change is intentional and documented.

Please also review [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## I Have a Question

If your topic is **usage/help/support**, please do **not** open a GitHub Issue for that.

Issues are reserved for:

- Verified bugs
- Actionable enhancement proposals
- Concrete engineering tasks

For usage questions and troubleshooting, use community channels:

- FCTostin Telegram chat
- FCTostin YouTube comments/community threads
- Other relevant Factorio/dev chats you use with your team

When asking, include context: what you tried, expected result, and current result.

## Reporting Bugs

High-signal bug reports get fixed faster. Before opening a new issue:

1. Check existing issues to avoid duplicates.
2. Confirm the bug on the latest repository state.
3. Prepare a minimal reproduction case.

Use this report structure:

- **Title**: short and specific (`Decode fails on blueprint book with custom icons`)
- **Environment**:
  - OS and version
  - Browser and version
  - Project commit hash or branch
  - Any extensions/security settings that may affect clipboard/storage
- **Steps to Reproduce**:
  1. Exact input used (or redacted safe sample)
  2. Exact sequence of actions
  3. Where behavior diverges
- **Expected Behavior**: what should happen
- **Actual Behavior**: what currently happens
- **Artifacts**: screenshots, console logs, and stack traces

Bug reports without reproducible steps are likely to stall.

## Suggesting Enhancements

Feature requests are welcome, but they need engineering context.

A strong enhancement proposal includes:

- **Problem statement**: what pain point exists today?
- **Use cases**: real scenarios where this helps.
- **Proposed behavior**: what should users see/do?
- **Scope estimate**: small tweak vs architectural change.
- **Compatibility notes**: does it impact existing decode/encode flows?

If the feature changes UX significantly, include mockups or rough interaction notes.

## Local Development / Setup

### 1. Fork and Clone

```bash
# Fork on GitHub first, then:
git clone https://github.com/<your-username>/blueprints-book-rich_text.git
cd blueprints-book-rich_text
```

### 2. Create a Working Branch

```bash
git checkout -b feature/your-change-name
```

### 3. Install Dependencies

No package manager install is required for base runtime.

The app is static and uses CDN-hosted dependencies.

### 4. Configure Environment

No `.env` file is required by default.

If you introduce configuration, document it in `README.md` and keep defaults safe.

### 5. Run Locally

```bash
# Option A: direct open
open index.html   # macOS

# Option B: local static server (recommended)
python -m http.server 8080
# Visit http://localhost:8080
```

## Pull Request Process

### Branch Naming

Use clear branch names:

- `feature/<short-description>`
- `bugfix/<issue-or-topic>`
- `docs/<short-description>`
- `refactor/<short-description>`

### Commit Messages

Use **Conventional Commits**:

- `feat: add blueprint import validation`
- `fix: handle malformed book metadata gracefully`
- `docs: rewrite readme getting-started section`
- `refactor: split icon parsing helpers`

### Sync With Upstream

Before opening a PR, sync your branch with the latest main branch and resolve conflicts locally.

### PR Description Requirements

Your PR description should include:

- Summary of what changed
- Why the change is needed
- Linked issue(s), e.g. `Closes #42`
- Testing evidence (commands + results)
- Screenshots/GIFs for UI changes

Keep PRs focused. Massive mixed-purpose PRs are hard to review and often delayed.

## Styleguides

### Code Style

- Keep JavaScript clear and modular where possible.
- Prefer small pure functions for transformation logic.
- Avoid hidden side effects in encode/decode paths.
- Preserve existing naming conventions unless there is a strong reason to refactor.

### Linting and Formatting

This repo does not currently enforce dedicated lint/format tooling in CI.

If you introduce ESLint/Prettier or other tools:

- Keep config minimal.
- Document commands in `README.md`.
- Avoid style-only churn unrelated to the task.

### Architecture Expectations

- Keep the app static-first and browser-friendly.
- Avoid introducing backend coupling unless discussed first.
- Treat decode/encode correctness as a critical path.

## Testing

Any code change should include validation.

Baseline checks:

```bash
# JavaScript syntax check
node --check script.js

# Manual smoke test via local server
python -m http.server 8080
```

For functional updates, verify at minimum:

- Blueprint decode works
- JSON edit + re-encode works
- Blueprint book decode/edit/re-encode works
- Clipboard/export interactions still function

If your change makes testing easier, adding lightweight test scaffolding is welcome.

## Code Review Process

- Maintainers review incoming pull requests.
- At least one maintainer approval is expected before merge.
- Critical-path changes may require additional review/testing passes.

When receiving review feedback:

1. Address comments directly in follow-up commits.
2. Reply to each thread with what changed.
3. Keep discussion technical, concise, and respectful.

If you disagree with feedback, explain the tradeoff and propose an alternative instead of silently ignoring the comment.

Thanks again for contributing and helping keep this tool battle-ready.
