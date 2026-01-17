# CLAUDE.md - Next.js + Supabase Project

## Project Overview
This is a Next.js 14 application using Supabase for database and authentication.

## Tech Stack
- **Framework:** Next.js 14 (App Router)
- **Database:** Supabase (PostgreSQL)
- **Auth:** Supabase Auth
- **Styling:** Tailwind CSS
- **Language:** TypeScript

## Commands
```bash
npm run dev      # Start development server
npm run build    # Build for production
npm run start    # Start production server
npm run lint     # Run ESLint
npm run test     # Run tests
```

## Project Structure
```
/app              # Next.js App Router
  /api            # API routes
  /(auth)         # Auth pages (login, signup)
  /(dashboard)    # Protected pages
/components       # React components
  /ui             # Reusable UI components
  /forms          # Form components
/lib              # Utilities
  /supabase       # Supabase clients
  /utils          # Helper functions
/types            # TypeScript types
/supabase         # Database migrations
```

## Environment Variables
Required in `.env.local`:
```
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
```

## Database Schema
[Add your schema here or reference /supabase/migrations]

## Key Patterns

### Server Components (Default)
```tsx
// app/dashboard/page.tsx
import { createClient } from '@/lib/supabase/server'

export default async function Dashboard() {
  const supabase = createClient()
  const { data } = await supabase.from('items').select()
  return <ItemList items={data} />
}
```

### Client Components (When Needed)
```tsx
'use client'
// components/InteractiveWidget.tsx
import { useState } from 'react'

export function InteractiveWidget() {
  const [count, setCount] = useState(0)
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>
}
```

### API Routes
```tsx
// app/api/items/route.ts
import { createClient } from '@/lib/supabase/server'
import { NextResponse } from 'next/server'

export async function GET() {
  const supabase = createClient()
  const { data, error } = await supabase.from('items').select()
  if (error) return NextResponse.json({ error: error.message }, { status: 500 })
  return NextResponse.json(data)
}
```

## Security Rules
- Never hardcode secrets
- Always use environment variables
- Enable RLS on all Supabase tables
- Validate all user inputs with Zod
- Use parameterized queries only

## When Generating Code
1. Use TypeScript with explicit types
2. Prefer server components
3. Add error handling
4. Include loading states
5. Follow existing patterns in codebase
