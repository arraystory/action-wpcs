# WPCS Checker

A reusable GitHub Action to run PHPCS with WordPress Coding Standards on your plugins and themes.

## Usage

```yaml
name: WPCS

on:
  push:
    branches: [master, develop]
  pull_request:
    branches: [master, develop]

jobs:
  phpcs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: arraystory/action-wpcs@v1
        with:
          text_domain: 'my-plugin'
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `text_domain` | Yes | - | Plugin/theme text domain |
| `php_version` | No | `8.2` | PHP version to use |
| `minimum_php` | No | `7.4` | Minimum PHP version for compatibility checks |
| `prefixes` | No | - | Function/class prefixes (comma-separated) |
| `paths` | No | `.` | Paths to scan |
| `ignore` | No | `vendor,node_modules,assets` | Paths to ignore |

## Examples

### Basic usage

```yaml
- uses: arraystory/action-wpcs@v1
  with:
    text_domain: 'my-plugin'
```

### With prefixes

```yaml
- uses: arraystory/action-wpcs@v1
  with:
    text_domain: 'my-plugin'
    prefixes: 'myplugin_,MyPlugin_'
```

### Custom PHP version and paths

```yaml
- uses: arraystory/action-wpcs@v1
  with:
    text_domain: 'my-plugin'
    php_version: '8.1'
    minimum_php: '7.4'
    paths: 'includes src'
    ignore: 'vendor,node_modules,assets,tests'
```

### Full example workflow

```yaml
name: Code Quality

on:
  push:
    branches: [master, develop]
  pull_request:
    branches: [master, develop]

jobs:
  phpcs:
    name: WordPress Coding Standards
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Run PHPCS
        uses: arraystory/action-wpcs@v1
        with:
          text_domain: 'my-plugin'
          prefixes: 'myplugin_'
          minimum_php: '7.4'
```

## What's included

- **PHPCS** - PHP CodeSniffer
- **WPCS 3.0** - WordPress Coding Standards
- **PHPCompatibilityWP** - PHP version compatibility checks

## License

MIT
