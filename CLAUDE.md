# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Bun-based monorepo for the Pelatform project, containing utility packages for SaaS applications. The repository uses Turborepo for build orchestration and Biome for linting/formatting.

## Tech Stack

- **Package Manager**: Bun (v1.3.3+)
- **Monorepo Tool**: Turborepo (v2.6.1)
- **Build Tool**: tsup (for package bundling)
- **Linting/Formatting**: Biome (v2.3.7)
- **Language**: TypeScript 5.9.3
- **Node Version**: >=20

## Common Commands

### Development

```bash
bun dev                    # Run all packages in dev mode with watch
bun build                  # Build all packages
bun types:check            # Type-check all packages
```

### Linting and Formatting

```bash
bun lint                   # Lint code with Biome (auto-fix)
bun format                 # Format code with Biome
bun lint:format            # Lint and format together (includes unsafe fixes)
```

### Package Management

```bash
bun install                # Install dependencies
bun clean                  # Clean build outputs in all packages
bun clean:all              # Deep clean (remove .turbo, bun.lock, node_modules)
```

### Publishing (for maintainers)

```bash
bun version                # Update versions using changesets
bun release                # Build and publish packages to npm
```

### Individual Package Development

```bash
cd packages/email && bun dev       # Develop email package with watch mode
cd packages/email && bun build     # Build specific package
cd packages/email && bun types:check  # Type-check specific package
```

## Repository Structure

```
.
├── packages/
│   ├── email/          # Email sending utilities (Resend, Nodemailer)
│   ├── storage/        # Storage providers (S3, Cloudinary, R2, MinIO, etc.)
│   └── utils/          # Common utility functions
└── apps/               # (Empty - reserved for future applications)
```

## Package Architecture

### @pelatform/email

- **Purpose**: Email template system and sending utilities
- **Providers**: Resend (default), Nodemailer (SMTP)
- **Key Dependencies**: @react-email/components, resend, nodemailer
- **Exports**: Main exports, `/components`, `/helpers`
- **Peer Dependencies**: react >=18.0.0

### @pelatform/storage

- **Purpose**: Unified storage interface for multiple cloud providers
- **Providers**: AWS S3, Cloudflare R2, MinIO, DigitalOcean Spaces, Supabase Storage, Cloudinary
- **Exports**: Main exports, `/s3`, `/cloudinary`, `/helpers`
- **Peer Dependencies**: Optional - @aws-sdk/client-s3, cloudinary (install only what you need)

### @pelatform/utils

- **Purpose**: Comprehensive utility functions for SaaS applications
- **Categories**: string, url, datetime, crypto, validation, browser, array, analytics
- **Exports**: Main exports, `/server` (for server-only utilities)
- **Key Features**: JWT handling, password hashing, slugification, URL utilities, date formatting

## Build Configuration

All packages use:

- **tsup** for bundling (configured via `tsup.config.ts`)
- **ESM format only** (no CommonJS)
- **Target**: ES2022
- **Multiple entry points** for tree-shaking (e.g., `/components`, `/helpers`, `/server`)

## Code Style

Biome is configured with:

- **Indentation**: 2 spaces
- **Line Width**: 100 characters
- **Quotes**: Single quotes for JS/TS, single quotes for CSS
- **Semicolons**: Always
- **Trailing Commas**: All
- **Import Sorting**: Enabled with custom groups (React/Next first, then packages, then @pelatform/\*, then relative imports)

Notable rules:

- Most a11y rules are disabled
- `noExplicitAny` is set to warn
- `useSortedClasses` is enabled for Tailwind (with `cn()` function)

## Turborepo Tasks

- **build**: Builds packages with dependency awareness (`dependsOn: ["^build"]`)
- **dev**: Runs dev servers (persistent, no cache)
- **start**: Starts production servers (requires build first)
- **types:check**: TypeScript type checking
- **clean/clean:all**: Cleanup tasks (no cache)

## TypeScript Configuration

All packages share similar tsconfig:

- **Module**: ESNext with bundler resolution
- **Strict mode**: Enabled
- **JSX**: react-jsx
- **Target**: ES2022
- **Declaration**: Generated automatically

## Publishing

Packages are published to npm with public access:

- Package names: `@pelatform/email`, `@pelatform/storage`, `@pelatform/utils`
- Versioning: Managed via changesets
- Build artifacts: `dist/` directory only

## Development Workflow

1. Make changes in `packages/*/src/`
2. Run `bun dev` in the specific package for watch mode
3. Run `bun types:check` to verify types
4. Run `bun lint:format` before committing
5. For publishing: update changesets, then run `bun version` and `bun release`

## Important Notes

- All packages are ESM-only (no CommonJS support)
- Storage package has optional peer dependencies - consumers only install what they need
- Email package requires React as a peer dependency
- Utils package has both client and server exports (`/server` for Node.js-only utilities)
- The `apps/` directory is empty and reserved for future applications
