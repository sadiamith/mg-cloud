mgCloud (Private Production App)

Full-stack property operations platform — Next.js + Django + Stripe + Mapbox + Kafka + ML

Code-less showcase. The production source is private for security and contractual reasons. This README summarizes the system, features, and engineering decisions. Demo available on request.

Live App:

https://meadowgreenpm.com

https://mgpmc.com

TL;DR

I built mgCloud, an end-to-end platform for landlords and investors to operate rental portfolios with real-time KPIs, geospatial context, robust payments, and ML-driven ROI forecasting. Frontend in Next.js 15/TypeScript, backend in Django REST + PostgreSQL/PostGIS, async via Kafka + Redis/Celery, maps via Mapbox, payments via Stripe (cards/bank, webhooks, disputes, reconciliation).

🔑 Highlights

Property Dashboard — Centralized KPIs: performance, occupancy, cash flow, trends.

Interactive Map (Mapbox) — Filter by location, occupancy, revenue; custom property markers and popups.

Tenant & Lease Management — Tenants, leases, rent schedules, renewals, reminders, payment status.

Expense & Utility Tracking — Upload bills, categorize expenses, monitor utility usage by unit/building.

AI-Powered ROI Forecasting — Custom ML forecasts for rental yield, cash flow, and long-term ROI.

Data & Reporting

Real-Time Reports — Income, expenses, and cash-flow statements.

Visualizations — Rent collection, vacancy trends, expense breakdowns.

Exports — One-click PDF/Excel for owners, investors, and accountants.

Portals & Access

Landlord Portal — Performance reports, statements, documents.

Tenant Portal (roadmap) — Invoices, maintenance requests, payments.

Role-Based Access — Separate permissions for owners, managers, and staff.

Payments (Stripe)

Cards/Bank — One-time + recurring rent, saved payment methods, automatic retries.

Webhooks — Real-time status, receipt issuance, ledger sync, dispute handling.

Payout Reconciliation — Owner statements aligned to Stripe balance transactions and fees.

🧱 Architecture (at a glance)
[Next.js 15 / TS / App Router]
   ├─ SSR/ISR pages, SWR + TanStack Query
   ├─ Mapbox GL (portfolio map, markers, popups)
   └─ Forms: React Hook Form + Zod (+ Turnstile / reCAPTCHA)

[Django REST Framework]
   ├─ Auth: JWT (rotation), RBAC, CORS
   ├─ Domains: properties, leases, tenants, expenses, utilities, reports
   ├─ Webhooks: Stripe (idempotent), SES notifications
   ├─ Services: Geocoding (Google), Mapbox utilities
   └─ Media: S3 (boto3), ImageKit + Pillow

[PostgreSQL + PostGIS]
   ├─ Geospatial indexes for map queries
   └─ Reporting views / materialized aggregates

[Async + Jobs]
   ├─ Kafka (events & messaging)
   └─ Redis + Celery (background jobs, email, ETL, reports)

[Infra/Ops]
   ├─ Dockerized services
   ├─ Nginx + Gunicorn
   └─ GitHub Actions CI/CD (env-based deploys)

🧰 Frontend Tech

Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS

State/Data: Zustand, TanStack Query, SWR

Forms/Security: React Hook Form, Zod, Cloudflare Turnstile, reCAPTCHA v3

UI/UX: Headless UI, Heroicons, Framer Motion, React Dropzone

Maps: Mapbox GL JS, React Map GL; custom property markers & clusters

SEO: JSON-LD, dynamic sitemaps/robots, canonical policy

Perf: Code splitting, image optimization (WebP/AVIF)

Quality: ESLint, Prettier, strict TS, automated audits

Multi-Domain production deployment

🧰 Backend Tech

Django 4.2, DRF 3.15, PostgreSQL (+ PostGIS), Gunicorn

Auth/Security: JWT (Simple JWT), custom permissions/RBAC, CORS, strict validators

Images/Media: ImageKit, Pillow, S3, WhiteNoise

Integrations: Stripe (payments/webhooks/disputes), Mapbox, Google Maps, Amazon SES

Docs & DevX: drf-yasg (OpenAPI/Swagger), Django Extensions, custom management commands

Ops: Signals for geocoding & image pipeline, bulk ops, cleanup tasks

⚙️ Engineering Decisions & Trade-offs

Payments: Idempotent Stripe webhook handlers; internal ledger for reconciliation against balance transactions/fees.

Geospatial: PostGIS with spatial indexes for fast bounding-box & proximity queries; server-side filtering to reduce map payloads.

Async: Kafka for event fan-out (notifications, audits), Celery for long-running tasks (reports, image ops).

Reporting: Aggregations + (optional) materialized views for heavy read paths; export pipeline for PDF/Excel.

Security: JWT rotation, CSP & hardened headers, strict input validation, file-type/size enforcement, CAPTCHA on public forms.

Scalability: Stateless app nodes, horizontal scaling, Redis-backed queues, DB indexing, read-optimized endpoints.

📈 Outcomes (production)

Lighthouse: 95+ on core properties pages (typical prod runs)

UX: Sub-second initial loads on cached routes; smooth map interactions with clustering

Ops: Clean CI/CD, environment-specific configs, automated housekeeping
Metrics vary by environment and content.

🗺️ Feature Matrix (snapshot)

 Property dashboard (KPIs, occupancy, cash flow)

 Mapbox portfolio map with filters & custom markers

 Tenants, leases, renewals, reminders

 Expenses & utilities with document uploads

 Real-time reports + visualizations

 PDF/Excel exports

 Role-based access (owners/managers/staff)

 Stripe cards/bank, recurring, retries, disputes

 Webhook-driven receipts and ledger sync

 Payout reconciliation to owner statements

 SES notifications

 Tenant portal (invoices, maintenance, payments) — roadmap

🔒 Privacy & Code Policy

Production code and infrastructure are private to protect users, data, and partners.

This public repo intentionally contains no source code.

I can provide a recorded walkthrough or a redacted live demo on request.

👋 About the Developer

Built solo end-to-end: system design → frontend → backend → integrations → CI/CD → production hardening.
Contact: sam774@usask.ca
 · Live app: https://meadowgreenpm.com
 | https://mgpmc.com

📌 Recruiter/Engineer Quick Scan

Stack: Next.js 15, TS, React 19, Tailwind, DRF, PostgreSQL/PostGIS, Redis, Kafka, Mapbox, Stripe, SES, S3

Strengths: payments at scale (idempotent webhooks + reconciliation), geospatial UX, reporting/exports, secure multi-tenant RBAC, async processing

What to see in a demo: dashboard KPIs, map filters, a Stripe webhook flow (test mode), and a report export

License

This showcase README is © Sadi Mustafa. Application code is proprietary and not distributed. Demo access provided case-by-case.
