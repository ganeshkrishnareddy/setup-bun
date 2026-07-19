# Setup Bun

A GitHub Action that sets up [Bun](https://bun.sh) runtime with automatic dependency caching.

## Usage

### Basic

```yaml
- uses: ganeshkrishnareddy/setup-bun@v1
```

### Specific Version

```yaml
- uses: ganeshkrishnareddy/setup-bun@v1
  with:
    bun-version: '1.3.14'
```

### With Caching

```yaml
- uses: ganeshkrishnareddy/setup-bun@v1
  with:
    cache: 'true'
    cache-key: 'bun-${{ hashFiles(''bun.lock'') }}'
```

### Full Example

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - uses: ganeshkrishnareddy/setup-bun@v1
        with:
          bun-version: 'latest'
          cache: 'true'
      
      - run: bun install
      - run: bun test
      - run: bun run build
```

### With Private Registry

```yaml
- uses: ganeshkrishnareddy/setup-bun@v1
  with:
    registry-url: 'https://registry.npmjs.org'
    github-token: ${{ secrets.NPM_TOKEN }}
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `bun-version` | No | `latest` | Bun version (`latest`, `1.3.14`, `canary`) |
| `cache` | No | `true` | Enable dependency caching |
| `cache-key` | No | `''` | Custom cache key prefix |
| `registry-url` | No | `''` | npm registry URL |
| `github-token` | No | `''` | Token for registry auth |

## Outputs

| Output | Description |
|--------|-------------|
| `bun-version` | Installed Bun version |
| `cache-hit` | Whether cache was restored |

## Why Bun?

- **10-100x faster** than npm/yarn for installs
- **Built-in test runner** and bundler
- **Native TypeScript** support
- **Drop-in replacement** for Node.js

## License

MIT
