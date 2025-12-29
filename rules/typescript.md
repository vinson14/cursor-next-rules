# TypeScript Rules

## Type Safety
- Always define types for function parameters and return values
- Avoid using `any` - use `unknown` if type is truly unknown
- Use type inference where appropriate, but be explicit for public APIs
- Define interfaces for object shapes

## Type Definitions
- Use `interface` for object shapes that might be extended
- Use `type` for unions, intersections, and computed types
- Create shared types in `types/` directory
- Export types from a central `types/index.ts` file

## Best Practices
- Enable strict mode in `tsconfig.json`
- Use const assertions for literal types
- Prefer readonly for immutable data structures
- Use discriminated unions for state management

## Code Organization
- Keep type definitions close to where they're used
- Extract shared types to separate files
- Use namespace for organizing related types
- Document complex types with JSDoc comments

