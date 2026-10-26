# ChannelMaster / InfoRepacker — UI handoff to Oleg

Date: 2026-10-26. Status: visual prototype / frontend reference, NOT production-ready application.

## Artifacts

- `index.html`: public marketing homepage (InfoRepacker), dark "Convergence" theme. Animated canvas visualization: Telegram (only source) -> AI processing -> multiple publication destinations.
- `app.html`: interactive ChannelMaster dashboard prototype, demo data and client-side actions.
- Live homepage: https://deployforceus.github.io/channelmaster-ui-demo/
- Live dashboard: https://deployforceus.github.io/channelmaster-ui-demo/app.html

Both HTML files are standalone, with embedded CSS/JS. No external build required. They do NOT connect to production API or billing.

## Current product contract (important)

There is ONE source platform: Telegram. The homepage animation must depict Telegram -> processing/AI -> multiple destination channels. Telegram publishing is the current scenario; Facebook, Instagram, YouTube and other destinations are PLANNED, not active. The dashboard demo may contain aspirational source UI and must be restricted accordingly during integration.

## Intended product boundaries

Homepage: publicly accessible overview for prospects and payment-provider review. Needs approved product/legal information and real contact details before use as a commercial site.

Dashboard: authenticated tenant workspace. Existing demo sections include dashboard, sources, inbox, routes, AI Studio, publishing, calendar, channels, analytics, media, billing, and admin. Demo controls and fake data are placeholders. Do not interpret visual functionality as backend readiness.

## Integration approach

1. Review the two prototypes as UX reference. Preserve the existing backend, authentication, tenant isolation, and application routing.
2. Implement homepage as a public route (`/`) and dashboard behind authenticated routes (e.g. `/app/*`) in the project's existing frontend stack. Do not overwrite backend source or production configuration with these static files.
3. Replace demo data/actions with real API calls incrementally, feature by feature. Add loading/error/empty states and permission checks.
4. Only Telegram is supported as an ingestion source at this stage. Map source configuration to Telegram donor channels and ingestion jobs; show actual connection and sync status. Other source platforms must be disabled or marked Coming Soon.
5. Map inbox/drafts to persisted collected messages and draft lifecycle; maintain source attribution and moderation state.
6. Map routes to persisted Telegram source -> transform -> destination workflows. Validate ownership and permitted destinations server-side.
7. Map AI Studio to asynchronous translation/rewriting tasks; show original, generated result, editing, approval and failures. Never place AI API keys in browser.
8. Map publishing and calendar to real queue/scheduled jobs with idempotency, status, retries and audit trail. Display returned backend statuses.
9. Map channels to Telegram account/channel permissions and real connection state. Other social platforms are planned publication destinations, not available functionality. Do not mislabel destinations as ingestion sources.
10. Map analytics only when real metrics exist; never display demo numbers as live business metrics.
11. Map billing to actual subscription status and approved checkout flow. Billing provider credentials and webhooks belong server-side; do not expose secrets.
12. Map admin to authorized admin roles, with strict tenant isolation. Hide unauthorized controls, but enforce authorization on backend.

## Homepage commercial launch checklist

Before submitting this as the official merchant website, owner must approve: company/service identity, accurate capabilities, public contact method, actual pricing and billing frequency, cancellation/refund policy, terms of service, privacy policy, and customer support details. The current homepage explicitly states that payment is not accepted and plans are in preparation.

## Visual notes

- Homepage dark graphite with restrained teal accents, no purple gradient.
- Convergence illustration is a canvas animation; respect reduced-motion preferences. Review responsive behavior on phone and desktop.
- Dashboard is an earlier, separate prototype with its own visual language. Harmonizing the dashboard to homepage theme is a future design task, not part of this handoff.

## Source control / safety

Use a dedicated integration branch and Pull Request against `HelgerLee/channelmaster`'s active `container-architecture` branch. Do not force-push or merge to upstream without owner review. Keep the standalone public demo repo independent. Avoid copying backend code or credentials to this public repository.

## Known limitations

No live auth, real database, production API, subscription checkout, payment-provider validation, or end-to-end tests are supplied by this demo. A successful click in the prototype is not proof of production functionality.
