# Research: Retail Login Page

**Date**: 2026-10-09

## Decisions

### Tailwind CSS and theme tokens

- **Decision**: Keep the installed Tailwind CSS 4 CSS-first setup. Define and
  consume semantic design tokens in `app/globals.css` using `@theme inline`;
  do not introduce a legacy `tailwind.config` file.
- **Rationale**: The repository already imports `tailwindcss`, maps CSS
  variables through `@theme inline`, and routes CSS through the existing
  Tailwind Turbopack integration.
- **Alternatives considered**: Replacing the current pipeline or adding legacy
  configuration would introduce unnecessary configuration and conflict with
  the installed v4 conventions.
- **Evidence**: `package.json` declares Tailwind CSS and
  `@tailwindcss/turbopack` version 4; the lockfile resolves both to 4.3.3.
  `app/globals.css` contains `@import "tailwindcss"` and an existing
  `@theme inline` block.

### shadcn/ui components

- **Decision**: Initialize shadcn/ui for the existing app using `app/globals.css`
  and the existing `@/*` TypeScript alias. Generate only the primitives needed
  by the login form: Button, Input, Label, and Checkbox. Add a semantic alert
  primitive only if the chosen validation presentation needs it.
- **Rationale**: Local, composable components match the existing app structure
  and provide accessible controls without adding a separate UI runtime.
- **Alternatives considered**: Hand-building every primitive duplicates
  accessibility behavior; installing a broad component suite exceeds scope.
- **Evidence**: No `components.json`, `components/ui`, or shadcn-related runtime
  dependencies are present. `tsconfig.json` already defines `@/*`.

### Theme and typography

- **Decision**: Extend current CSS variables and `@theme inline` with the
  semantic tokens required by shadcn (background, foreground, card, primary,
  muted, destructive, border, input, ring, and radius). Preserve coherent
  light/dark color-scheme values and use the configured Geist sans font for
  body text rather than the current Arial override.
- **Rationale**: Semantic tokens allow the requested shadcn controls to follow
  the app theme consistently; using the font already loaded by the root layout
  avoids an unnecessary font dependency.
- **Alternatives considered**: Hard-coded colors in each component would
  duplicate style decisions; selecting a branded palette without brand guidance
  would be speculative. Use neutral tokens until retail branding is supplied.

### Authentication and navigation integration

- **Decision**: Keep authentication behind a typed application boundary that
  accepts email, password, and the Remember Me choice, and distinguishes
  accepted credentials, rejected credentials, and service unavailability.
  Bind recovery and registration links to existing application destinations.
  Do not invent endpoint paths, fake success, or store a password for Remember
  Me.
- **Rationale**: The feature spec assumes existing authentication and
  account-journey capabilities, but repository inspection found no auth
  implementation or established route destinations. Session duration and
  persistence belong to the approved provider.
- **Alternatives considered**: Adding an arbitrary endpoint or client-side
  success state would claim authentication without a real provider. Building
  recovery and registration flows would exceed the stated feature scope.
- **Integration dependency**: The implementation requires the host application
  to identify the approved authentication provider and existing recovery,
  registration, and authenticated landing destinations. Until then the UI must
  remain explicit about unavailable integration and must not claim a successful
  sign-in.

## Project Evidence

- `package.json`: Next.js 16.4.0, React 19.3.0, Tailwind CSS 4, and
  `@tailwindcss/turbopack`.
- `app/globals.css`: Tailwind CSS v4 import, root colors, `@theme inline`,
  system color-scheme override, and an Arial body font override.
- `app/layout.tsx`: App Router root layout loads Geist and Geist Mono.
- `app/page.tsx`: Current route is an empty placeholder.
- `tsconfig.json`: Strict TypeScript configuration and existing `@/*` alias.
- `next.config.ts`: Existing Tailwind Turbopack CSS loader configuration.
- `components.json` and shadcn component sources: not present.
- Authentication code or account journey routes: not found in the repository.
