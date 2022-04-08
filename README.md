# Grouparoo Docker Omnibus Image

[![Node.js CI](https://github.com/grouparoo/omnibus/actions/workflows/test.yml/badge.svg)](https://github.com/grouparoo/omnibus/actions/workflows/test.yml)

This repository builds the `grouparoo/omnibus` Docker image. This Docker image contains the following packages to make it easy to trial the commercially available Grouparoo packages.

## Quickstart

```bash
curl -L https://www.grouparoo.com/docker-compose --output docker-compose.yml
docker compose up
# wait for boot
# visit http://localhost:3000
```

## What's Included

This repository contains:

- `@grouparoo/bigquery` - Open Source
- `@grouparoo/calculated-property` - Open Source
- `@grouparoo/cloudwatch` - Open Source
- `@grouparoo/core` - Open Source
- `@grouparoo/csv` - Open Source
- `@grouparoo/customerio` - Open Source
- `@grouparoo/eloqua` - Open Source
- `@grouparoo/facebook` - Open Source
- `@grouparoo/google-sheets` - Open Source
- `@grouparoo/hubspot` - Open Source
- `@grouparoo/intercom` - Open Source
- `@grouparoo/iterable` - Open Source
- `@grouparoo/logger` - Open Source
- `@grouparoo/mailchimp` - Open Source
- `@grouparoo/mailjet` - Open Source
- `@grouparoo/marketo` - Open Source
- `@grouparoo/mixpanel` - Open Source
- `@grouparoo/mongo` - Open Source
- `@grouparoo/mysql` - Open Source
- `@grouparoo/onesignal` - Open Source
- `@grouparoo/pardot` - Open Source
- `@grouparoo/pipedrive` - Open Source
- `@grouparoo/postgres` - Open Source
- `@grouparoo/redshift` - Open Source
- `@grouparoo/sailthru` - Open Source
- `@grouparoo/salesforce` - Open Source
- `@grouparoo/sendgrid` - Open Source
- `@grouparoo/sentry` - Open Source
- `@grouparoo/snowflake` - Open Source
- `@grouparoo/sqlite` - Open Source
- `@grouparoo/ui-enterprise` - Open Source
- `@grouparoo/zendesk`- Open Source

## Running with Docker

```bash
docker pull grouparoo/omnibus:v{version}
```

⚠️ Note: DO NOT USE The `latest` release - pick a version number! The `latest` release of this image will include our Alpha packages, which may not be suitable for Production.

At minimum, the following Environment variables will need to be set:

```
PORT=3000
WEB_URL=http://localhost:3000
WEB_SERVER=true
WORKERS=1
SERVER_TOKEN=my-super-cool-server-token
GROUPAROO_LOG_LEVEL=info
REDIS_URL="redis://localhost:6379/0"
DATABASE_URL="postgresql://localhost:5432/grouparoo_development"
```

To see the full list of configuration environment variables, check out the `.env.example` in this repository or visit https://www.grouparoo.com/docs/support/environment.

## Running with Docker Compose

`grouparoo/omnibus` can be deployed with Docker Compose to orchestrate everything you need for a Grouparoo cluster. This includes:

- Redis and Postgres services for data storage.
- Separate services for both Grouparoo `web` and `worker` roles, so they can be scaled independently.
- 2 internal networks (frontend and backend) to keep your data isolated.

You can quickly demo a Docker Compose Grouparoo deployment via:

```bash
curl -L https://www.grouparoo.com/docker-compose --output docker-compose.yml
docker compose up
# wait for boot
# visit http://localhost:3000
```

Wait for the image to build and eventually visit `http://localhost:3000` to see the Grouparoo UI. Learn more by viewing the `docker-compose.yml` file included in this repository. Remember, all environment variables can be changed from their defaults, including database information, PORT, etc.

⚠️ Note: The example `docker-compose.yml` in this repository has limited data persistence and also no load balancing between `grouparoo-web` instances. Do not use in production.

## AWS Cloudwatch Logs

This image can be configured to store logs with AWS Cloudwatch. To enabled this, set the following environment variables:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`

Note that, `GROUPAROO_LOG_LEVEL` also effects this logger. By default, the log-level of this logger is is "notice" NOT "info".

---

Visit https://github.com/grouparoo/app-examples to see other Grouparoo Example Projects.

---

## Publishing Notes

You can build and push this Docker image locally

0. Start fresh

```bash
docker kill $(docker ps -q) # stop all running docker containers
docker system prune -a # erase all local docker images
```

1. Build the image with the appropriate tag

```bash
docker build -t grouparoo/omnibus:v0.6.3 --secret id=npmrc,src=$HOME/.npmrc .
```

- Note that we are using your local `~/.npmrc` for installing the commercial Grouparoo Plugins. Change this if needed.
- Note we use `v` in font of the version number. You can also add the `latest` tag if needed.

1. Confirm that the image is created properly with `docker images`

```bash
REPOSITORY          TAG       IMAGE ID       CREATED          SIZE
grouparoo/omnibus   v0.6.3    6a3c9137d2a0   11 seconds ago   1.46GB
```

3. Push the image + tag

```bash
docker push grouparoo/omnibus:v0.6.3
```
