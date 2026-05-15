<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into Skild — a registry for agentic intelligence built with TanStack Start and Clerk authentication.

**Changes made:**

- **`src/routes/__root.tsx`** — Added `PostHogProvider` wrapping the app with EU host, reverse proxy API host, and exception capture enabled. Added a `PostHogUserIdentifier` component that calls `posthog.identify()` when a Clerk user is signed in and `posthog.reset()` on sign-out.
- **`vite.config.ts`** — Added reverse proxy routes for `/ingest`, `/ingest/static`, and `/ingest/array` pointing to `eu.i.posthog.com` and `eu-assets.i.posthog.com`.
- **`src/components/SkillCard.tsx`** — Added `install_command_copied` event with skill title, install command, and category properties. Added `skill_card_opened` event on the Open link. Added `posthog.captureException()` in the clipboard error handler.
- **`src/routes/index.tsx`** — Added `browse_registry_clicked` event on the Browse Registry CTA and `publish_skill_clicked` on the Publish Skill CTA.
- **`src/components/Navbar.tsx`** — Added `sign_in_clicked` event on the Sign In button.
- **`.env`** — Created with `VITE_PUBLIC_POSTHOG_PROJECT_TOKEN` and `VITE_PUBLIC_POSTHOG_HOST` (EU).
- **`package.json`** — Installed `@posthog/react` and `posthog-node`.

## Events instrumented

| Event | Description | File |
|---|---|---|
| `browse_registry_clicked` | User clicked the 'Browse Registry' CTA on the home page hero | `src/routes/index.tsx` |
| `publish_skill_clicked` | User clicked the 'Publish Skill' CTA on the home page hero | `src/routes/index.tsx` |
| `sign_in_clicked` | Unauthenticated user clicked 'Sign In' in the navbar | `src/components/Navbar.tsx` |
| `install_command_copied` | User copied the install command from a skill card (includes skill_title, install_command, category) | `src/components/SkillCard.tsx` |
| `skill_card_opened` | User clicked 'Open' on a skill card (includes skill_title, category) | `src/components/SkillCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics dashboard](/dashboard/683468)
- [Key user actions over time](/insights/ANhplUQX) — line chart of all 4 main events over 30 days
- [Homepage to install conversion funnel](/insights/gKMQXbhZ) — 3-step conversion: Browse Registry → Skill Card Opened → Install Command Copied
- [Sign-in intent over time](/insights/NedrCUuc) — daily trend of `sign_in_clicked` as a leading indicator of auth conversion
- [Install commands copied by skill category](/insights/UOWtYzNo) — breakdown of copies by skill category to surface the most popular types
- [Publish Skill vs Browse Registry CTAs](/insights/XIJi4Nin) — weekly bar chart comparing unique users hitting each homepage CTA

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
