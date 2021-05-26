# Grouparoo Docker Omnibus Image

This repository builds the `grouparoo/omnibus` Docker image. This Docker image contains the following packages to make it easy to trial the commercially available Grouparoo packages.

This Docker Image is provided for trial use only. The trial period is not to exceed one month. After that one month period, you must obtain a commercial license from Grouparoo Inc. to continue using this software.

## Quickstart

```
curl -L https://www.grouparoo.com/docker-compose --output docker-compose.yml && docker-compose up
```

## What's Included

This repository contains:

- `@grouparoo/bigquery` - Open Source
- `@grouparoo/core` - Open Source
- `@grouparoo/csv` - Open Source
- `@grouparoo/customerio` - Open Source
- `@grouparoo/facebook` - Open Source
- `@grouparoo/files-s3` - Open Source
- `@grouparoo/google-sheets` - Open Source
- `@grouparoo/hubspot` - Open Source
- `@grouparoo/intercom` - Open Source
- `@grouparoo/iterable` - Open Source
- `@grouparoo/logger` - Open Source
- `@grouparoo/mailchimp` - Open Source
- `@grouparoo/marketo` - Open Source
- `@grouparoo/mongo` - Open Source
- `@grouparoo/mysql` - Open Source
- `@grouparoo/onesignal` - Open Source
- `@grouparoo/pardot` - Open Source
- `@grouparoo/pipedrive` - Open Source
- `@grouparoo/postgres` - Open Source
- `@grouparoo/redshift` - Open Source
- `@grouparoo/salesforce` - Open Source
- `@grouparoo/sendgrid` - Open Source
- `@grouparoo/sentry` - Open Source
- `@grouparoo/snowflake` - Open Source
- `@grouparoo/ui-enterprise` - Commercially Licensed
- `@grouparoo/zendesk`- Open Source

## Running with Docker

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

```
curl -L https://www.grouparoo.com/docker-compose --output docker-compose.yml
docker-compose up
```

Wait for the image to build and eventually visit `http://localhost:3000` to see the Grouparoo UI. Learn more by viewing the `docker-compose.yml` file included in this repository. Remember, all environment variables can be changed from their defaults, including database information, PORT, etc.

⚠️ Note: The example `docker-compose.yml` in this repository has limited data persistence and also no load balancing between `grouparoo-web` instances. Do not use in production.

---

Visit https://github.com/grouparoo/app-examples to see other Grouparoo Example Projects.
