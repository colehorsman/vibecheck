# Project Kickoff Prompt

Use this when starting a new project from scratch.

---

## The Prompt

```
I want to build [PROJECT DESCRIPTION].

Tech stack:
- Frontend: [FRAMEWORK - e.g., Next.js 14, React, Vue]
- Backend: [BACKEND - e.g., Node.js, Python, Supabase]
- Database: [DATABASE - e.g., PostgreSQL, Supabase, MongoDB]
- Styling: [CSS - e.g., Tailwind, CSS Modules, styled-components]
- Deployment: [PLATFORM - e.g., Vercel, AWS, Railway]

Core features (MVP):
1. [FEATURE 1]
2. [FEATURE 2]
3. [FEATURE 3]

Constraints:
- [CONSTRAINT - e.g., Must work offline, Must be mobile-first]
- [CONSTRAINT - e.g., Budget: $0, No external APIs]

Please:
1. Create the project structure
2. Set up the basic configuration files
3. Implement [FIRST FEATURE] as a starting point
4. Include a .env.example file
5. Add a proper .gitignore

Start with the project structure, then we'll implement features one by one.
```

---

## Example: Todo App

```
I want to build a todo app with categories and due dates.

Tech stack:
- Frontend: Next.js 14 with App Router
- Backend: Supabase
- Database: Supabase PostgreSQL
- Styling: Tailwind CSS
- Deployment: Vercel

Core features (MVP):
1. Create, edit, delete todos
2. Organize todos by category
3. Set due dates with reminders
4. Mark todos as complete

Constraints:
- Must work on mobile
- Free tier only (Supabase + Vercel)

Please:
1. Create the project structure
2. Set up the basic configuration files
3. Implement the todo CRUD as a starting point
4. Include a .env.example file
5. Add a proper .gitignore

Start with the project structure, then we'll implement features one by one.
```

---

## Example: SaaS Dashboard

```
I want to build a SaaS dashboard for tracking customer metrics.

Tech stack:
- Frontend: Next.js 14 with App Router
- Backend: Next.js API routes
- Database: Supabase PostgreSQL
- Auth: Supabase Auth
- Styling: Tailwind CSS + shadcn/ui
- Deployment: Vercel

Core features (MVP):
1. User authentication (email/password)
2. Dashboard with key metrics (cards + charts)
3. Customer list with search/filter
4. Settings page for user profile

Constraints:
- Must be responsive
- Dark mode support
- Free tier compatible

Please:
1. Create the project structure
2. Set up the basic configuration files
3. Implement authentication first
4. Include a .env.example file
5. Add a proper .gitignore

Start with the project structure, then we'll implement features one by one.
```

---

## Tips

- Start with MVP features only
- Be explicit about tech stack versions
- Mention budget constraints upfront
- Ask for one feature at a time after setup
