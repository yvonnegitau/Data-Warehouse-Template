# Data Orchestration

For data orchestration we will be using Dagster. We will add Dagster to our docker compose. When running Dagster, one needs the below long running containers :

- Webserver
- Daemon
- Code Location (each code has its own container)
- Metadata database

Each run will be executed on its own container. Webserver and Daemon will have the same Docker image. We will also have files below which are a requirement:

* `workspace.yaml` tells the webserver and daemon the location of the code
* `dagster.yaml` configures the dagster instance

## Reverse Proxy
Dagster OSS does not come with authentication. I have added basic authentication to secure the webserver.

**NOTE: Sessions is not handled well. A better authentication should be used prod. This auth also does not handle RBAC. This only secures this setup.**

## Run Code

`docker compose up`

The webserver can be accessed through `localhost:3000`