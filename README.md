# TradeHub AI

Premium black/white/gold SaaS website for an AI-powered trading platform, built with Next.js 15 (App Router), TypeScript, Tailwind CSS, Framer Motion, Supabase, and Stripe.

## Getting started

```bash
npm install
cp .env.example .env.local   # fill in your Supabase + Stripe keys
npm run dev
```

Open http://localhost:3000.

## Pages

| Route | Description |
|---|---|
| `/` | Home — hero, ticker tape, features, founder, pricing preview, CTA |
| `/features` | Full feature grid |
| `/pricing` | Free / Pro ($19) / Elite ($49) plans + FAQ |
| `/blog` | Blog index + `/blog/[slug]` post pages |
| `/dashboard` | Product dashboard: 6 tool modules + account stats |
| `/login`, `/signup` | Supabase email/password + Google OAuth |
| `/contact` | Contact form (writes to Supabase `contact_messages`) |

## Supabase setup

1. Create a project at supabase.com.
2. Run `supabase/schema.sql` in the SQL editor to create the `contact_messages` table.
3. In **Authentication → Providers**, enable Email and (optionally) Google.
4. Copy your Project URL and anon key into `.env.local`.

## Stripe setup

1. Create two recurring Prices in the Stripe dashboard: Pro ($19/mo) and Elite ($49/mo).
2. Add their Price IDs and your secret key to `.env.local`.
3. `POST /api/checkout` with `{ "plan": "pro" | "elite" }` returns a Checkout Session URL — wire this up to the pricing buttons when you're ready to charge.

## Founder / About section

`components/Founder.tsx` currently renders a placeholder monogram card. No photo was attached to this request — drop the founder photo into `/public` (e.g. `founder.jpg`) and swap in the commented `<Image>` code inside that file.

## Design system

- **Palette:** near-black (`#050505`), off-white (`#f4f2ec`), gold (`#c9a227` → `#e8cc6e`)
- **Type:** Fraunces (display/serif) + Inter (body) + JetBrains Mono (data/ticker)
- **Signature element:** live-animated candlestick hero graphic + scrolling market ticker tape
- All cards use glassmorphism (`.glass` / `.glass-gold` utility classes in `globals.css`)

## Deploying

Deploys cleanly to Vercel. Add the same environment variables from `.env.example` in your Vercel project settings.
