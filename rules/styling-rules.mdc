---
description: Apply when styling components with Tailwind CSS v4. Covers CSS-first configuration, @theme directive for custom colors, utility class usage, and avoiding custom CSS classes in favor of Tailwind utilities.
globs:
  - "**/*.css"
  - "**/globals.css"
  - "**/tailwind.config.*"
alwaysApply: false
---

## Styling (Tailwind CSS v4)

-   **Refer to Tailwind Documentation**: Always refer to the Tailwind CSS documentation (@Tailwind docs) when applying styles, selecting utility classes, or configuring theme settings. Use the official Tailwind documentation to ensure correct usage of utilities, understand available options, and follow best practices.
-   **Theme Configuration**: Use the CSS-first configuration approach. Define global colors and theme extensions directly in the global CSS file (e.g., `app/globals.css`) using the `@theme` directive.
-   **Colors**: Define colors as CSS variables within the `@theme` block. This automatically generates Tailwind utilities (e.g., `bg-brand`, `text-brand`).
    ```css
    @theme {
        --color-brand: #3b82f6;
        --color-accent: #f59e0b;
    }
    ```
-   **Avoid Custom Classes**: Do not create global CSS classes (e.g., `.my-button`) for styling. Instead, use Tailwind utility classes or extend the theme if a value is missing.
