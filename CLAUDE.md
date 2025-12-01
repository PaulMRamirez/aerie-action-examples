# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains runnable examples of [PlanDev actions](https://nasa-ammos.github.io/plandev-docs/sequencing/actions/) for the NASA AMMOS PlanDev mission planning system. Each example demonstrates patterns for building custom actions that can be uploaded to PlanDev.

## Repository Structure

- **Root**: npm workspace configuration managing all examples
- **`examples/`**: Each subdirectory is an independent Node.js/TypeScript package
  - `basic-action/`: Simple action demonstrating core patterns
  - `ascii-art-action/`: Action with visual output
  - `fresh-action/`: Action demonstrating FRESH patterns
- **`.github/workflows/`**: CI pipeline running tests on all examples

## Common Commands

### From repository root:
```bash
npm install          # Install dependencies for all examples (uses workspaces)
npm test             # Run tests for all examples
```

### From an example directory (e.g., `examples/basic-action/`):
```bash
npm run build        # Build action to dist/action.js (TypeScript compile + Rollup bundle)
npm run test         # Run unit tests using Node.js test runner with tsx
npm run lint         # Check formatting with Prettier and ESLint
npm run format       # Auto-format code with Prettier
npm run stringify    # Build and stringify for PlanDev upload
```

## Technology Stack

- **Runtime**: Node.js 22.x (18.x minimum, see `.nvmrc`)
- **Language**: TypeScript
- **Build**: Rollup with TypeScript plugin
- **Test**: Node.js native test runner (`node --test`) with tsx for TypeScript support
- **Formatting**: Prettier
- **Key Dependency**: `@nasa-jpl/plandev-actions` - Core library for action development

## Development Patterns

### Example Package Structure
Each example follows this structure:
```
examples/<action-name>/
├── src/index.ts       # Main action entry point
├── tests/             # Unit tests (*.test.ts)
├── dist/              # Build output (gitignored)
├── package.json       # Example-specific dependencies
├── rollup.config.js   # Bundle configuration
└── tsconfig.json      # TypeScript configuration
```

### Build Output
Actions are bundled to `dist/action.js` - a single file ready for upload to PlanDev.

## Testing

Tests use Node.js native test runner with tsx for TypeScript transpilation:
```bash
node --import tsx --test 'tests/**/*.test.ts'
```

## CI/CD

GitHub Actions workflow (`.github/workflows/test.yml`) runs on:
- Push to `main`
- Pull requests to `main`

The workflow installs dependencies and runs `npm test` across all workspace examples.
