# Cursor Rules Repository

This repository contains reusable rules that can be imported into Cursor IDE.

## How to Use These Rules in Cursor

### Option 1: Import from Repository URL

1. Open Cursor Settings
2. Navigate to Rules or `.cursorrules` settings
3. Import rules using the repository URL: `https://github.com/yourusername/cursor-next-rules`

### Option 2: Copy Rules File

1. Copy the contents of `.cursorrules` or any rule file
2. Paste into your project's `.cursorrules` file or Cursor settings

### Option 3: Reference in Your Project

Add a reference in your project's `.cursorrules` file:

```
@import https://raw.githubusercontent.com/yourusername/cursor-next-rules/main/.cursorrules
```

## Repository Structure

-   `.cursorrules` - Main rules file (can be imported directly)
-   `rules/` - Directory containing specialized rule files
    -   `nextjs.md` - Next.js specific rules
    -   `typescript.md` - TypeScript specific rules
    -   `react.md` - React specific rules

## Contributing

To add new rules:

1. Create a new `.md` file in the `rules/` directory
2. Follow the existing format
3. Update this README with a description
