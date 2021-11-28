# Egghdz Demo - WordPress Development Environment with Docker

## Prerequisites

- [Docker](https://www.docker.com/get-started)

## Get Started

### Start Local Development Environment

1. Copy `.env.example` as `.env` and make changes accordingly.
2. Copy `Dockerfile.dev.example` as `Dockerfile.dev` and make changes accordingly.
3. Start the environment by running:

```shell
$ docker-compose up -d
```

4. Start playing around with WordPress by visiting: http://localhost:8080 (assuming `HOST_HTTP_PORT=8080` in
   your `.evn`).

### Stop Local Development Environment

```shell
$ docker-compose down
```

### Refresh from Scratch

1. Remove Docker Compose volumes.
   **Note:** This will wipe out the whole database instance as well as any WordPress files reside in the Docker Compose
   named volume `wordpress`. Please back them up accordingly beforehand if needed.
    - If the containers are running:
      ```shell
      $ docker-compose down -v --remove-orphans
      ```
    - Otherwise (if you haven't renamed the pre-defined volumes in `docker-compose.yml`):
      ```shell
      $ docker volume rm demo_wordpress_docker_wordpress demo_wordpress_docker_mariadb
      ```

2. Remove `src` from your project root. Again, please back up your files accordingly.

### Customise `php.ini` Directives

[`php.ini` directives](https://www.php.net/manual/en/ini.list.php) can be customised via `configuration/custom.ini`.
Check out `Dockerfile.dev.example` to see how this file can be included into a Docker image build.

### PHPMyAdmin

An instance of PHPMyAdmin will also be available at http://localhost:81, after staring up the development environment.

### Additional Notes

#### Why not use the Docker `user` option?

The `Dockerfile.dev.example` UID/GID workaround is necessary. The common PHP image solution of passing the `user` option
to Docker (Compose) - mentioned in the "Running as an arbitrary user" section
of [the WordPress Docker hub page](https://hub.docker.com/_/wordpress) - unfortunately won't work. This is because the
official WordPress image specifically uses `www-data:www-data` for some of its permission related operations.
