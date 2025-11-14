# Publishing Guide for @neo-heroes/types

## Before Publishing

### 1. Update Version (if needed)
```bash
cd /home/coronell/projects/neo-hero-types
npm version patch  # or minor, or major
```

### 2. Build the Package
```bash
npm run build
```

This will generate:
- `dist/` folder with compiled JavaScript
- Type declaration files (`.d.ts`)
- Declaration maps for better IDE support

## Publishing Options

### Option A: Publish to npm Registry (Public)

1. **Login to npm** (first time only):
```bash
npm login
```

2. **Publish as public scoped package**:
```bash
npm publish --access public
```

### Option B: Publish to npm Registry (Private)

```bash
npm publish
```

Note: Requires a paid npm account for private scoped packages.

### Option C: Use as Local Package (Current Setup)

The server already uses this as a local package. To update:

```bash
cd /home/coronell/projects/neo-hero-server
npm update @neo-heroes/types
```

### Option D: Publish to GitHub Packages

1. Create a `.npmrc` in the types package:
```
@neo-heroes:registry=https://npm.pkg.github.com
```

2. Update `package.json`:
```json
{
  "name": "@coronellw/neo-heroes-types",
  "repository": "https://github.com/coronellw/neo-heroes"
}
```

3. Publish:
```bash
npm publish
```

### Option E: Use Git Repository Directly

In your consuming projects:
```bash
npm install coronellw/neo-heroes-types#main
```

Or add to `package.json`:
```json
{
  "dependencies": {
    "@neo-heroes/types": "github:coronellw/neo-heroes-types"
  }
}
```

## After Publishing

### Install in Other Projects

```bash
# From npm
npm install @neo-heroes/types

# Or in package.json
npm install ../neo-hero-types  # Local path
```

### Usage in Projects

```typescript
import { ICharacter, Job, ICalculatedCharacter } from '@neo-heroes/types';

const hero: ICharacter = {
  name: "Aragorn",
  job: Job.Warrior
};
```

## Version Management

Follow semantic versioning:
- **PATCH** (1.0.x): Bug fixes, type corrections
- **MINOR** (1.x.0): New types added, backward compatible
- **MAJOR** (x.0.0): Breaking changes to existing types

## Automated Publishing (CI/CD)

Add to `.github/workflows/publish.yml`:

```yaml
name: Publish Package

on:
  release:
    types: [created]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
          registry-url: 'https://registry.npmjs.org'
      - run: npm ci
      - run: npm run build
      - run: npm publish --access public
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

## Best Practices

1. **Always build before publishing**: Run `npm run build`
2. **Test locally first**: Use local installation to test changes
3. **Update version**: Use `npm version` to update version in package.json
4. **Write changelog**: Document changes in README or CHANGELOG.md
5. **Tag releases**: Use git tags for published versions
