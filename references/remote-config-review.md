# Remote configuration and feature switches

Use for backend-driven settings, Firebase Remote Config, custom config endpoints, experiments, remotely selected paywalls, and remotely delivered content. Verify current [Guidelines 2.3.1(a), 2.5.2, and 2.5.19](https://developer.apple.com/app-store/review/guidelines/), plus [Apple's October 16 explanation](https://developer.apple.com/news/?id=vvzx6cul).

## Policy distinction

Remote configuration is not categorically banned. The concern is whether it conceals, introduces, or materially misrepresents app behavior. Apple does not prescribe removing the configuration SDK or displaying every internal setting to users. Make the actual feature clear and reviewable.

The steps below are audit techniques and design recommendations. They are not a separate Apple-mandated architecture.

## Build an inventory

Locate the configuration client/model, bundled defaults, persistence, activation timing, server response schema, and consumers. Follow repository graph-first instructions when tools are available; otherwise use narrow source searches. Example search terms: RemoteConfig, AppConfig, featureFlag, enabled, experiment, variant, offering, paywall, maintenance, minimumVersion, reviewMode.

Restrict searches to safe source/documentation types. Do not read protected environment or Firebase configuration files. Do not retrieve production payloads or log user-specific responses just to fill this table.

For relevant entries, record:

| Key/source | Visible behavior | Default/cache/offline state | Audience or condition | How reviewers reach it | Finding/evidence |
| --- | --- | --- | --- | --- | --- |

Include information shown or hidden, purchase behavior, data sharing, permissions, deep links, and alternate navigation. A value named "enabled" or "review" is only a lead; inspect its consumers before deciding its meaning.

## Trace meaningful differences

- Compare release behavior with test/debug behavior. Look for account, receipt, date, network, region, or environment checks that change which product is shown. Distinguish legitimate sandbox billing and test infrastructure from concealment.
- Follow a disabled route into the feature implementation. Determine whether it is an already reviewed feature temporarily unavailable, an unfinished feature, or a new capability waiting for activation. Flag shipping dormant unreviewed functionality; propose exclusion from the release or review of the completed feature.
- Compare server-selected paywalls and text to the store products, actual feature access, and required consent. A remotely supplied true/false value must not stand in for the user's permission.
- Inspect meaningful variants for review access. Document intended differences and navigation in review notes; do not create a misleading reviewer-only experience or a hidden bypass.
- Inspect remote WebViews and scripts separately from plain data/content. Remote lesson JSON and videos do not by themselves establish downloaded executable code. Software offered outside the binary may require a different analysis under Guideline 4.7.

## Example judgments

| Observed behavior | Appropriate finding |
| --- | --- |
| A maintenance switch temporarily suspends an existing service and gives a clear explanation. | Assess availability, reviewer access, and paid-user effects; the switch alone does not prove a violation. |
| A reviewed lesson catalog receives additional videos within the same described service. | Check content, rights, safety, rating, and business claims. Do not assume every content update is a new executable feature. |
| The submitted binary contains an unreviewed coaching/chat feature scheduled to activate after approval. | Flag dormant/unreviewed functionality; describe the trigger and user-visible difference. |
| A reviewer account sees a harmless screen while ordinary users see undisclosed functionality. | Confirmed concealment if supported by evidence. |
| A flag removes a privacy explanation while user data continues to leave the device. | Trace transmission and consent, then report the supported privacy issue. |
| A paywall experiment changes copy or layout. | Verify accessible variants, truthful terms, matching store data, and existing reviewed functionality; it is not automatically prohibited. |

## Practical recommendations

Prefer a small typed configuration surface, reliable bundled defaults, understandable unavailable states, and a retained release configuration snapshot. Keep sensitive consent and purchase assertions tied to real user/store state. These are engineering recommendations, not mandated Apple mechanisms.

In review notes, explain the switches that materially affect the reviewed experience, the variants, regional conditions, and how to exercise the associated functionality. Include enough detail to make the features reviewable; do not expose internal credentials or claim Apple requires publication of every key.

If a future change adds material functionality, the practical path is to submit the completed behavior for review rather than enabling an unreviewed dormant feature after approval. Missing live-state evidence must remain **Needs verification**.
