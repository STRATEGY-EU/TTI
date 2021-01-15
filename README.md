# TTI

Table-Top Infrastructure for the H2020 STRATEGY project.

![TTI](https://github.com/STRATEGY-EU/TTI/blob/main/img/table-top-infrastructure.png)

## Explanation

To run a technology-supported trial, exercise, training or table top, the EU-funded DRIVER+ project has developed a complete setup. Within the EU-funded H2020 STRATEGY project, this infrastructure is further refined and adapted to support the 7 tabletops and the final exercise. It consists of:

- Middleware, so different solutions/applications can exchange information with each other, receive (simulation) time information, and can exchange large files.
- The Trial Management Tool (TMT), a scenario editor to inject messages/events into the middleware, triggering actions in role players, end-user applications or attached simulators.
- Mail service, for exchanging messages between participants, and with the TMT.
- Map service, for displaying geographic information, like a flood or earthquake overlays on a map.

## Installation

All services are running in Docker containers, so you need to have Docker running on your system. In the `docker` folder, several TTI configurations can be found, including specific instructions. To start up all services, do:

```bash
docker-compose pull
docker-compose up -d
```

To show the status of all services, you can, for example, use `dockly` (you need to have [node.js](https://nodejs.org) installed), which you can install using `npm i -g dockly` (on Linux, this may require `sudo` privileges). Alternatively, you can simply do `docker ps`.
