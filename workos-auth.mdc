---
description: Apply when implementing WorkOS AuthKit authentication. Covers middleware auth mode configuration in proxy.ts, unauthenticatedPaths setup, and auth callback route handler configuration.
globs:
  - "**/proxy.ts"
  - "**/auth/callback/route.ts"
alwaysApply: false
---

When implementing authentication with WorkOS AuthKit in middleware auth mode, use the following configuration in `proxy.ts`:

```typescript
import { authkitMiddleware } from "@workos-inc/authkit-nextjs";

// In middleware auth mode, each page is protected by default.
// Exceptions are configured via the `unauthenticatedPaths` option.
export default authkitMiddleware({
    middlewareAuth: {
        enabled: true,
        unauthenticatedPaths: [],
    },
    redirectUri: process.env.WORKOS_REDIRECT_URI,
});
```

**Important:**

-   This configuration must be placed in `proxy.ts` (not `middleware.ts`).
-   All pages are protected by default when `middlewareAuth.enabled` is `true`.
-   Add any public paths that should not require authentication to the `unauthenticatedPaths` array.
-   The `redirectUri` must be set via the `WORKOS_REDIRECT_URI` environment variable.

## Auth Callback Route

For handling WorkOS authentication callbacks, create a `route.ts` file at `/auth/callback` with the following configuration:

```typescript
import { handleAuth } from "@workos-inc/authkit-nextjs";

// Redirect the user to `/` after successful sign in
// The redirect can be customized: `handleAuth({ returnPathname: '/foo' })`
export const GET = handleAuth({
    returnPathname: "/projects",
});
```

**Important:**

-   This file must be created at `app/auth/callback/route.ts` (or `src/app/auth/callback/route.ts` if using the `src` directory).
-   The `returnPathname` option specifies where users are redirected after successful authentication.
-   Customize the `returnPathname` value based on your application's requirements (default shown is `/projects`).
