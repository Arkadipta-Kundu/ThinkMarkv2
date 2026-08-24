# ThinkMark v2

Multi-account ThinkMark: each account has private notes, and the same 4-character code can exist in different accounts.

Example:
- user1 + rt45 → note A
- user2 + rt45 → note B

## Stack
Vanilla HTML/CSS/JS + Supabase Auth + PostgreSQL + RLS + Cloudflare Pages.

## Setup
1. Supabase → SQL Editor → run `supabase/schema.sql`.
2. Supabase → Authentication → URL Configuration: set Site URL to your deployed `https://YOUR-SITE.pages.dev` and add it as a Redirect URL. For local testing add `http://localhost:5500`.
3. In `public/app.js`, replace `YOUR_SUPABASE_URL` and `YOUR_SUPABASE_PUBLISHABLE_KEY` with your Supabase Project URL and publishable/anon browser key. Never put a secret/service-role key in frontend code.
4. Deploy to Cloudflare Pages using root `/`, build command `exit 0`, output directory `public`.
5. In Supabase Auth, configure email confirmation according to your preference. Password reset uses Supabase Auth email links.

## Local test
`python -m http.server 5500 -d public`
then open `http://localhost:5500`.

## Security
RLS makes notes private by `auth.uid()`. The unique constraint is `(user_id, code)`, so codes can repeat across accounts but not within the same account.
# ThinkMarkv2
