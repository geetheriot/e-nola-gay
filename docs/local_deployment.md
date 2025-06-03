# Local Deployment

This guide explains how to set up an Islandora environment for local development using the `isle-dc` project.

## Requirements

- Docker 19.x or newer
- docker-compose 1.25.x or newer
- GNU Make 4.0+
- Git 2.0+
- At least 8 GB of RAM (16 GB recommended)

Ensure Docker is configured with enough resources before running any of the Make commands.

## Getting Started

1. Clone this repository.
2. Copy `sample.env` to `.env` and edit any variables as needed. The default `ENVIRONMENT` value of `starter` will build a basic site from the Islandora starter project.
3. Run `make starter` to build the Docker images and initialize the `codebase` directory. The command will also generate secrets under `secrets/live`.
4. Start the containers with `make up`.
5. Visit [https://islandora.traefik.me](https://islandora.traefik.me) in your browser. If secrets are disabled, log in with username `admin` and password `password`. Otherwise, the admin password can be found in `secrets/live/DRUPAL_DEFAULT_ACCOUNT_PASSWORD`.

## Customizing the Codebase

Place an exported Drupal site in the `codebase/` directory before running `make starter` if you want to use an existing project. If you need to import configuration during installation, set the following in your `.env` file:

```bash
INSTALL_EXISTING_CONFIG=true
DRUPAL_INSTALL_PROFILE=minimal
```

## Managing the Environment

To rebuild the `docker-compose.yml` file after editing `.env` run:

```bash
make -B docker-compose.yml
make up
```

Stop the containers without destroying data with:

```bash
docker-compose down
```

Remove all containers and volumes to start fresh with:

```bash
docker-compose down -v
```

## Next Steps

Consult the main [README](../README.md) for more details on available services, enabling secrets, and additional configuration options.
