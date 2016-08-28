# Run WordPress with Docker Compose and WP-CLI

Quick and easy way to start and run new WordPress installation with Docker Compose and WP-CLI. Great way to develop themes and plugins, try new ideas. Easy to start, easy to dump.

## Dependencies
- Docker Engine 1.10.0+
- Docker Compose 1.6.0+

## How to run
To start your WordPress installation create `.env` file and make required configuration changes (`.example.env` may be used as a reference).

Edit `docker-compose.yml` file to mount custom theme/plugin folder(s) add aditional services etc.:

```yaml
...

wp:
    image: dbooom/docker-wp-cli
    volumes:
        - ./host-theme-dir:/usr/share/nginx/html/wp-content/themes/theme-name
    links:
        - db
    env_file: ./.env
    
...
```

Next, inside your project root directory (the same directory `docker-compose.yml` file is located), run the following command:

```sh
docker-compose up -d
```

This command will try to set up the environment and install WordPress and database inside the docker [data volumes](https://docs.docker.com/engine/userguide/containers/dockervolumes/). In case of any problems `docker-compose logs` may be used to inspect and get a hint about what could go wrong.

To stop and later resume created project, `docker-compose stop` and `docker-compose start` should be used.

To know more about how to work with Docker and Docker Compose, please refer to the [documentation](https://docs.docker.com/).

Note: First time you run `docker-compose up` command, few images will be downloaded from Docker Hub registry, this may take some time to finish bootstrap process.

## Configuration
All available configuration options are listed in `.env.example` file. Additional information about images used and its options may be found at:
- [WordPress (PHP) image](https://hub.docker.com/r/dbooom/docker-wp-cli/)
- [Nginx image](https://hub.docker.com/r/dbooom/docker-nginx-with-templates/)
