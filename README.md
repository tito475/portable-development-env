# Portable Development Environment with Docker Compose

This project sets up a fully ready, portable development environment using Docker Compose. The environment is designed to be easy to spin up by any user with minimal configuration and supports multiple languages and frameworks. Users can check out this repository, run `docker-compose` with minimal additional parameters, and get an environment where a code server is running, fully equipped with all necessary tools and libraries.

## Features

- **Code Server**: A web-based IDE powered by Visual Studio Code.
- **Support for Multiple Languages and Frameworks**:
- Angular
- Java
- **Pre-configured Tools and Libraries**:
- Node.js
- Angular CLI
- OpenJDK
- Maven
- Google Chrome

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1. **Build and run the Docker containers**:
        ```sh
        docker-compose up --build
        ```

2. **Access the Code Server**:
        Open your web browser and navigate to `https://localhost:8443`. The default password is `password`.

## Directory Structure
- `code/`: Directory for user code.
- `codeserver/`: Contains configurations and Dockerfiles for the code server.
- `angular/`: Dockerfile for setting up an Angular development environment.
  - `java/`: Dockerfile for setting up a Java development environment.
  - `config/`: Configuration files for the code server.
  - `config.bak/`: Backup configuration files.
- `docker-compose.yml`: Docker Compose configuration file.

## Configuration

### Environment Variables

- `SUDO_PASSWORD`: Password for sudo access within the container.

### Volumes

- `./code:/config/workspace`: Mounts the `code` directory to the workspace directory in the container.
- `./codeserver/config:/config`: Mounts the `config` directory to the configuration directory in the container.

## Customization

You can customize the development environment by modifying the Dockerfiles and configuration files located in the `codeserver` directory.

### Adding New Tools and Libraries

To add new tools and libraries, edit the respective Dockerfile (e.g., `angular/Dockerfile` or `java/Dockerfile`) and add the necessary installation commands.

### Changing Code Server Settings

To change the settings of the code server, edit the configuration files located in the `codeserver/config` directory.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes or improvements.
