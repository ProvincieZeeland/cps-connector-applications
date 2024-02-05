# NGINX proxy
NGINX is used as a reverse proxy to expose TCP ports from within the Docker application / API controllers to the internet.

- Removed the use of the management defintions (we use the makefile for creating vhosts / users / policies etc).
- Added our custom labels (used in Dashboard to group containers)
- Added security options
- Added restart options
- Added logging
- Added healthcheck

## Getting started

