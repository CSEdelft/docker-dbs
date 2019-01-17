repo=tudelft
name=postgres

ROOT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

.PHONY:run
run:
	mkdir -p ${ROOT_DIR}/DATA
	docker run \
		--rm -d \
		--name ${repo}-${name}-dev \
		-p 5432:5432 \
		--volume=${ROOT_DIR}/DATA:/var/lib/postgresql/data \
		-e POSTGRES_PASSWORD=pwd \
		-e POSTGRES_USER=postgres \
		postgres:10

.PHONY:restore
restore:
	psql \
		--host=localhost \
		--port=5432 \
		--username=postgres \
		--password \
		-X \
		-c "CREATE DATABASE ecommerce" \
	; \
	pg_restore \
		--host=localhost \
		--port=5432 \
		--username=postgres \
		--password \
		--dbname "ecommerce" \
		--clean \
		${ROOT_DIR}/postgres_ecommerce.backup

.PHONY:connect
connect:
	psql \
		--host=localhost \
		--port=5432 \
		--username=postgres \
		--password \
		-X \
		-d ecommerce

.PHONY:kill
kill:
	docker kill $$( \
	docker ps -aq \
	--filter="name=${repo}-${name}-dev" )

