# REDIS high-availability using sentinel
Redis is used to store our oAUTH key with a TTL as specified by the oAUTH provider, as well as a solution to versioning issues between Sharepoint and Zaaksysteem.
As Redis is an important part of the software architecture it should be high-available with a automatic fail-over which we solved used the Sentinel setup.

![image](https://github.com/ProvincieZeeland/cps-connector-applications/assets/196572/1645dcd5-57c7-437e-900a-f7eb4fd76a73)

The original source code at https://github.com/Developers-Notebook/Redis-Sentinel-Docker-Compose

- Upgraded from redis:6-alpine to redis:7.2.4-alpine3.19
- Added rabbitmq.conf to support persistency using disk
- Added our custom labels (used in Dashboard to group containers)
- Added volumes for data and rabbitmq.conf
- Added security options
- Added restart options
- Added logging
- Added healthchecks

