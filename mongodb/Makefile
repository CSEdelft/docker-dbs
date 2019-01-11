repo=uni
name=mongodb

ROOT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

.PHONY:run
run:
	mkdir -p ${ROOT_DIR}/DATA
	docker run \
		--rm -d \
		--name ${repo}-${name}-dev \
		-p 27017:27017 \
    --volume=${ROOT_DIR}/DATA:/data \
		mongo:4.0.5-xenial

.PHONY:restore
restore:
	mongorestore --gzip \
		--archive=${ROOT_DIR}/mongo_ecommerce.agz
	mongorestore --gzip \
		--archive=${ROOT_DIR}/mongo_ecommerceTabular.agz

.PHONY:connect
connect:
	mongo

.PHONY:kill
kill:
	docker kill $$( \
	docker ps -aq \
	--filter="name=${repo}-${name}-dev" )

