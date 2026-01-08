Implement React features using usehooks-ts library: $ARGUMENTS

**Process:**
1. Analyze requirements and identify hook needs
2. Check if usehooks-ts has suitable hooks (use Context7 MCP to query docs)
3. If no suitable hook exists, recommend alternatives (native React hooks, custom hooks, other libraries)
4. Implement with proper TypeScript types

**When usehooks-ts may NOT be suitable:**
- Complex state management (use Context/Redux)
- Data fetching (use React Query/SWR)
- Forms (use React Hook Form)
- Animation (use Framer Motion)
- Routing (use React Router/Next.js)

**Docs lookup:**
```
mcp__context7__resolve-library-id: libraryName="usehooks-ts"
mcp__context7__get-library-docs: query="[specific hook or feature]"
```

Do NOT force usehooks-ts if it doesn't fit. Recommend appropriate alternatives instead.
