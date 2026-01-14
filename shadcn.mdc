---
description: Apply when using, adding, or customizing shadcn/ui components. Covers CLI usage, component customization patterns, form integration with React Hook Form, theming with CSS variables, and accessibility considerations.
globs:
  - "**/components/ui/**/*.tsx"
  - "**/@ui/**/*.tsx"
  - "**/components.json"
alwaysApply: false
---

# shadcn/ui Guidelines

## 1. Overview

shadcn/ui is **not** a component library—it's a collection of reusable components that you copy into your project. Components are built on **Radix UI** primitives and styled with **Tailwind CSS**.

Key principles:

-   Components live in your codebase (not `node_modules`)
-   Full ownership and customization control
-   Accessible by default (via Radix UI)
-   Styled with Tailwind CSS utilities

## 2. Project Setup

### Directory Structure

shadcn components should be installed to the `@ui` directory as defined in [Directory Rules](./directory-rules.mdc).

```
components/
└── ui/                    # shadcn components live here
    ├── button.tsx
    ├── card.tsx
    ├── dialog.tsx
    ├── form.tsx
    ├── input.tsx
    └── ...
```

### Configuration (`components.json`)

```json
{
    "$schema": "https://ui.shadcn.com/schema.json",
    "style": "new-york",
    "rsc": true,
    "tsx": true,
    "tailwind": {
        "config": "",
        "css": "app/globals.css",
        "baseColor": "neutral",
        "cssVariables": true,
        "prefix": ""
    },
    "iconLibrary": "lucide",
    "aliases": {
        "components": "@/components",
        "utils": "@/lib/utils",
        "ui": "@/components/ui",
        "lib": "@/lib",
        "hooks": "@/hooks"
    },
    "registries": {}
}
```

**Configuration Notes:**

-   `tailwind.config: ""` - Empty for Tailwind v4 CSS-first configuration (no config file needed)
-   `iconLibrary: "lucide"` - Uses Lucide icons for consistent iconography
-   Aliases match the directory structure defined in [Directory Rules](./directory-rules.mdc)

## 3. Adding Components

Use the CLI to add components. Never copy-paste from the website manually.

```bash
# Add a single component
pnpm dlx shadcn@latest add button

# Add multiple components
pnpm dlx shadcn@latest add card dialog dropdown-menu

# Add all components (use sparingly)
pnpm dlx shadcn@latest add --all
```

### When to Add Components

-   ✅ Add components as needed, not preemptively
-   ✅ Review the component code after adding to understand its structure
-   ❌ Don't add all components upfront—adds unnecessary code

## 4. Component Customization

### Approach 1: Modify the Source (Preferred for Global Changes)

Since you own the code, modify `@ui/button.tsx` directly for app-wide changes.

```typescript
// @ui/button.tsx - Modified variant
const buttonVariants = cva("inline-flex items-center justify-center ...", {
    variants: {
        variant: {
            default: "bg-primary text-primary-foreground hover:bg-primary/90",
            destructive: "bg-destructive text-destructive-foreground",
            // Add custom variant
            brand: "bg-brand text-white hover:bg-brand/90",
        },
        // ...
    },
});
```

### Approach 2: Extend with className (Preferred for One-Off Changes)

Use Tailwind classes to override styles for specific instances.

```typescript
<Button className="rounded-full px-8">Custom Button</Button>
```

### Approach 3: Compose New Components (Preferred for Complex Variations)

Create new components that wrap shadcn primitives.

```typescript
// @ui/icon-button.tsx
import { Button, ButtonProps } from "@/components/ui/button";
import { cn } from "@/lib/utils";

interface IconButtonProps extends ButtonProps {
    icon: React.ReactNode;
}

export function IconButton({ icon, className, ...props }: IconButtonProps) {
    return (
        <Button
            size="icon"
            className={cn("rounded-full", className)}
            {...props}
        >
            {icon}
        </Button>
    );
}
```

## 5. Form Integration

shadcn provides form components that integrate with React Hook Form. Use them with the patterns from [Forms Guidelines](./forms.mdc).

```typescript
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";
import {
    Form,
    FormControl,
    FormDescription,
    FormField,
    FormItem,
    FormLabel,
    FormMessage,
} from "@/components/ui/form";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

const formSchema = z.object({
    name: z.string().min(2, "Name must be at least 2 characters"),
    email: z.string().email("Invalid email address"),
});

type FormValues = z.infer<typeof formSchema>;

export function ContactForm() {
    const form = useForm<FormValues>({
        resolver: zodResolver(formSchema),
        defaultValues: {
            name: "",
            email: "",
        },
    });

    function onSubmit(data: FormValues) {
        // Handle submission
    }

    return (
        <Form {...form}>
            <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
                <FormField
                    control={form.control}
                    name="name"
                    render={({ field }) => (
                        <FormItem>
                            <FormLabel>Name</FormLabel>
                            <FormControl>
                                <Input placeholder="John Doe" {...field} />
                            </FormControl>
                            <FormDescription>Your full name</FormDescription>
                            <FormMessage />
                        </FormItem>
                    )}
                />
                <FormField
                    control={form.control}
                    name="email"
                    render={({ field }) => (
                        <FormItem>
                            <FormLabel>Email</FormLabel>
                            <FormControl>
                                <Input
                                    type="email"
                                    placeholder="john@example.com"
                                    {...field}
                                />
                            </FormControl>
                            <FormMessage />
                        </FormItem>
                    )}
                />
                <Button type="submit">Submit</Button>
            </form>
        </Form>
    );
}
```

## 6. Theming

### CSS Variables

shadcn uses CSS variables for theming. Define them in your global CSS as specified in [Styling Rules](./styling-rules.mdc).

```css
@layer base {
    :root {
        --background: 0 0% 100%;
        --foreground: 0 0% 3.9%;
        --primary: 0 0% 9%;
        --primary-foreground: 0 0% 98%;
        /* ... other variables */
    }

    .dark {
        --background: 0 0% 3.9%;
        --foreground: 0 0% 98%;
        --primary: 0 0% 98%;
        --primary-foreground: 0 0% 9%;
        /* ... other variables */
    }
}
```

### Color Convention

Colors use HSL format without the `hsl()` function wrapper:

```css
--primary: 222.2 84% 4.9%; /* H S% L% */
```

Usage in Tailwind: `bg-primary` automatically resolves to `hsl(var(--primary))`.

## 7. Common Component Patterns

### Dialog with Form

```typescript
"use client";

import {
    Dialog,
    DialogContent,
    DialogDescription,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { CreateProjectForm } from "@/features/projects";

export function CreateProjectDialog() {
    const [open, setOpen] = useState(false);

    return (
        <Dialog open={open} onOpenChange={setOpen}>
            <DialogTrigger asChild>
                <Button>New Project</Button>
            </DialogTrigger>
            <DialogContent>
                <DialogHeader>
                    <DialogTitle>Create Project</DialogTitle>
                    <DialogDescription>
                        Add a new project to your workspace.
                    </DialogDescription>
                </DialogHeader>
                <CreateProjectForm onSuccess={() => setOpen(false)} />
            </DialogContent>
        </Dialog>
    );
}
```

### Data Table

For complex tables, use the shadcn DataTable pattern with TanStack Table:

```typescript
import {
    Table,
    TableBody,
    TableCell,
    TableHead,
    TableHeader,
    TableRow,
} from "@/components/ui/table";

// For simple tables, use the basic Table components
// For complex tables with sorting/filtering/pagination, add:
// pnpm dlx shadcn@latest add table
// Then follow the Data Table documentation pattern
```

## 8. Accessibility

shadcn components are accessible by default via Radix UI. Maintain this by:

-   ✅ Using semantic HTML elements
-   ✅ Keeping `aria-*` attributes from the original components
-   ✅ Testing keyboard navigation
-   ✅ Ensuring sufficient color contrast
-   ❌ Don't remove accessibility attributes when customizing
-   ❌ Don't override focus states without providing alternatives

## 9. Best Practices Summary

| Do                                         | Don't                                        |
| :----------------------------------------- | :------------------------------------------- |
| Use CLI to add components                  | Copy-paste from website                      |
| Add components as needed                   | Add all components upfront                   |
| Modify source for global changes           | Create wrapper components for simple changes |
| Use `cn()` utility for conditional classes | String concatenation for classes             |
| Keep accessibility attributes              | Remove aria-\* or role attributes            |
| Follow existing component patterns         | Create entirely custom implementations       |
| Use CSS variables for theming              | Hardcode colors in components                |
