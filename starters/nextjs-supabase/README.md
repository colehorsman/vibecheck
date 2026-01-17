# Next.js + Supabase Starter

Full-stack starter with authentication, database, and styling.

## Stack

- **Framework:** Next.js 14 (App Router)
- **Database:** Supabase PostgreSQL
- **Auth:** Supabase Auth
- **Styling:** Tailwind CSS
- **Deployment:** Vercel

## Quick Start

```bash
# Create project
npx create-next-app@latest my-app --typescript --tailwind --eslint --app

cd my-app

# Install Supabase
npm install @supabase/supabase-js @supabase/ssr

# Copy environment template
cp .env.example .env.local
# Fill in your Supabase credentials
```

## Project Structure

```
my-app/
├── app/
│   ├── layout.tsx          # Root layout
│   ├── page.tsx            # Home page
│   ├── login/
│   │   └── page.tsx        # Login page
│   ├── dashboard/
│   │   └── page.tsx        # Protected dashboard
│   └── api/
│       └── auth/
│           └── callback/
│               └── route.ts # Auth callback
├── components/
│   ├── auth-form.tsx       # Login/signup form
│   └── navbar.tsx          # Navigation
├── lib/
│   └── supabase/
│       ├── client.ts       # Browser client
│       └── server.ts       # Server client
├── .env.example
├── .env.local              # Your secrets (gitignored)
└── middleware.ts           # Auth middleware
```

## Environment Variables

```bash
# .env.local
NEXT_PUBLIC_SUPABASE_URL=your-project-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

## Key Files

### lib/supabase/client.ts

```typescript
import { createBrowserClient } from '@supabase/ssr'

export function createClient() {
  return createBrowserClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  )
}
```

### lib/supabase/server.ts

```typescript
import { createServerClient } from '@supabase/ssr'
import { cookies } from 'next/headers'

export async function createClient() {
  const cookieStore = await cookies()

  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll() {
          return cookieStore.getAll()
        },
        setAll(cookiesToSet) {
          cookiesToSet.forEach(({ name, value, options }) =>
            cookieStore.set(name, value, options)
          )
        },
      },
    }
  )
}
```

### middleware.ts

```typescript
import { createServerClient } from '@supabase/ssr'
import { NextResponse, type NextRequest } from 'next/server'

export async function middleware(request: NextRequest) {
  let response = NextResponse.next({
    request: { headers: request.headers },
  })

  const supabase = createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll() {
          return request.cookies.getAll()
        },
        setAll(cookiesToSet) {
          cookiesToSet.forEach(({ name, value }) =>
            request.cookies.set(name, value)
          )
          response = NextResponse.next({ request })
          cookiesToSet.forEach(({ name, value, options }) =>
            response.cookies.set(name, value, options)
          )
        },
      },
    }
  )

  const { data: { user } } = await supabase.auth.getUser()

  // Protect dashboard routes
  if (!user && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url))
  }

  return response
}

export const config = {
  matcher: ['/((?!_next/static|_next/image|favicon.ico).*)'],
}
```

## Next Steps

1. Set up Supabase project at [supabase.com](https://supabase.com)
2. Copy credentials to `.env.local`
3. Create database tables in Supabase dashboard
4. Build your features!

## Deployment

```bash
# Deploy to Vercel
vercel

# Add environment variables in Vercel dashboard
```
