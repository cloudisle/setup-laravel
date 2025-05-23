# Setup Laravel Environment

A GitHub Action to set up PHP and Node.js for Laravel workflows. This composite action combines [shivammathur/setup-php](https://github.com/shivammathur/setup-php) and [actions/setup-node](https://github.com/actions/setup-node) to provide a complete environment for Laravel applications.

## Usage

### Basic Usage

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: username/setup-laravel@v1 # Replace with your username and version
  # No need to run these commands separately as they are included in the action
```

### Custom Configuration

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: username/setup-laravel@v1 # Replace with your username and version
    with:
      php-version: '8.3'
      extensions: 'mbstring, xml, curl, zip, pdo, redis'
      node-version: '20'
      cache: 'npm'
      install-composer-cmd: 'install --no-interaction --no-dev'
      npm-build-cmd: 'production'
```

### Using Version Files

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: username/setup-laravel@v1 # Replace with your username and version
    with:
      php-version-file: '.php-version'
      node-version-file: '.nvmrc'
```

### Disabling Automatic Steps

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: username/setup-laravel@v1 # Replace with your username and version
    with:
      install-composer: 'false'
      install-npm: 'false'
      copy-env: 'false'
      generate-key: 'false'
      ziggy: 'false'
      npm-build: 'false'
  # Now run only the steps you need manually
  - run: composer install --no-dev
  - run: php artisan config:cache
```

## Inputs

### PHP Setup Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|--------|
| `php-version` | PHP version to set up (e.g., 8.2, 8.3, latest) | No | `8.2` |
| `php-version-file` | File containing the PHP version to use (e.g., .php-version) | No | `` |
| `extensions` | PHP extensions to install (comma-separated, prefix with : to disable) | No | `mbstring, xml, curl, zip, pdo, sqlite, mysql, pgsql, bcmath, gd, intl, redis, memcached` |
| `ini-file` | Base php.ini file (production, development, none) | No | `production` |
| `ini-values` | PHP ini values to add (comma-separated) | No | `memory_limit=256M, max_execution_time=180` |
| `coverage` | PHP code coverage driver (xdebug, pcov, none) | No | `xdebug` |
| `tools` | PHP tools to set up (comma-separated) | No | `composer` |

### Node.js Setup Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|--------|
| `node-version` | Node.js version to set up (e.g., 18, 20, lts/*) | No | `18` |
| `node-version-file` | File containing the Node.js version to use (e.g., .nvmrc, .node-version) | No | `` |
| `check-latest` | Check for the latest available version that satisfies the version spec | No | `false` |
| `architecture` | Target architecture for Node.js to use (x86, x64) | No | `` |
| `cache` | Package manager for caching (npm, yarn, pnpm) | No | `npm` |
| `cache-dependency-path` | Path to dependency file for caching | No | `` |
| `registry-url` | Registry URL for Node.js package manager | No | `` |
| `scope` | Scope for authenticating against scoped registries | No | `` |
| `always-auth` | Set always-auth option in npmrc file | No | `` |

### Laravel Setup Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|--------|
| `install-composer` | Install Composer | No | `true` |
| `install-composer-cmd` | Composer install command | No | `install --no-interaction --prefer-dist --optimize-autoloader` |
| `install-npm` | Install NPM | No | `true` |
| `install-npm-cmd` | NPM install command | No | `ci` |
| `copy-env` | Copy .env file | No | `true` |
| `generate-key` | Generate application key | No | `true` |
| `ziggy` | Generate Ziggy routes | No | `true` |
| `npm-build` | Run npm run build command | No | `true` |
| `npm-build-cmd` | NPM build command | No | `build` |

## License

MIT
