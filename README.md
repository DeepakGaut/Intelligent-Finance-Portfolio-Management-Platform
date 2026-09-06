# AI Finance Platform

A full-stack personal finance management app built with Next.js. Track accounts and transactions, set budgets with automated alerts, scan receipts with AI, and get monthly financial insights — all in one dashboard.

## Features

- **Multi-account tracking** — create current and savings accounts, each with its own balance and transaction history
- **Transaction management** — log income and expenses, categorize them, and mark one as your default account
- **Recurring transactions** — schedule daily, weekly, monthly, or yearly transactions that process automatically in the background
- **AI receipt scanning** — snap or upload a photo of a receipt and have Google Gemini extract the amount, date, and category automatically
- **Budgeting with alerts** — set a monthly budget and get notified by email when you're close to going over
- **Dashboard & reports** — visual breakdowns of spending by category and account activity over time (via Recharts)
- **Monthly email reports** — automated summary emails sent via a background job
- **Authentication** — secure sign-in/sign-up handled by Clerk
- **Rate limiting & bot protection** — sensitive actions are protected with Arcjet

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | [Next.js 15](https://nextjs.org/) (App Router) |
| UI | React 19, Tailwind CSS, shadcn/ui, Radix UI |
| Database | PostgreSQL via [Prisma ORM](https://www.prisma.io/) |
| Auth | [Clerk](https://clerk.com/) |
| Background jobs | [Inngest](https://www.inngest.com/) |
| AI | [Google Gemini API](https://ai.google.dev/) |
| Email | [Resend](https://resend.com/) + React Email |
| Security | [Arcjet](https://arcjet.com/) (rate limiting) |
| Charts | [Recharts](https://recharts.org/) |
| Forms & validation | React Hook Form + Zod |

## Getting Started

### Prerequisites

- Node.js 18+
- A PostgreSQL database (e.g. [Supabase](https://supabase.com/) or [Neon](https://neon.tech/))
- Accounts/API keys for: Clerk, Google Gemini, Resend, Arcjet

### 1. Clone and install

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
npm install
```

### 2. Configure environment variables

Create a `.env` file in the project root:

```env
DATABASE_URL=
DIRECT_URL=

NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/onboarding
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/onboarding

GEMINI_API_KEY=

RESEND_API_KEY=

ARCJET_KEY=
```

### 3. Set up the database

```bash
npx prisma migrate deploy
npx prisma generate
```

### 4. Run the dev server

```bash
npm run dev
```

The app will be available at [http://localhost:3000](http://localhost:3000).

## Project Structure

```
app/                  Next.js App Router pages (auth, dashboard, account, transaction routes)
actions/              Server actions (accounts, budgets, transactions, email)
components/           Reusable UI components (incl. shadcn/ui components)
lib/                  Core utilities — Prisma client, Arcjet config, Inngest client/functions
prisma/               Database schema and migrations
emails/               React Email templates
data/                 Static data (categories, landing page content)
hooks/                Custom React hooks
```

## Data Model

The app is built around four core Prisma models:

- **User** — synced from Clerk, owns accounts, transactions, and a budget
- **Account** — a current or savings account with a balance
- **Transaction** — an income or expense entry, optionally recurring, linked to an account
- **Budget** — a single monthly budget per user with alert tracking

See [`prisma/schema.prisma`](./prisma/schema.prisma) for the full schema.

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start the development server (Turbopack) |
| `npm run build` | Build for production |
| `npm run start` | Start the production server |
| `npm run lint` | Run ESLint |
| `npm run email` | Preview React Email templates locally |

## License

This project is open source and available for personal and educational use.
