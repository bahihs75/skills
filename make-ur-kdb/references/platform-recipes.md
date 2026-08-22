# Platform Recipes

Choose the recipe that exactly matches the user’s stated hosting and data platforms.

| Pair | Implementation direction |
| --- | --- |
| Render + Neon | Run a server-rendered or API-backed Node/Python app on Render; use pooled PostgreSQL connections; run schema migrations before traffic; store media in object storage. |
| Cloudflare + Firebase | Host the public application on Pages/Workers; use Firebase Authentication and Firestore rules as the authorization boundary; route privileged mutations through Cloud Functions or Workers. |
| Cloudflare + D1 | Use Workers for APIs, D1 migrations for relational data, R2 for media, and durable/queued processing only when required. |
| Vercel + Supabase | Use server-side Supabase clients for privileged work, Row Level Security for user data, storage buckets for media, and typed migrations. |
| Firebase Hosting + Firebase | Keep public content static where possible; enforce roles with Auth custom claims and Firestore rules; use Functions for trusted totals and order changes. |

Always map the chosen platform’s secrets through its official environment configuration, never through client-side source files.
