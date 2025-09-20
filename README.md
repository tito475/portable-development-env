# Portable Development Environment with Docker Compose

This project sets up a fully ready, portable development environment using Docker Compose. The environment is designed to be easy to spin up by any user with minimal configuration and supports multiple languages and frameworks. Users can check out this repository, run `docker-compose` with minimal additional parameters, and get an environment where a code server is running, fully equipped with all necessary tools and libraries.

## Features

- **Code Server**: A web-based IDE powered by Visual Studio Code.
- **Support for Multiple Languages and Frameworks**:
- Angular
- Java
- Python (with pyenv)
- PHP (with Composer, Laravel, Symfony CLI, and Xdebug)
- **Some Pre-configured Tools and Libraries**:
- Node.js
- Angular CLI
- OpenJDK
- Maven
- Google Chrome
- Pyenv
- PHP 8.2
- Composer
- Laravel CLI
- Symfony CLI
- PHPUnit
- PHP_CodeSniffer
- PHP-CS-Fixer
- Xdebug

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1. **Determine which language you want to work with and modify `context: ./codeserver/python` with the correct value in the `docker-compose` file.**
   - For Python: `./codeserver/python`
   - For Angular: `./codeserver/angular`
   - For Java: `./codeserver/java`
   - For PHP: `./codeserver/php`
2. **Build and run the Docker containers**:
        ```sh
        docker-compose up --build
        ```

3. **Access the Code Server**:
        Open your web browser and navigate to `https://localhost:8443`. The default password is `password`.

## Directory Structure

- `code/`: Directory for user code.
- `codeserver/`: Contains configurations and Dockerfiles for the code server.
- `angular/`: Dockerfile for setting up an Angular development environment.
- `java/`: Dockerfile for setting up a Java development environment.
- `codeserver/python`: Python Dockerfile (pyenv + Python 3.11.0 + pyenv-virtualenv)
- `codeserver/php`: PHP Dockerfile (PHP 8.2 + Composer + Laravel/Symfony CLI + Xdebug)
- `config/`: Configuration files for the code server.
- `docker-compose.yml`: Docker Compose configuration file.

## Configuration

### Environment Variables

- `SUDO_PASSWORD`: Password for sudo access within the container.

### Volumes

- `./code:/config/workspace`: Mounts the `code` directory to the workspace directory in the container.
- `./codeserver/config:/config`: Mounts the `config` directory to the configuration directory in the container.

### Python

- Managed via **pyenv** (installed under `/opt/pyenv`) with **Python 3.11.0** as the global interpreter.
- Includes **pyenv-virtualenv** for creating and managing isolated virtual environments.
- Quickstart:

  ```bash
  pyenv virtualenv 3.11.0 myenv
  pyenv activate myenv
  ```

### PHP

- **PHP 8.2** with comprehensive extensions (curl, mbstring, mysql, xml, zip, gd, sqlite3, bcmath, intl, soap)
- **Composer** for dependency management
- **Pre-installed frameworks and tools**:
  - Laravel CLI
  - Symfony CLI
  - PHPUnit for testing
  - PHP_CodeSniffer for code standards
  - PHP-CS-Fixer for code formatting
- **Xdebug** configured for debugging (listening on port 9003)
- Quickstart:

  ```bash
  # Create a new Laravel project
  laravel new my-project

  # Or create a new Symfony project
  symfony new my-project

  # Run PHP built-in server
  php -S 0.0.0.0:8000
  ```

## Quick Start Examples

After setting up your environment, try these quick examples:

### Python
```bash
python --version
pip install requests
python -c "import requests; print('Python environment ready!')"
```

### PHP
```bash
php --version
composer --version
composer install && php index.php
```

### Java
```bash
java --version
mvn --version
```

### Angular
```bash
node --version
ng version
ng new my-app
```

## Customization

You can customize the development environment by modifying the Dockerfiles and configuration files located in the `codeserver` directory.

### Adding New Tools and Libraries

To add new tools and libraries, edit the respective Dockerfile (e.g., `angular/Dockerfile`, `java/Dockerfile`, `python/Dockerfile`, or `php/Dockerfile`) and add the necessary installation commands.

### Changing Code Server Settings

To change the settings of the code server, edit the configuration files located in the `codeserver/config` directory.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes or improvements.
