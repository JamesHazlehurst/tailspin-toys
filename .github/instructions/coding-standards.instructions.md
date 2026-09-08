---
description: 'Shared TypeScript, documentation, and commenting standards'
applyTo: '**/*.{ts,astro}'
---

# Coding Standards

## Comments Explain Intent

- Use comments to explain why code exists, the reasoning behind a non-obvious decision, or a constraint that is not evident from the code.
- Do not restate mechanics that the code already expresses. Prefer clearer names or smaller functions over comments that paraphrase the next line.
- Keep comments accurate. When changing related code, update or delete comments that no longer describe its intent; treat stale comments as bugs.
- Avoid commented-out code. Version control preserves prior implementations.

## API Documentation

Use TSDoc-style `/** ... */` comments for code contracts. Documentation should add information that types and names alone cannot communicate.

### Data-layer exports

Every exported function in `db/` and `src/lib/` must document:

- its purpose and any important behavior or side effects;
- every parameter with `@param`, including why an injectable `db` parameter is accepted;
- its return value with `@returns`, including meaningful `null`, empty, or rejected/error cases.

```ts
/**
 * Finds a game and its related publisher and category.
 *
 * @param db - Injectable database used by production pages and in-memory tests.
 * @param id - Numeric identifier of the game to retrieve.
 * @returns The mapped game, or `null` when no matching row exists.
 */
export async function getGameById(db: Database, id: number): Promise<Game | null> {
  // ...
}
```

### Astro component props

Every reusable component in `src/components/` must define and document a `Props` interface. Add a TSDoc comment that explains the component contract and document each property with its meaning, accepted values, and optional/default behavior where applicable. When the interface extends HTML attributes, state which native element receives them.

```astro
---
/** Properties accepted by the reusable status badge. */
interface Props {
  /** Text displayed inside the badge. */
  label: string;
  /** Visual emphasis; defaults to `neutral`. */
  tone?: 'neutral' | 'success';
}
---
```

## TypeScript Formatting

- Use two spaces for indentation and terminate statements with semicolons.
- Use single quotes for strings. Use template literals for interpolation and allow double quotes only when they avoid escaping.
- Include trailing commas in multiline arrays, objects, imports, exports, parameters, and arguments.
- Include parentheses around arrow-function parameters.
- Include spaces inside object braces, but not inside array brackets.
- Remove trailing whitespace and end every file with a newline.
- Let ESLint enforce these rules; do not disable a formatting rule locally to preserve inconsistent formatting.

Run lint through the `quality-checks` skill after changing TypeScript or Astro files.
