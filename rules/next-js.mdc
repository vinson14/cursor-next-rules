---
description: Apply for Next.js App Router conventions including routing, layouts, metadata, proxy (middleware), and route handlers. Covers page.tsx, layout.tsx, route.ts patterns, dynamic routes, parallel routes, and intercepting routes.
globs:
    - "**/app/**/page.tsx"
    - "**/app/**/layout.tsx"
    - "**/app/**/route.ts"
    - "**/proxy.ts"
alwaysApply: false
---

# Next.js App Router Conventions

## 1. File-Based Routing

| File            | Purpose                                    |
| :-------------- | :----------------------------------------- |
| `page.tsx`      | Route UI - makes route publicly accessible |
| `layout.tsx`    | Shared UI for a segment and its children   |
| `loading.tsx`   | Loading UI (auto-wrapped in Suspense)      |
| `error.tsx`     | Error UI (must be Client Component)        |
| `not-found.tsx` | 404 UI for the segment                     |
| `route.ts`      | API endpoint (GET, POST, etc.)             |
| `template.tsx`  | Like layout but re-mounts on navigation    |
| `default.tsx`   | Fallback for parallel routes               |

## 2. Dynamic Routes

```
app/
├── projects/
│   ├── page.tsx              # /projects
│   └── [id]/
│       └── page.tsx          # /projects/123
├── blog/
│   └── [...slug]/
│       └── page.tsx          # /blog/a/b/c (catch-all)
└── shop/
    └── [[...slug]]/
        └── page.tsx          # /shop OR /shop/a/b (optional catch-all)
```

## 3. Route Groups

Use parentheses `(folder)` to organize without affecting URL:

```
app/
├── (marketing)/
│   ├── about/page.tsx        # /about
│   └── contact/page.tsx      # /contact
└── (dashboard)/
    ├── layout.tsx            # Shared dashboard layout
    └── settings/page.tsx     # /settings
```

## 4. Layouts

-   Layouts preserve state and don't re-render on navigation
-   Layouts cannot access current pathname (use `usePathname` in Client Component)
-   Root layout is required and must include `<html>` and `<body>`

```typescript
// app/layout.tsx (Root Layout - required)
export default function RootLayout({
    children,
}: {
    children: React.ReactNode;
}) {
    return (
        <html lang="en">
            <body>{children}</body>
        </html>
    );
}
```

## 5. Metadata

```typescript
// Static metadata
export const metadata = {
    title: "My App",
    description: "App description",
};

// Dynamic metadata
export async function generateMetadata({ params }: Props) {
    const project = await getProject(params.id);
    return { title: project.name };
}
```

## 6. Route Handlers

```typescript
// app/api/projects/route.ts
import { NextResponse } from "next/server";

export async function GET() {
    const projects = await getProjects();
    return NextResponse.json(projects);
}

export async function POST(request: Request) {
    const body = await request.json();
    const project = await createProject(body);
    return NextResponse.json(project, { status: 201 });
}
```

## 7. Proxy (Middleware)

In Next.js 16+, `middleware.ts` has been renamed to `proxy.ts` to better reflect its role in intercepting and modifying requests at the network boundary.

```typescript
// proxy.ts (root level)
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function proxy(request: NextRequest) {
    // Add custom header
    const response = NextResponse.next();
    response.headers.set("x-custom-header", "value");
    return response;
}

export const config = {
    matcher: ["/dashboard/:path*", "/api/:path*"],
};
```

**Migration:** If you have an existing `middleware.ts` file, use the codemod to migrate:

```bash
npx @next/codemod@canary middleware-to-proxy .
```

## 8. Best Practices

-   ✅ Use Server Components by default
-   ✅ Fetch data at the segment level closest to where it's used
-   ✅ Use `loading.tsx` for instant loading states
-   ✅ Use route groups to share layouts without affecting URLs
-   ❌ Don't create API routes for data that can be fetched directly in Server Components
-   ❌ Don't use `getServerSideProps` or `getStaticProps` (App Router uses different patterns)
