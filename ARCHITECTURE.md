# Code structure

## Why feature folders

This is a React app, so strict MVC folders would split one feature across many places. Feature folders keep the screen and rules for one part of the app close together. The API and database stay in separate layers.

| Code | Meaning |
|---|---|
| `app/` | Next.js pages and request handlers. |
| `features/campaign-agent/screens/` | Screens for plans, tasks, and Satcon details. |
| `features/campaign-agent/plans.ts` | Builds the three ad plans and the team's task list. |
| `features/campaign-agent/performance.ts` | Uses saved Satcon campaign results to rank channels. |
| `features/workspace/` | Workspace screens, shared data types, and display helpers. |
| `app/api/` | Checks sign-in and access, then reads or saves information. |
| `db/` | Database connection and table definitions. |
| `drizzle/` | Database change history. |
| `lib/` | Shared research records, source links, and small utilities. |

## Where to make a change

| Code | Meaning |
|---|---|
| New ad-plan rule | Edit `features/campaign-agent/plans.ts`. |
| New campaign screen | Add it under `features/campaign-agent/screens/`. |
| Country study or media contact | Edit `lib/market-research.ts` and include its source link. |
| New saved field | Update `db/schema.ts`, then make a migration in `drizzle/`. |
| New web request | Add or update a route under `app/api/`. |

## Keep the layers clear

1. A screen displays data and handles clicks or form input.
2. A feature rule decides what plans, tasks, or summaries to create.
3. An API route checks the signed-in user and handles the web request.
4. The database layer saves data.

Do not put ad ranking rules in a screen. Do not put screen layout in an API route. Keep source dates and links beside the research record they support.

## Before merging a code change

- Keep names clear and use one feature folder for related changes.
- Reuse the shared types in `features/workspace/types.ts` and `features/campaign-agent/types.ts`.
- Use small screen components instead of adding another page to the workspace controller.
- Keep tests and validation checks beside the feature they cover when the team adds them.
- Never publish, book, or pay for an ad from an automatic app action. Keep CEO and owner approval in the flow.
