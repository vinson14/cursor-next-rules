---
description: Foundational project structure conventions for Next.js. Defines folder organization including @ui, @features, @layout, @hooks, @lib, and @types directories. Reference this when creating new files, organizing imports, or structuring features.
alwaysApply: false
---

In this Next.js repository, we will have the following folders:

-   `@ui` or `@ui/*` for reusable UI components (e.g., `@ui/button`, `@ui/dialog`). These should only contain components that can be re-used across the entire repository.
-   `@features` or `@features/*` for feature components (e.g., `@features/projects` resolves to index.tsx). A feature is usually complex and has its own folder. Within the feature folder:
    -   The main file should be within an `index.tsx` file
    -   Split required functions, handlers, hooks, etc. into separate files within the same folder
    -   The `index.tsx` file should be a composition of all those together with reusable components and functions from `@ui`, `@hooks`, `@lib`, etc.
    -   Anything that is specific to a particular feature should be placed inside the feature folder
-   `@layout` or `@layout/*` for reusable layout components (e.g., `@layout/MainLayout`). These should only contain layouts that can be re-used across the entire repository.
-   `@hooks/*` for reusable hooks (e.g., `@hooks/useExample`). These should only contain hooks that can be re-used across the entire repository.
-   `@lib/*` for reusable utilities (e.g., `@lib/apiClient`). These should only contain utilities that can be re-used across the entire repository.
-   `@types/*` for reusable types (e.g., `@types/user`). These should only contain types that can be re-used across the entire repository.

## Supabase File Structure (if using Supabase)

When using Supabase, organize files as follows:

-   `@lib/supabase/` for Supabase client factories:
    -   `server.ts` - Server-side Supabase client factory (used in Server Components and Server Actions)
    -   `client.ts` - Browser-side Supabase client factory (used in Client Components)
-   `@types/database.ts` - Generated TypeScript types from Supabase database schema (run `pnpm db:types` after schema changes)
-   `app/auth/` for authentication pages and routes:
    -   `login/page.tsx` - Login page
    -   `signup/page.tsx` - Signup page
    -   `callback/route.ts` - OAuth callback handler
    -   `verify-email/page.tsx` - Email verification page
-   `proxy.ts` - Auth refresh and route protection (Next.js 16+)

Additionally:

-   `page.tsx` files should always be a composition of components and features. They can also include calling server actions to render initial data.
