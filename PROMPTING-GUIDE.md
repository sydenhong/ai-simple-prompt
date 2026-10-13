# AI Prompt Guide — SYDEN Blog
For student and team. Use with free AI: **Google AI Studio**, ChatGPT, Gemini, DeepSeek.

How to use:
1. Copy the block
2. Paste in AI Studio
3. Change the red part `[...]` to your own project

---

# 🔥 Structure Prompt (Master) — Real Example: SYDEN Blog
This is a **full, real prompt**. Copy all of it into AI Studio. It can build the whole project.

```
## Project: SYDEN Blog

## Description:
A personal technology blog. I write article about web development, coding,
and real problem from my work. Visitor can read post, search, and comment.
Only admin (me) can write post, upload image, and manage advertisement.
The site also show my CV page.

## Tech Stack:
- Frontend: ReactJS 18 + Vite 5 (JavaScript .jsx, no TypeScript)
- Styling: Tailwind CSS 3.4 + @tailwindcss/typography
- Router: react-router-dom v6
- Backend: Supabase (PostgreSQL + Auth + Row Level Security)
- Storage: Cloudflare R2 (image, PDF)
- Hosting: Cloudflare Worker (serve React app + upload API)
- Markdown: marked + dompurify

## Database:
- Table: profiles
  (id, email, full_name, avatar_url, bio, is_admin, created_at)
- Table: posts
  (id, author_id, category_id, title, slug, excerpt, content, content_format,
   cover_url, status, is_featured, views, reading_time, published_at,
   created_at, updated_at)
- Table: categories (id, name, slug, description, created_at)
- Table: tags (id, name, slug)
- Table: post_tags (post_id, tag_id)
- Table: comments
  (id, post_id, parent_id, author_name, author_email, content,
   is_approved, created_at)
- Table: ads
  (id, name, slot, ad_type, image_url, link_url, script_code, width, height,
   position, is_active, starts_at, ends_at, impressions, clicks)
- Table: media
  (id, uploaded_by, object_key, public_url, file_name, mime_type,
   size_bytes, alt_text, created_at)
- Table: cv_sections (id, key, title, icon, position, is_visible)
- Table: cv_items
  (id, section_id, label, value, subtitle, url, position)
- Table: site_settings (key, value jsonb, updated_at)
- Table: subscribers (id, email, is_active, created_at)
- Table: contact_messages (id, name, email, subject, message, is_read, created_at)

## Features — Public (no login):
- Home page: list post, newest first, with pagination
- Post detail page: title, cover image, content, view counter, tag
- Category page and Tag page
- Search post by title
- Comment form (comment is hidden until admin approve)
- CV page (data come from cv_sections + cv_items table)
- About page and Contact form
- Newsletter subscribe by email
- Dark mode / light mode button

## Features — Admin (login only):
- Login with Supabase Auth (email + password)
- Dashboard: count post, draft, comment waiting, active ads
- Post: create, edit, delete, publish / unpublish
- Post editor: Markdown or HTML, live preview, auto slug from title,
  cover image, tag, reading time
- Category: create, rename, delete
- Comment: approve or delete
- Advertisement: image ads (upload to R2) or script ads (paste JS/HTML code)
- Media library: upload to Cloudflare R2, copy URL, delete
- CV editor: add / edit / delete CV row
- Message from contact form
- Site setting: site title, tagline, profile, CV PDF link

## Advertisement Detail (important):
- Slot: header, sidebar_top, sidebar_bottom, in_article, below_post, footer
- ad_type = 'image'  -> show <img>, click go to link_url, count click
- ad_type = 'script' -> inject raw HTML / JavaScript (Google AdSense)
  Note: innerHTML cannot run <script>. You must create the script element
  by document.createElement('script') and append it.
- Count impressions and clicks
- Ads can have start date and end date

## Security Rule (very important):
- Enable Row Level Security on EVERY table
- Create function public.is_admin() that read profiles.is_admin
- Public can SELECT: posts (only status='published'), categories, tags,
  cv_sections, cv_items, site_settings, ads (only is_active and in date)
- Public can INSERT only: comments (is_approved must be false),
  subscribers, contact_messages
- Only is_admin() can INSERT / UPDATE / DELETE other table
- Comment show to public only when is_approved = true

## Code Rules:
- All database call go in src/lib/api.js — never call supabase inside component
- Tailwind class only, no new .css file
- Dark mode use [data-theme="dark"] on <html>, not .dark class
- Post content must pass DOMPurify before render (XSS)
- Upload file go through POST /api/upload in the Worker (check admin token),
  never upload direct from browser
- Do not add new npm package that I did not list
- Do not invent table name or column name — use only my list above

## Output:
- Complete file, from first line to last line
- No "// ... rest of code same"
- Markdown code block, ready to copy and paste
- Short note only if I must change another file

## Request — do step by step, stop and wait for me after each step:
Step 1: SQL schema for Supabase (table + RLS policy + is_admin function
        + seed category)
Step 2: src/lib/supabase.js, src/lib/api.js, src/lib/AuthContext.jsx
Step 3: Layout, Header, Footer, Sidebar component
Step 4: Public page — Home, Post detail, Category, Search
Step 5: Admin — Login, RequireAdmin, AdminLayout, Dashboard
Step 6: Admin — PostsAdmin + PostEditor
Step 7: Admin — AdsAdmin + AdSlot component
Step 8: Cloudflare Worker (serve app, /api/upload to R2, /cdn/ to read R2)

Start with Step 1 only.
```

**Teach point:** the AI answer is only as good as this block. Short prompt = random answer.

---

# Structure: Fix Bug
```
## Project: SYDEN Blog
## Tech Stack: ReactJS + Vite + Tailwind + Supabase + Cloudflare Worker

## What I expect:
Ex: Click "Publish" button, then post show on home page

## What happen now:
Ex: Click button, nothing happen, post still draft

## Error message:
[paste FULL error from browser console, include the stack trace]

## My code:
[paste the COMPLETE file, not only a part]

## I already tried:
- Ex: I login as admin already — same problem
- Ex: Save draft is working, only publish not working

## Rules:
- Find the root cause, do not give me list of 5 maybe
- If you need to see another file, tell me the file name — do not guess it

## Output:
- Root cause in 2 sentence
- Before / after code
- How I can test it
```

# Structure: New Page or Component
```
## Project: SYDEN Blog
## Tech Stack: ReactJS 18 + Vite + Tailwind CSS + Supabase

## My existing file — copy this style:
[paste 1 complete file you already have, ex: CategoriesAdmin.jsx]

## Database table:
- Table: newsletters (id, subject, body, status, sent_at, recipients)

## What I want:
Admin page to list newsletter in a table, with New / Edit / Delete button.

## Rules:
- Same style as my file above (.card .panel .btn table.data .modal)
- Tailwind class only, no new css file
- Database call go in src/lib/api.js, not inside the component
- Handle loading state and empty state

## Output:
- Complete file src/pages/admin/NewslettersAdmin.jsx
- Only the new function to add in api.js
- 1 line route to add in App.jsx
```

# Structure: Code Review (before deploy)
```
## Project: SYDEN Blog

## My code:
[paste the complete file]

## Check by priority:
1. Security — can a normal user (not admin) write data?
2. Bug and error not handled
3. Slow query (N+1, no pagination)
4. Code already exist in my api.js

## Rules:
- Do not comment about format or naming style
- Do not rewrite everything
- Show me the line and the fix
- If my code is OK, just say OK — do not invent problem

## Output:
- Number list, most serious first, maximum 6
```

# Structure: SQL Migration (live database)
```
## Project: SYDEN Blog

## My existing table:
posts (id, title, slug, status, views, published_at, created_at)

## What I want to change:
Ex: Add column is_pinned boolean default false, and pin the 3 newest post

## Rules:
- Safe to run on live database with real data
- Safe to run 2 times (idempotent)
- Do not drop or rename existing column
- End with a SELECT so I can check the result

## Output:
- 1 SQL block, ready to paste in Supabase SQL Editor
```

# Structure: Write Blog Post
```
## My blog:
Technology article for developer. Simple English, short sentence.

## The real story:
- Problem I hit: [....]
- Why hard to find the answer: [....]
- What I tried but failed: [....]
- The fix that worked: [....]
- The code: [paste before / after code]

## Rules:
- Simple English, short sentence
- No marketing word (seamless, leverage, dive deep)
- Do not invent detail I did not give — write [TODO: ...] instead

## Output:
- 3 title option
- 2 sentence excerpt
- Full post in Markdown, 700-1000 word
- 5 tag
```

---

# ❌ Don't / ✅ Do
```
❌ make a login page
✅ [Tech stack + my file style] Write src/pages/Login.jsx use
   supabase.auth.signInWithPassword. Complete file only.

❌ my code is broken
✅ Expect X, get Y. Error: [full error]. Code: [full file]. Already tried A, B.

❌ is this good?
✅ Check security + error not handled. Max 6 finding. If OK just say OK.

❌ add comment feature
✅ Step 1 of 3: only the SQL for comments table with RLS.

❌ write better code
✅ Make this 3 database call become 1, same return value.
```

---

# Rules for Team
```
1. Free AI cannot see your file, your database, your screen.
   It only know what you paste. Always paste the project info first.

2. One task = one message. Not 5 file in 1 message.

3. Never accept "// ... rest of code same".
   Reply: "Give me the complete file from first line to last line."

4. Paste the FULL error message, not "it show error".

5. Never paste: service_role key, database password, client data, .env file.
   (Supabase anon key is OK — it is public already)

6. Big task? Ask the plan first:
   "Do not write code yet. Tell me your plan in 5 bullet."
   Then: "OK, but use X instead of Y. Now write it."

7. When AI start to forget your table name = the chat is full.
   Open new chat, paste the project info again.

8. You are senior, AI is junior. Read every line before you paste.
   If you cannot explain the line, do not use it.

9. Khmer OK: add "Reply in Khmer, keep code and technical term in English."

10. Change the database? Update this prompt file the same day.
    Old info = confident wrong code.
```
