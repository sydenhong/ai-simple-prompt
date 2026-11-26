My project: [describe your app here, e.g. "A Telegram Bot Management Dashboard"]
Features I want: [list your pages/features]

You are an expert prompt engineer and full-stack teacher.
Write ONE complete, detailed prompt that I can paste into Google AI Studio
(Build mode) to generate my working web app.

Make the prompt detailed and specific: list every page, every database table
with columns, every Edge Function, and every setup step. Do not be vague.

The prompt you write must include these sections:

1. TECH STACK
   React + TypeScript + Tailwind CSS (Vite), Supabase (PostgreSQL, Auth,
   Edge Functions with Deno), native fetch for any external API.
   No Node.js/Express backend. No Gemini or any paid AI service.

2. OUTPUT RULES
   Write all code ONLY into project files, never paste code or SQL in the chat.
   SQL goes in supabase/migrations/001_init.sql, the setup guide goes in SETUP.md,
   and the chat reply is only a short list of files.

3. FRONTEND CONFIG
   .env with VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY (import.meta.env),
   plus .env.example and .gitignore. Show a friendly "Supabase is not configured"
   screen if values are missing.

4. AUTHENTICATION
   Supabase Auth login/logout, no public sign-up page. Only users in an
   "admins" table can access the dashboard. Protect all pages.

5. PAGES
   Each page and exactly what it shows or does. Clean, modern, responsive
   design with sidebar navigation. Use React Router BrowserRouter.

6. DATABASE
   Every table with columns and types, default/sample data where needed,
   indexes, an is_admin() function, and Row Level Security on all tables.

7. EDGE FUNCTIONS (only if needed)
   Use them for anything secret or external (APIs, bots, webhooks).
   Include CORS + OPTIONS handling, admin authorization checks, and secrets
   stored in Supabase Edge Function Secrets. Webhooks from outside services
   must disable JWT verification and use their own secret check.

8. SECURITY
   Never put secret keys (API tokens, service-role key) in the frontend or .env.
   Only the anon/publishable key is allowed in the frontend.

9. CLOUDFLARE WORKERS DEPLOY
   wrangler.jsonc with assets directory ./dist and
   not_found_handling "single-page-application", no Worker script.
   Deploy with "npm run build && npx wrangler deploy".
   If deploying from Git, VITE_ variables must be BUILD variables.
   Set Supabase Auth Site URL to the workers.dev URL.

10. SETUP.md
    Beginner step-by-step guide: create Supabase project, fill .env, run SQL,
    create admin user and insert into admins table, set secrets, deploy
    Edge Functions, run locally (npm install, npm run dev), deploy to
    Cloudflare Workers, and test every feature.
    Add a "Common Errors and Fixes" section for this project.

Keep it simple for a beginner and a 3-hour workshop.
Real working functionality, no mock data.
Reply with only the final prompt inside one code block.
