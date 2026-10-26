# ChannelMaster Pro — UI design handoff

Reference: `container-architecture` at `8df7150`. This is a standalone interactive **design prototype**, not a deployed production application.

## Concept
Source → Process → Destination. Sources and destinations are independent. Telegram is the current integration domain; Facebook, Instagram, RSS, YouTube and Web are **future adapters**, not live features.

## Screens and actions
| Screen | Main actions | Intended integration |
|---|---|---|
| Dashboard | Recent content, KPIs, shortcuts | Aggregate existing posts/donors/publishing state |
| Sources | Add donor, configure pull | Telegram donors, user Telegram accounts, source posts |
| Inbox | Filter, inspect, edit collected post | Source posts, drafts |
| Routes | Source → transformation → destination, save/pause | **Proposed route/orchestration service; not established as implemented** |
| AI Studio | Original, target language, translation, draft | Existing translation/draft services; generic rewrite is future |
| Publishing | Drafts, scheduled jobs, delivery results | PublishingService, publish_attempts |
| Calendar | Schedule and review publishing | Scheduled posts; UI integration to verify |
| Channels | Targets, bots, Telethon account access | Channels, bots, targets |
| Analytics | Reach, engagement | **Future; not implemented according to 2026-10-26 backlog** |
| Media | Select/upload assets | Media API, MinIO upload/confirm |
| Billing | Plan and usage | FOSSBilling source of truth, /me/limits |
| Admin | Users, tenant status, block, quotas | **Separate admin domain/container; never use tenant session** |

## Interactive prototype behavior
- Navigation switches pages; search filters visible post rows.
- Modals open for adding sources, posts, routes, channels, media and scheduling.
- Route builder selects a source, transform and destination, and can add a local demo route.
- Pause/resume changes only in-memory demo state.
- AI transformation is simulated; no external AI calls.
- Calendar, metrics, prices, users and channel names are fictional.
- All “save” operations are local demonstrations. No backend calls, secrets, token storage, uploads, or real publishing.
- Demo state is not persistent after refresh.

## Implementation guidance for Oleg
1. Preserve existing Next.js/React/Tailwind frontend and FastAPI backend. Translate the approved design into reusable React components.
2. Map each screen to actual OpenAPI contracts before enabling any action.
3. Show loading/empty/error/suspended/disconnected/permission-denied states.
4. Validate quota, tenant identity, compliance blocks and publish status on the server.
5. Do not expose bot tokens, Telethon sessions, provisioning keys or owner DB role in browser code.
6. Keep FOSSBilling as billing source of truth; do not duplicate subscription state.
7. Route builder is a product proposal; first reconcile with existing donor→draft→publish pipeline and avoid creating redundant persistence.
8. Keep Admin UI on its separate origin and authentication boundary.
9. Introduce social platforms only after official platform permissions, auth, media formats, rate limits and error semantics are implemented.
10. Add responsive/accessibility QA and Playwright tests before production deployment.

## Review priorities
1. Approve the overall visual direction and navigation.
2. Detail multi-source/multi-destination routes with filtering, approval and execution history.
3. Design split-screen editorial review, Telegram preview and failure handling.
4. Design onboarding wizard for first Telegram donor and first successful publish.
5. Produce exact API map and handoff checklist with Oleg.

## Preview
Open `design/channelmaster-ui/index.html` via an HTTP(S) static host. GitHub's ordinary source viewer displays HTML as code; GitHub Pages requires separate configuration. The design branch is deliberately isolated from Oleg's working branch.
