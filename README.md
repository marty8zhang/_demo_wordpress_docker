# Egghdz Demo - WordPress Development Environment with Docker

## Prerequisites

- [Docker](https://www.docker.com/get-started)

## Get Started

### Start Local Development Environment

1. Copy `.env.example` as `.env` and make changes accordingly.
2. Copy `Dockerfile.dev.example` as `Dockerfile.dev` and make changes accordingly.
3. 
```shell
$ docker-compose up -d
```

### Stop Local Development Environment

```shell
$ docker-compose down
```

### Refresh from Scratch

1. Remove Docker Compose volumes.
   **Note:** This will wipe out the whole database instance as well as any WordPress files reside in the Docker Compose named volume `wordpress`. Please back them up accordingly beforehand if needed.
   - If the containers are running:
     ```shell
     $ docker-compose down -v --remove-orphans
     ```
   - Otherwise (if you haven't renamed the pre-defined volumes in `docker-compose.yml`):
     ```shell
     $ docker volume rm demo_wordpress_docker_wordpress demo_wordpress_docker_mariadb
     ```

3. Remove `src` from your project root. Again, please back up your files accordingly.
