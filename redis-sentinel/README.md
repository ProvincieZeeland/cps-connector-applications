# REDIS high-availability using sentinel
Original source code at https://github.com/Developers-Notebook/Redis-Sentinel-Docker-Compose

- Upgraded from redis:6-alpine to redis:7.2.4-alpine3.19
- Added rabbitmq.conf to support persistency using disk
- Added our custom labels (used in Dashboard to group containers)
- Added volumes for data and rabbitmq.conf
- Added security options
- Added restart options
- Added logging
- Added healthchecks

