# PHP Development Environment

This directory contains the Dockerfile for setting up a comprehensive PHP development environment with VS Code Server.

## What's Included

### PHP Runtime
- **PHP 8.2** with essential extensions:
  - `php8.2-cli` - Command line interface
  - `php8.2-curl` - cURL support for HTTP requests
  - `php8.2-mbstring` - Multibyte string support
  - `php8.2-mysql` - MySQL database support
  - `php8.2-xml` - XML processing
  - `php8.2-zip` - ZIP archive support
  - `php8.2-gd` - Image processing
  - `php8.2-sqlite3` - SQLite database support
  - `php8.2-bcmath` - Arbitrary precision mathematics
  - `php8.2-intl` - Internationalization support
  - `php8.2-soap` - SOAP protocol support
  - `php8.2-xdebug` - Debugging and profiling

### Development Tools
- **Composer** - PHP dependency manager
- **Laravel CLI** - Laravel framework installer
- **Symfony CLI** - Symfony framework tools
- **PHPUnit** - Unit testing framework
- **PHP_CodeSniffer** - Code standards checker
- **PHP-CS-Fixer** - Code style fixer
- **Node.js 18** - For modern frontend tooling

### Configuration
- **Memory limit**: 256M
- **Max execution time**: 300 seconds
- **Upload max filesize**: 64M
- **Post max size**: 64M
- **Xdebug**: Configured for debugging with VS Code

## Usage Examples

### Creating a Laravel Project
```bash
# Inside the container
laravel new my-laravel-app
cd my-laravel-app
php artisan serve --host=0.0.0.0 --port=8000
```

### Creating a Symfony Project
```bash
# Inside the container
symfony new my-symfony-app
cd my-symfony-app
symfony server:start --no-tls --port=8000
```

### Running Tests
```bash
# PHPUnit is globally available
phpunit tests/

# Or using Composer
composer test
```

### Code Quality Tools
```bash
# Check code standards
phpcs --standard=PSR12 src/

# Fix code style
php-cs-fixer fix src/
```

## Debugging with Xdebug

The environment comes pre-configured with Xdebug for debugging PHP applications in VS Code:

1. **Xdebug is enabled** and configured to connect to `host.docker.internal:9003`
2. **Install the PHP Debug extension** in VS Code
3. **Create a launch configuration** in VS Code (`.vscode/launch.json`):

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/config/workspace": "${workspaceFolder}"
            }
        }
    ]
}
```

4. **Set breakpoints** in your PHP code
5. **Start debugging** in VS Code and run your PHP script

## Port Forwarding

When running web applications, make sure to bind to `0.0.0.0` instead of `localhost` so the application is accessible from outside the container:

```bash
# Laravel
php artisan serve --host=0.0.0.0 --port=8000

# Symfony
symfony server:start --no-tls --port=8000

# Built-in PHP server
php -S 0.0.0.0:8000
```

Then access your application at `http://localhost:8000` in your browser.

## Customization

To add more PHP extensions or tools, modify the `Dockerfile` in this directory and rebuild the container:

```dockerfile
# Add more PHP extensions
RUN apt-get update && apt-get install -y \
    php8.2-redis \
    php8.2-mongodb

# Install additional global tools
RUN composer global require phpstan/phpstan
```