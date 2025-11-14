# Neo Heroes Types

Shared TypeScript types for the Neo Heroes game ecosystem.

## Installation

### Local Development
```bash
npm install ../neo-hero-types
```

### From npm (after publishing)
```bash
npm install @neo-heroes/types
```

## Usage

```typescript
import { ICharacter, Job, ICalculatedCharacter } from '@neo-heroes/types';

const hero: ICharacter = {
  name: "Aragorn",
  job: Job.Warrior
};
```

## Types Exported

- `IAttributes` - Basic character attributes
- `IStats` - Extended stats with modifiers
- `Job` - Character job/class enum
- `ICharacter` - Base character interface
- `ICalculatedCharacter` - Computed character with battle stats
- `Modifier` - Stat modifier type

## Building

```bash
npm run build
```

This generates type declarations in the `dist/` folder.

## Publishing

```bash
npm publish
```

Or for scoped packages:
```bash
npm publish --access public
```
