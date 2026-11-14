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
npm ci
npm run lint            # Biome lint + format check
npm run typecheck       # tsc
npm test                # Vitest
npm run build           # Vite library build -> dist/
npm run check:exports   # verify published entry points and types
```

## Release

Releases are published from CircleCI, not GitHub Actions. The `npm publish`
pipeline (config: `workflows/publish/npm-polyrepo-semantic-release.yaml` in
[hideokamoto/circleci-configurations](https://github.com/hideokamoto/circleci-configurations))
runs on pushes to `main`. semantic-release decides the version from the
Conventional Commits since the last tag and publishes with npm trusted
publishing (OIDC).

Publishing from a local machine also works: `npm publish` runs lint, tests and
the build first (`prepublishOnly`).
