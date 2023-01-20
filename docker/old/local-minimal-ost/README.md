# Local C2 demo

This is a demo for the TMT integration with the Observer Support Tool (OST) application.

![TTI demo](img/tti_demo.gif)

## Steps to get started

1. run `docker compose up -d`
2. Go to the [homepage](http://localhost)
3. Use the homepage to open the TMT, or go to [TMT](http://localhost/tmt)
4. Click the + icon and upload the sqlite file from this folder
5. Go to [C2 app](http://localhost:3001/#!/map)
6. Go to [Webmail](http://localhost/webmail/?_user=ci@strategy.eu) and fill in the password (password is "default" without quotations)
7. Go back to the TMT and click on the running person icon on the scenario.
8. A popup will appear if you have not selected a role, select `exercise control` and then `start`
9. Click `start session`, then click the button that just appeared: `initialize` (you may uncheck `realtime` and specify your own time)
10. In the other tabs you can see that the scenario is running, and things should start to appear in the C2 app (SAFR = Situational Awareness for First Responders)

## Steps to edit a scenario

1. Click on the scenario's name
2. navigate to the `scenarios` tab
3. You can now change the injects

![Starting the TTI docker demo](img/tti_demo_start_docker.gif)

## Developer instructions

This folder contains a single `docker-compose` files, allowing you to run an OSINT track either:

- Locally: make sure to edit the `.env` file (see `.env_example`) first.
- Run `./start.sh`. Stop with `./stop.sh` or `./down.sh`.

## Environment variables

### `HOST`

Please copy `.env_example` to `.env` and set the HOST IP address or localhost appropriately. The docker compose will read from this file and substitute the variables in your script.

### `BROKER` and `SCHEMA` registry

Set the location of the Kafka broker and schema registry.

```bash
# When Kafka is part of the docker compose
BROKER=broker:29092
SCHEMA=http://schema-registry:8081
```

```bash
# When Kafka is externally hosted
BROKER=134.221.20.203:3501
SCHEMA=http://134.221.20.203:3502
```

### `COMPOSE_PROFILES`

It also includes [profiles](https://docs.docker.com/compose/profiles/) to selectively run some services. E.g. the profile

- `tmt`: is for starting the TMT
- `ost`: is for starting the OST

Multiple profiles can be specified by passing multiple --profile flags or a comma-separated list for the `COMPOSE_PROFILES` environment variable. E.g. to start the system on the server, set the `.env` to contain

```bash
COMPOSE_PROFILES=ost,tmt
```
