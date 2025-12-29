# React Rules

## Component Structure
- Use functional components with hooks
- Keep components small and focused (single responsibility)
- Extract reusable logic into custom hooks
- Use composition over inheritance

## Hooks
- Follow Rules of Hooks (only call at top level)
- Create custom hooks for reusable logic
- Use `useMemo` and `useCallback` appropriately
- Clean up effects with return functions

## Props
- Use TypeScript for prop types
- Destructure props at the function signature
- Use default props or default parameters
- Keep prop interfaces close to components

## State Management
- Use `useState` for local component state
- Use `useReducer` for complex state logic
- Lift state up when multiple components need it
- Consider context for deeply nested prop drilling

## Performance
- Memoize expensive computations
- Use `React.memo` for components that re-render frequently
- Avoid creating objects/functions in render
- Use keys properly in lists

