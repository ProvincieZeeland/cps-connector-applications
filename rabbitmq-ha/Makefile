#!make
include .env

# https://www.rabbitmq.com/ha.html#ways-to-configure

help:
	@echo "Build, start , stop RabbitMQ, init queues and view logs"
	@echo ""
	@echo "usage: make COMMAND"
	@echo ""
	@echo "Commands:"
	@echo "  build_rabbit        Build and start RabbitMQ"	
	@echo "  start_rabbit        Start RabbitMQ"
	@echo "  stop_rabbit         Stop RabbitMQ"
	@echo "  logs_rabbit-1       RabbitMQ logs node 1"
	@echo "  logs_rabbit-2       RabbitMQ logs node 2"
	@echo "  acc_init            Init queues for ACC environment"	
	@echo "  prod_init           Init queues for PROD environment"	
	@echo "  logs_rabbit         Show RabbitMQ logs"	


acc_init:
	# create user (NOTE: for admin user set "tags":"administrator" instead of "tags":"none")
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/users/${ACC_USER}" -H "Content-Type: application/json" -d '{"password":"${ACC_PASS}", "tags":"none"}'	

	# Create vhost
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/vhosts/${ACC_VHOST}" -H "Content-Type: application/json" -d '{"description": "CPS acceptatie", "default_queue_type": "quorum"}'

	# set vhost permissions
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/permissions/${ACC_VHOST}/${ACC_USER}" -H "Content-Type: application/json" -d '{"configure":".*","write":".*","read":".*"}'

	# create queues
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/queues/${ACC_VHOST}/cps_out" -H "Content-Type: application/json" -d '{"durable": true}'
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/queues/${ACC_VHOST}/zs_in" -H "Content-Type: application/json" -d '{"durable": true}'

	# Create exchanges
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/exchanges/${ACC_VHOST}/cps.exchange.acc" -H "Content-Type: application/json" -d'{"type":"direct","durable":true}'
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/exchanges/${ACC_VHOST}/zs.exchange.acc" -H "Content-Type: application/json" -d'{"type":"direct","durable":true}'	

	# Bind queues to exchange
	curl -X POST -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/bindings/${ACC_VHOST}/e/cps.exchange.acc/q/cps_out" -H "Content-Type: application/json" -d'{"routing_key":"cps_out","arguments":{}}'
	curl -X POST -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/bindings/${ACC_VHOST}/e/zs.exchange.acc/q/zs_in" -H "Content-Type: application/json" -d'{"routing_key":"zs_in","arguments":{}}'

	# set HA property
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/policies/${ACC_VHOST}/ha-acc" -H "Content-Type: application/json" -d '{"pattern": ".", "priority":0, "apply-to": "all", "definition": {"ha-mode": "all", "ha-sync-mode": "automatic", "ha-sync-batch-size": 1}}'

prod_init:
	# create user (NOTE: for admin user set "tags":"administrator" instead of "tags":"none")
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/users/${PROD_USER}" -H "Content-Type: application/json" -d '{"password":"${PROD_PASS}", "tags":"none"}'	

	# Create vhost
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/vhosts/${PROD_VHOST}" -H "Content-Type: application/json" -d '{"description": "CPS productie", "default_queue_type": "quorum"}'

	# set vhost permissions
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/permissions/${PROD_VHOST}/${PROD_USER}" -H "Content-Type: application/json" -d '{"configure":".*","write":".*","read":".*"}'

	# create queues
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/queues/${PROD_VHOST}/cps_out" -H "Content-Type: application/json" -d '{"durable": true}'
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/queues/${PROD_VHOST}/zs_in" -H "Content-Type: application/json" -d '{"durable": true}'

	# Create exchange
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/exchanges/${PROD_VHOST}/cps.exchange.prod" -H "Content-Type: application/json" -d'{"type":"direct","durable":true}'
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/exchanges/${PROD_VHOST}/zs.exchange.prod" -H "Content-Type: application/json" -d'{"type":"direct","durable":true}'		

	# Bind queues to exchange
	curl -X POST -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/bindings/${PROD_VHOST}/e/cps.exchange.prod/q/cps_out" -H "Content-Type: application/json" -d'{"routing_key":"cps_out","arguments":{}}'
	curl -X POST -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/bindings/${PROD_VHOST}/e/zs.exchange.prod/q/zs_in" -H "Content-Type: application/json" -d'{"routing_key":"zs_in","arguments":{}}'

	# set HA property
	curl -X PUT -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/policies/${PROD_VHOST}/ha-acc" -H "Content-Type: application/json" -d '{"pattern": ".", "priority":0, "apply-to": "all", "definition": {"ha-mode": "all", "ha-sync-mode": "automatic", "ha-sync-batch-size": 1}}'

diwoo:
	curl -X POST -i -u ${RABBIT_USER}:${RABBIT_PASS} "${RABBIT_SERVER}/api/queues/cps_dev/cps_out_diwoo/get" -H "Content-Type: application/json" -d '{"count":1, "ackmode":"ack_requeue_true", "encoding":"auto", "truncate":50000}'

build_rabbit:
	docker-compose up --build -d
	docker ps

start_rabbit:
	docker-compose up -d
	docker ps	

stop_rabbit:
	docker-compose down		
	docker ps	

logs_rabbit-1:
	docker logs rabbit1

logs_rabbit-2:
	docker logs rabbit2	
