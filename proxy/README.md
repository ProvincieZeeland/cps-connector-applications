# NGINX proxy
NGINX is used as a reverse proxy to expose TCP ports from within the Docker application / API controllers to the internet. We are using a custom build container based on the nginx:1.23.3-alpine image with the addition of a custom compiled module to disable http headers.

- Added our custom labels (used in Dashboard to group containers)
- Added security options
- Added restart options
- Added logging
- Added healthcheck

## Getting started

- Copy example.conf to sites-enabled and configure with correct domain.
- Copy certificates to certs-enabled.
- Start using ```docker compose up --build``` (with optional -d to start in detached mode).


