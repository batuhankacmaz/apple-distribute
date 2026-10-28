---
name: apple-distribute
license: MIT
description: Review iOS App Store or TestFlight submission readiness against current Apple rules, including remote feature switches, privacy, purchases, metadata, and reviewer access. Use for pre-submission audits, policy updates, or rejection follow-up.
metadata:
  version: "2.0.0"
  author: batuhankacmaz
  policy_verified: "2026-10-28"
---

# Apple Distribute

Produce an evidence-backed submission review with actionable findings. Adapt the depth to a full audit, a focused concern, or rejection feedback. A policy question alone does not authorize app changes or submission.

## Policy freshness

At each review, check Apple's live [App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/), [latest announcements](https://developer.apple.com/news/), and [submission requirements](https://developer.apple.com/news/upcoming-requirements/). Cite the applicable rule and date; distinguish new changes, clarified existing policy, and older obligations. If browsing fails, identify the unverified policy areas rather than claiming current compliance.

Read [the dated policy snapshot](references/policy-snapshot-2026-10-28.md) for the verified October 2026 changes and supporting sources. Refresh any time-sensitive requirement before relying on it.

## Scope and protected files

- Follow repository instructions, including code intelligence tools when available. Identify the intended app, release target, build, distribution channel, and storefronts from available context.
- Review source, public metadata, safe configuration, and existing build evidence. Do not publish, upload, accept agreements, change live flags, or modify signing as part of an audit.
- Exclude protected files before content searches: production/staging environment files, credentials/service-account JSON, GoogleService-Info variants, certificates, provisioning profiles, and private keys. Repository exclusions take precedence. Never print tokens or demo passwords into reports.
- Use explicit file-type allowlists and exclude dependencies, generated output, and build caches. A public client identifier is not automatically a leaked secret; classify findings by actual sensitivity.

## Review workflow

1. Establish applicable features and gather evidence. Reuse available context before asking questions. Missing App Store Connect or device evidence is an unverified check, not an automatic failure.
2. Review remote behavior using [remote-config-review.md](references/remote-config-review.md) whenever server responses, feature flags, experiments, or remote paywalls affect the app. This is also part of a full audit.
3. Inspect the applicable areas below. Trace important flows through to visible behavior; a symbol match is only a lead.
4. Run appropriate read-only checks and relevant existing tests. Report exactly what was run. Inspect any project-provided helper before executing it against a real project.
5. Present prioritized findings and unresolved evidence using [the report template](templates/submission-report.md). Draft review notes when useful, without inventing credentials or untested behavior.

## Applicable review areas

### Build and completeness

Verify the SDK/toolchain used for the submitted build, separately from its minimum deployment target. Prefer archive/build metadata such as DTSDKName and DTXcodeBuild; the locally selected Xcode alone does not prove how an existing binary was built. Refresh current minimums from Apple.

Check launch stability, working links/services, actual user-visible placeholders, offline/error behavior, and supported devices, including compact iPad layouts where applicable. TODO comments, placeholder identifiers, and absence of a standalone Info.plist are not by themselves submission blockers. Modern generated Info.plist and launch-screen settings need contextual inspection.

### Privacy and AI

Map data from collection to storage and recipients, including analytics, purchases, crash reporting, and AI providers. Compare runtime behavior, permission strings, the privacy policy, App Store privacy labels, and privacy manifests. Verify required-reason declarations and applicable SDK signatures against Apple's current SDK list.

For third-party AI, inspect the consent flow and what is transmitted before consent. Distinguish bundled content created with AI during development, on-device processing, and runtime sharing of personal data. Only the last establishes the third-party AI data-sharing concern; other applicable privacy obligations still need review.

Check tracking based on actual cross-company tracking behavior; neither an analytics import nor ordinary first-party analytics alone establishes an ATT requirement. Account deletion, privacy labels, consent, and manifests are separate checks.

### Accounts and login

Evaluate actual login options and current Guideline 4.8 exceptions. An auth SDK import or email/password login alone does not prove social-login obligations. Sign in with Apple is one way to meet the qualifying privacy-preserving login requirement.

For apps supporting account creation, trace the in-app deletion initiation through backend removal and user confirmation, including automatic/guest accounts where applicable. Deactivation and logout do not establish deletion. Inspect Sign in with Apple token revocation if relevant, plus effects on active subscriptions. See [Apple's deletion guidance](https://developer.apple.com/help/app-review/guideline-reference/5-1-1-account-deletion).

### Purchases and subscriptions

Review the actual StoreKit 2, StoreKit 1, or purchase-provider integration, including RevenueCat when used. Do not require SKPaymentTransactionObserver in a StoreKit 2 implementation or a .storekit testing file for App Store approval.

Exercise purchase, restore, cancellation, pending, error, and entitlement-recovery paths as applicable. Inspect displayed price, billing period, trial eligibility, post-trial charge, renewal terms, legal links, and ongoing subscription value. Compare remote paywall claims to store product data. See [Apple's subscription guidance](https://developer.apple.com/app-store/subscriptions/).

Evaluate external checkout and links against the actual storefront, distribution model, entitlements, and current terms. An external payment SDK is not proof of a violation; a blanket global prohibition is inaccurate. Do not infer entitlement eligibility from a locale or device language.

### Listing, content, and health claims

Review each asset by its type: screenshots, app previews, and the new creative assets have different purposes. Use [Apple's asset guidance](https://developer.apple.com/app-store/asset-best-practices/). Inspect whether the listing represents shipped behavior, supported purchases, rights, and age suitability. Review claims in onboarding and paywalls as well as the listing.

For fitness/health products, examine physical safety and claims about pain, treatment, measurements, or guaranteed results. Identify when specialist evidence or regulatory documentation may be needed; do not label a general exercise app as a regulated medical device solely because it discusses wellness. A disclaimer does not validate an unsupported claim.

Apply user-generated content and creator-content safeguards only when those capabilities exist. Trace reporting, filtering, blocking, and moderation responses where relevant; inspect age restrictions when content can exceed the app rating. Development-time AI artwork alone does not create a user-generated content platform.

### Reviewer access and account-side requirements

Prepare concrete navigation steps, external-service dependencies, regional differences, and access to purchase flows. Inspect reviewer access without creating a misleading reviewer-only product. Use [Apple's complete-review guidance](https://developer.apple.com/help/app-review/before-submitting-for-review/complete-review).

Check available evidence for current age-rating answers, EU trader status where relevant, agreements, and storefront availability. Do not read private signing material to check expiration; mark unavailable signing evidence explicitly.

## Evidence and reporting

- Use **Confirmed issue**, **Needs verification**, **Verified**, and **Not applicable**. State the rule, observed behavior, file/line or runtime evidence, impact, and smallest practical fix for each finding.
- Separate recommendations from Apple requirements. Static text searches cannot prove consent, complete deletion, working restore, moderation quality, or remote configuration currently served.
- Lead with confirmed blockers and material unknowns. Do not use a percentage score or guarantee approval. An inaccessible account-side setting must remain unverified.
- Save a report when requested or useful within an authorized location; otherwise give the review in chat. Preserve existing reports. Do not require a long manual questionnaire before reporting completed work.
