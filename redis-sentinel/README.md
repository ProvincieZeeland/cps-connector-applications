# REDIS high-availability using sentinel
Original source code at https://github.com/Developers-Notebook/Redis-Sentinel-Docker-Compose and more information at https://www.developers-notebook.com/development/using-redis-sentinel-with-docker-compose

- Added rabbitmq.conf to support persistency using disk
- Added our custom labels (used in Dashboard to group containers)
- Added volumes for data and rabbitmq.conf
- Added security options
- Added restart options
- Added logging
- Added healthchecks

