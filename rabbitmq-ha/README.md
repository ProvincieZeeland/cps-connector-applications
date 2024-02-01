# RabbitMQ high-availability using 2 nodes and HAProxy as a load balancer.
RabbitMQ is used to queue received webhooks from the Sharepoint container and Zaaksysteem.nl, entries within the queues are processed using Python workers available in the CPS API.  

Parts of the solution found at https://bhoey.com/blog/high-availability-rabbitmq-with-mirrored-queues/ but altered the following:

- Removed the use of the management defintions (we use the makefile for creating vhosts / users / policies etc).
- Added our custom labels (used in Dashboard to group containers)
- Added volumes for data and rabbitmq.conf
- Added security options
- Added restart options
- Added logging
- Added healthchecks

## Getting started

- Copy the env-example to .env and set the variables.
- Run docker compose up --build -d
- if all running use the Makefile to setup users / vhosts / exchanges / queues and the HA policy.
 
