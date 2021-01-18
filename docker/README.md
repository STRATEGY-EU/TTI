# TTI Local

Example of running the Table-Top Infrastructure locally on your PC. This `docker-compose.yml` will start the following services:

- Zookeeper: [Apache Zookeeper](https://zookeeper.apache.org/), an internal service, required for managing the state of connected client (what group of clients have read what messages). In case a client crashes, it can continue processing messages where it crashed.
- Broker: [Apache Kafka](https://kafka.apache.org/) is an open-source distributed event streaming platform used by thousands of companies for high-performance data pipelines, streaming analytics, data integration, and mission-critical applications. All TTI messages are streamed over Kafka between different solutions.
- Schema registry: Each published message must adhere to a an [AVRO-based](https://avro.apache.org/) schema, so each connected client knows exactly what information it receives.
- Kafka REST: A REST client for getting information from Kafka.
- Kafka topics ui: An optional service to easily inspect the Kafka topics, and the messages that were sent.
- Kafka schema registry ui: An optional service to easily inspect the AVRO schemas that are used per topic (each topic is associated with one and only one schema, but a schema may have different versions).
- Bootstrapper: A service that runs on startup, registering all required schemas and topics.
- [Time service](https://github.com/DRIVER-EU/test-bed-time-service): A service that manages the simulation time, i.e. the virtual clock of the tabletop.
- [Large file service](https://github.com/DRIVER-EU/large-file-service): An FTP-like service, where clients can upload large files and for sharing them (either openly or privately).
- [Trial management tool](https://github.com/DRIVER-EU/scenario-manager): A service that allows the exercise director to manage the scenario.
- [Mail service](https://github.com/DRIVER-EU/email-gateway): An adapted SMTP mail service that listens to Kafka, and sends all messages over Kafka, so email exchanges between participants can be tracked and followed for training and evaluation purposes during a tabletop.
