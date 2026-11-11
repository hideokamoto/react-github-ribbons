# React GitHub Ribbons

Simple React Component to add GitHub Ribbon for your React Application.

Ref: https://github.blog/2008-12-19-github-ribbons/

## Install

```bash
$ yarn add react-github-ribbons
```

## Usage

```tsx
import 'react-app-polyfill/ie11';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import GitHubRibbon from 'react-github-ribbons';

const App = () => {
  return (
    <div>
      <GitHubRibbon href="https://example.com" />
    </div>
  );
};
```

### Ribbon color & position
We can change the color and position

```tsx
// Default
<GitHubRibbon href="example.com" color="black" position="right"/>

// Orange and left
<GitHubRibbon href="example.com" color="orange" position="left" />

// White and right
<GitHubRibbon href="example.com" color="white" position="right" />
```

### Link parameters

The component will proxy `a` tag properties.

```tsx
<GitHubRibbon
  target="_blank"
  rel="noopener noreferrer"
  className="a-tag-link"
  href="example.com"
  color="orange"
  position="left"
/>
```

And you can import the property types.

```tsx
import GitHubRibbon, { GitHubRibbonProps } from 'react-github-ribbons';

const App = () => {
  const props: GitHubRibbonProps = {
    target: "_blank",
    rel: "noopener noreferrer",
    className: "a-tag-link",
    href: "example.com",
    color: "orange",
    position: "left",
  }
  return (
    <div>
      <GitHubRibbon {...props} />
    </div>
  );
};
```

## Development

This project uses modern tooling:

- **Vite** - Fast build tool and dev server
- **Vitest** - Lightning-fast unit testing
- **Biome** - Fast linter and formatter
- **TypeScript 5** - Type safety
- **React 18** - Latest React features

### Available Scripts

This project uses [pnpm](https://pnpm.io/).

```bash
# Install dependencies
pnpm install

# Development mode (watch mode)
pnpm run dev

# Build the library
pnpm run build

# Type check
pnpm run typecheck

# Run tests
pnpm test

# Run tests in watch mode
pnpm run test:watch

# Lint code
pnpm run lint

# Lint and auto-fix
pnpm run lint:fix

# Format code
pnpm run format
```

### Development Workflow

1. Make changes in `/src`
2. Run `pnpm run dev` to build in watch mode
3. Run `pnpm test` to verify tests pass
4. Run `pnpm run lint` to check code quality

The library will be built to `/dist` with both ESM and CommonJS formats.

## Release

Releases are automated on CircleCI with [semantic-release](https://semantic-release.gitbook.io/).
Merging a pull request into `main` decides the next version from the [Conventional Commits](https://www.conventionalcommits.org/) since the last `v*` tag, then pushes the tag, publishes to npm (Trusted Publishing / OIDC) and creates a GitHub Release.

- `fix:` / `perf:` → patch, `feat:` → minor, `feat!:` or `BREAKING CHANGE:` → major
- Other types (`chore:`, `docs:`, `ci:`, `test:` ...) do not release
- Do not bump `version` in `package.json` by hand. The published version comes from the tag.
