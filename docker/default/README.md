# Tabletop Technical Infrastructure

This folder contains a single `docker-compose` file, with multiple profiles (see below):

- Locally: make sure to edit the `.env` file (copy `example.env` to `.env`) first.
- Run `./start.sh`. Stop with `./stop.sh` or `./down.sh`.

## Running the infrastructure

This folder contains a single `docker-compose` files, allowing you to run either locally or in the cloud by editing the properties in the `.env` file:

- Locally: make sure to edit the `.env` file (see `.env_example`) first.
- Run `./start.sh`. Stop with `./stop.sh` or `./down.sh`.

### Environment variables

#### `HOST`

Please copy `.env_example` to `.env` and set the HOST IP address or localhost appropriately. The docker compose will read from this file and substitute the variables in your script.

#### `BROKER` and `SCHEMA` registry

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

It also includes [profiles](https://docs.docker.com/compose/profiles/) to selectively run some optional services, i.e. you can leave it blank for a minimal version. E.g. the profile:

- `tmt`: for starting the TMT
- `ost`: for starting the OST
- `mail`: for starting the webmail services (for fake mail accounts)
- `lfs`: for starting the large file service
- `homepage`: for starting the homepage

Multiple profiles can be specified by passing multiple --profile flags or a comma-separated list for the `COMPOSE_PROFILES` environment variable. E.g. to start the OST and TMT, set the `.env` to contain:

```bash
COMPOSE_PROFILES=ost,tmt
```

## Developer instructions

In order to connect your own services to either publish or receive (subscribe) information, you need to:

1. Connect to the infrastructure: [Apache Kafka](https://kafka.apache.org/) on port 9092 (on localhost) or 3501 (externally), and the schema registry on port 3502. You can use one of the existing adapters to achieve this (each repo contains examples of how to consume or produce messages).
   - [Node.js adapter](https://github.com/DRIVER-EU/node-test-bed-adapter), [examples](https://github.com/DRIVER-EU/example-node-test-bed-adapter).
   - [Python adapter](https://github.com/DRIVER-EU/python-test-bed-adapter).
   - [C# adapter](https://github.com/DRIVER-EU/csharp-test-bed-adapter).
   - [Java adapter](https://github.com/DRIVER-EU/java-test-bed-adapter).
   - Alternatively, you can create your own adapter from scratch, based on one of the open available Kafka connectors. Just be aware that all topics use [Apache AVRO](https://avro.apache.org/) to send messages (see also below), so you need to encode your message's key and value to AVRO before sending it to Kafka. The adapters mentioned above also include support for logging via Kafka, sharing the current simulation time, or sharing large files using the `large file service` (basically, an ftp-like folder with open access to store files and sharing their location via a `large file message`).
2. Each message that is sent needs its own AVRO schema, so either create one yourself or reuse an [existing AVRO schema](https://github.com/DRIVER-EU/avro-schemas). As each message consists of a key and value (the actual message), note that both are based on AVRO.
3. Add your message to the schemas folder and restart the `bootstrapper`, so it uploads your schema to the schema registry. Note that the name of your schema defines the corresponding Kafka topic, e.g. the `cm_cap-value.avsc` AVRO schema corresponds to the `cm_cap` topic.
