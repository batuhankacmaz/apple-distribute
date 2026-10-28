# Apple Distribute

An agent skill for reviewing iOS App Store and TestFlight submission readiness against current Apple requirements.

Use it for a full pre-submission audit, a focused policy question, or a response to App Review feedback. It checks live Apple sources, traces the relevant app behavior, and reports confirmed issues alongside evidence still needed.

## What it covers

- Build completeness, actual build SDK/toolchain evidence, and supported devices.
- Privacy disclosures, manifests, permissions, tracking, and runtime AI data sharing.
- Login requirements, account deletion, and reviewer access.
- Purchases, subscriptions, restore flows, and storefront-specific payment rules.
- Remote configuration, feature switches, experiments, and remotely selected paywalls.
- Listing assets, age suitability, user-generated content, and health or fitness claims where applicable.

The review distinguishes Apple requirements from engineering recommendations. Static searches are evidence to investigate; they cannot establish that a purchase, consent, or deletion flow works. Account-side and runtime checks remain unverified when access is unavailable.

## Install in Codex

Ask Codex:

```text
$skill-installer Install the apple-distribute skill from https://github.com/batuhankacmaz/apple-distribute
```

Or clone the skill into your personal skills directory:

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/batuhankacmaz/apple-distribute.git ~/.agents/skills/apple-distribute
```

Start a new Codex chat after installation. If that directory already contains a copy, review it before replacing or updating it. See the [official skills documentation](https://learn.chatgpt.com/docs/build-skills) for supported installation locations.

Other agents that support the Agent Skills format can load [SKILL.md](SKILL.md) using their own installation mechanism.

## Usage

Run the skill from the app repository with a request such as:

```text
Use $apple-distribute to review this app before its next App Store submission.
Prioritize confirmed blockers and list the account-side checks you cannot verify.
```

```text
Use $apple-distribute to review our remote feature flags and paywall experiments.
Explain which behaviors need to be accessible to App Review.
```

```text
Use $apple-distribute to investigate this rejection notice against the current
Apple guidelines. Cite the relevant rules and propose the smallest practical fix.
```

The agent needs read access to safe project source and access to the web for current Apple policy. Xcode or device access is needed only for checks that depend on builds or runtime behavior. The skill has no bundled scripts or package dependencies.

## Review output

Findings use **Confirmed issue**, **Needs verification**, **Verified**, or **Not applicable**, with the rule, observed behavior, evidence, impact, and proposed action. Reports can use the bundled [submission report template](templates/submission-report.md).

A review does not upload a build, submit an app, accept agreements, change signing, or change live feature flags. It does not guarantee App Store approval.

## Contents

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Review workflow and evidence standards. |
| [Remote configuration review](references/remote-config-review.md) | Feature switches, remote content, experiments, and reviewer visibility. |
| [Policy snapshot](references/policy-snapshot-2026-10-28.md) | Dated Apple policy reference with primary sources. |
| [Submission report template](templates/submission-report.md) | Findings, verification, unknowns, and suggested review notes. |

The policy snapshot was checked on **28 October 2026**. The skill requires refreshing time-sensitive rules from Apple at each review. Older local validation scripts and examples are excluded from this public package because their assumptions do not match the current workflow.

## Contributing

Keep guidance portable and changes focused. Cite primary Apple sources for policy changes, distinguish requirements from recommendations, and update dated claims only after verifying them. Follow [AGENTS.md](AGENTS.md) for repository checks. Do not include app source, credentials, signing material, or real review-account details in examples or issues.

## License

[MIT](LICENSE), copyright 2026 batuhankacmaz. This is an independent project and is not affiliated with Apple or OpenAI.
