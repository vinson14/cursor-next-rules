# Next.js Rules

## File Structure
- Use the App Router structure (`app/` directory)
- Place components in `components/` directory
- Use `lib/` for utilities and helpers
- API routes go in `app/api/` directory

## Server Components
- Default to Server Components unless interactivity is needed
- Use 'use client' directive only when necessary
- Fetch data directly in Server Components

## Client Components
- Mark components with 'use client' when using hooks or browser APIs
- Keep client components small and focused
- Extract server logic to separate functions

## Routing
- Use file-based routing
- Use `route.ts` for API routes
- Use `layout.tsx` for shared layouts
- Use `loading.tsx` for loading states
- Use `error.tsx` for error boundaries

## Data Fetching
- Use async Server Components for data fetching
- Implement proper error handling
- Use Next.js caching strategies appropriately
- Revalidate data when needed

## Performance
- Optimize images using `next/image`
- Use dynamic imports for code splitting
- Implement proper metadata for SEO
- Use Suspense boundaries appropriately

