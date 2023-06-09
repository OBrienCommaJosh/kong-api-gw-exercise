# kong-api-gw-exercise
Small exercise to play with OSS Kong API Gateway in Free Mode

The default project:

- Creates a shared network, `kong-net`, for the Kong services to communicate
- Creates 3 services via Docker: `kong-database`, `kong-migrations`, and `kong-gateway` (note that it is also possible to run Kong Gateway in db-less mode if you plan purely to perform configuration via decK but that the db-related services are included here for the sake of optionality)
- Creates a Kong Gateway Service and Route that point to httpbin.org
- Extends the Gateway using the [Response Transformer](https://docs.konghq.com/hub/kong-inc/response-transformer/) plugin from Kong
- Adds a header that caches response results for 5 minutes

## Prerequisites

Before running this application, you will need to have the following prerequisites installed:

- [Docker](https://www.docker.com/) (and Docker Compose)
- [decK by Kong](https://github.com/Kong/deck)
- [curl](https://curl.se/)

In addition to these prerequisites, you will also need to create two files: `KONG_PASSWORD` and `POSTGRES_PASSWORD`. These files should contain passwords of your choosing that are required for services defined in the `docker-compose.yml` file.

To create these files, simply create two empty text files named `KONG_PASSWORD` and `POSTGRES_PASSWORD` in the root directory of this project. Then, open each file and enter a password of your choosing on a new line. Save and close the files when you're done.

Make sure all of these prerequisites are installed and properly configured before running this application.

## Quickstart Guide

After fulfilling the prerequisites outlined above, you can create the necessary services by running the following command in the root directory of this project:

```bash
docker compose up -d
```

This will start up the Kong Gateway and other services defined in the `docker-compose.yml` file.

Once the services are up and healthy, you should check decK's ability to connect to the Kong Gateway with the following command:

```bash
deck ping
```

If the command is successful, you can upload the predefined configuration located in the `kong.yaml` file using the following command:

```bash
deck sync
```

This will configure the Kong Gateway with the necessary services and routes for interfacing with httpbin.org.

Finally, you can use your local Kong Gateway to interface with httpbin.org by navigating to `http://localhost:8000` in your web browser.

When you are ready to deprovision the project, simply run `docker compose down` from the CLI:

```bash
docker compose down
```
