# AGENTS.md

## Repo purpose

This repo builds a `php:8.3-fpm-alpine`-based image with common PHP extensions and helper scripts for building, pushing, and running the image locally via Docker Compose.

## Key files

- `Dockerfile`: Defines the PHP-FPM image and extensions (including `gd`, `imagick`, `intl`, `mysqli`, `pdo_mysql`, `zip`, `opcache`).
- `docker/build/execute.sh`: Builds the Docker image for the current git branch.
- `docker/build/upload.sh`: Pushes the image to Docker Hub (expects a prior login).
- `docker/build/all.sh`: Runs `execute.sh` then `upload.sh`.
- `docker/compose/execute.sh`: Runs Docker Compose for the current branch and prints container info.
- `docker/compose/main/docker-compose.yml`: Compose config for the `main` tag.
- `docker/compose/develop/docker-compose.yml`: Compose config for the `develop` tag.
- `docker/login.sh`: Logs into Docker Hub using `docker/username.txt` and `docker/password.txt`.
- `docker/cleanup.sh`: Removes exited containers and images (destructive).
- `docker/shutdown.sh`: Stops/removes containers and prunes dangling images (destructive).
- `tools/*.sh`: Utility scripts for chmod/chown/dos2unix and access.

## Common workflows

Build image for current branch:

- `docker/build/execute.sh`

Build and push image:

- `docker/build/all.sh`

Run compose for current branch:

- `docker/compose/execute.sh`

Login to Docker Hub (expects credentials files):

- `docker/login.sh`

## Notes and cautions

- Many scripts use `sudo` on Linux; run them in an environment where sudo is allowed.
- `docker/cleanup.sh` and `docker/shutdown.sh` are destructive (remove containers/images). Use with care.
- `docker/login.sh` expects `docker/username.txt` and `docker/password.txt` (not in repo).
