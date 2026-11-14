# React GitHub Ribbons

A tiny React component that renders the classic "Fork me on GitHub" ribbon.

Ref: https://github.blog/2008-12-19-github-ribbons/

- Works with React 18 and 19
- Renders in the browser, in server-side rendering and in React Server Components
- Ships ESM, CommonJS and TypeScript declarations for both

## Install

```bash
npm install react-github-ribbons
```

## Usage

```tsx
import GitHubRibbon from 'react-github-ribbons';

const App = () => (
  <div>
    <GitHubRibbon href="https://github.com/your/repo" />
  </div>
);
```

The ribbon is absolutely positioned at the top corner of the nearest
positioned ancestor (or the page).

### Color and position

```tsx
// Default
<GitHubRibbon href="https://github.com/your/repo" color="black" position="right" />

// Orange, left
<GitHubRibbon href="https://github.com/your/repo" color="orange" position="left" />
```

| Prop       | Type                                                           | Default               |
| ---------- | -------------------------------------------------------------- | --------------------- |
| `href`     | `string` (required)                                            |                       |
| `color`    | `'black' \| 'red' \| 'green' \| 'orange' \| 'grey' \| 'white'` | `'black'`             |
| `position` | `'left' \| 'right'`                                            | `'right'`             |
| `alt`      | `string`                                                       | `'Fork me on GitHub'` |

### Anchor attributes, style and ref

Any other `<a>` attribute is passed through. `style` is merged on top of the
default positioning, so you can add or override individual properties.
`ref` is forwarded to the `<a>` element.

```tsx
<GitHubRibbon
  href="https://github.com/your/repo"
  target="_blank"
  rel="noopener noreferrer"
  className="github-ribbon"
  style={{ zIndex: 10 }}
/>;
```

The prop type is exported:

```tsx
import GitHubRibbon, { type GitHubRibbonProps } from 'react-github-ribbons';

const props: GitHubRibbonProps = {
  href: 'https://github.com/your/repo',
  color: 'orange',
  position: 'left',
};

const App = () => <GitHubRibbon {...props} />;
```

## Development

```bash
pnpm install
pnpm run lint            # Biome lint + format check
pnpm run typecheck       # tsc
pnpm test                # Vitest
pnpm run build           # Vite library build -> dist/
pnpm run check:exports   # verify published entry points and types
```

## Release

Releases are automated by CircleCI. Merge a PR whose commits follow
[Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, …)
into `main`, and [semantic-release](https://github.com/semantic-release/semantic-release)
pushes the git tag, publishes to npm via Trusted Publishing (OIDC), and creates the
GitHub Release. Release notes are published on
[GitHub Releases](https://github.com/hideokamoto/react-github-ribbons/releases).
Do not bump `version`, create tags, or run `npm publish` / `np` manually.

`feat:` -> minor, `fix:` / `perf:` -> patch, `feat!:` or a `BREAKING CHANGE:` footer
-> major. `chore:` / `docs:` / `ci:` / `test:` / merge commits do not release.
Commit messages are checked locally by commitlint (husky `commit-msg` hook,
enabled by `pnpm install`).

The pipeline definition is shared via
[`circleci-configurations`](https://github.com/hideokamoto/circleci-configurations)
(`workflows/publish/npm-polyrepo-semantic-release.yaml`). The release settings
live in `.releaserc.json`.
