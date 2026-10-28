# Apple policy snapshot

Verified: **2026-10-28**. Latest App Review Guidelines revision found: **2026-10-16**. This is a dated working reference; check live sources for later changes.

## October 16, 2026 changes

Apple's [change announcement](https://developer.apple.com/news/?id=92th7e5i) identifies these review changes:

| Area | Change | Review action |
| --- | --- | --- |
| 2.5.19 | Dedicated rule for hidden, dormant, or undocumented functionality, previously covered by 2.3.1. Apple describes this as clarification of existing policy. | Inspect feature switches and release-only behavior using the remote configuration reference. |
| 2.3.14 | New creative-asset guideline. | Include product-page headers and search creative in listing reviews. |
| 1.2 | Clarified scope of content safeguards and consequences for failing to address violations. | Assess applicability before adding moderation findings. |
| 3.1.1(a) | External-purchase-link wording and entitlement references revised. | Check current storefront-specific permissions and permitted destinations. |
| Section 5 | Clarified removal and alternative-distribution blocking for apps facilitating trafficking or child exploitation. | Apply when relevant to the app's capabilities. |

Apple's [enforcement explanation](https://developer.apple.com/news/?id=vvzx6cul) specifically addresses behavior concealed during review and exposed after approval, and safeguards against nonconsensual intimate imagery, including AI-generated imagery. Do not turn that explanation into an invented blanket ban on remote configuration.

## Current rules most likely to affect ordinary iOS apps

The following are concise requirements from the [live guidelines](https://developer.apple.com/app-store/review/guidelines/), followed by review implications:

- **2.3.1(a):** Describe new features and product changes specifically in review notes and make them accessible to reviewers.
- **2.5.2:** Downloaded executable code must not introduce or change functionality outside permitted exceptions.
- **2.5.19:** Hidden, dormant, or undocumented features are prohibited.
- **5.1.2(i):** Clearly disclose third-party personal-data sharing and obtain explicit permission before it occurs, including third-party AI sharing.
- **4.8:** Qualifying social login requires an equivalent privacy-preserving login option, subject to exceptions.
- **1.4:** Physical safety and medical accuracy claims receive scrutiny.

These requirements do not mandate a public raw-config screen, a particular configuration vendor, or a universal removal of feature flags. Audit their effects and reviewability. Treat maintenance controls, experiments, remote text, content updates, and changes to product functionality according to their actual behavior.

The AI-sharing clarification dates to [November 13, 2025](https://developer.apple.com/news/?id=ey6d8onl), not the October 2026 update. That announcement also added age-restriction requirements for applicable creator content and software offered outside the binary. Do not apply these categories automatically to an ordinary native fitness app.

## Submission requirements already effective

Source: [Apple's requirements page](https://developer.apple.com/news/upcoming-requirements/).

| Effective date | Verified requirement | Evidence to inspect |
| --- | --- | --- |
| 2026-04-28 | Uploaded apps need Xcode 26 or later and the applicable platform's version 26 SDK or later. | Actual build/archive metadata; this does not require an iOS 26 deployment target. |
| 2026-09-09 | iOS/iPadOS uploads must target iOS 13 or later. | Release deployment settings, separately from build SDK. |
| 2026-01-31 | Updated age-rating questionnaire responses were due to avoid update-submission interruption. | Current App Store Connect answers; refresh for subsequently added questions. |
| 2025-02-17 | EU availability requires verified trader-status information where applicable. | Account-side distribution evidence. |
| 2024-05-01 | Listed required-reason API use needs approved reasons. | App and SDK privacy manifests in the submission. |

Use [the current SDK requirements](https://developer.apple.com/support/third-party-SDK-requirements/) to identify SDKs needing manifests and, for applicable binary dependencies, signatures. A manifest's presence alone does not prove its declarations match runtime collection. Do not treat public Firebase client configuration values as server credentials.

## Purchases, assets, and account-side updates

- [EU changes announced August 18, 2026](https://developer.apple.com/news/?id=gmws0jgp) took effect October 1, 2026. Review applicable payment options, child-safety conditions, business terms, and commissions. A payment integration must be assessed per distribution arrangement; do not reuse a global "external digital payments are always forbidden" check.
- [Asset guidance](https://developer.apple.com/app-store/asset-best-practices/) distinguishes brand/content creative from screenshots and app previews. Creative must represent the app and suit all audiences; avoid unsupported claims and specific or discounted prices. Screenshots and app previews still demonstrate actual use. Record which asset type was inspected.
- [October 13, 2026 agreement changes](https://developer.apple.com/news/?id=17mwd36z) include security requirements and subscription terms. Check whether the account has a pending agreement; accepting legal terms is outside a read-only audit.
- Use [complete-review guidance](https://developer.apple.com/help/app-review/before-submitting-for-review/complete-review) for tested-device information, service dependencies, regional differences, and appropriate demo access, including an expired-subscription account when needed to review the purchase flow. Keep credentials out of the audit report.

## Review interpretation examples

These are practical review heuristics, not additional Apple rules:

- Bundled AI-made tutor videos do not by themselves show runtime transmission of user data to an AI provider. Trace actual network flows before alleging missing AI consent.
- A pain-relief promise, before/after image, or treatment claim needs closer substantiation review than a general description of gentle exercise.
- Missing server configuration or App Store Connect access leaves a material unknown; source inspection cannot certify the live experience.
- Proposed fixes should address observed behavior. Do not delete an entire remote-configuration integration merely because a switch exists.
