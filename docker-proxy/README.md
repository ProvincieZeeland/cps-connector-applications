# Docker proxy
Access the Docker HTTP API using the tecnativa/docker-socket-proxy, used in the dashboard application to show Docker container information.

You might want to disable access to some specific API parts (like start/stop containers or exec code with a container), access is configured in the docker-compose file.
The settings match the API endpoints, internally HAProxy is used to validate the access.




