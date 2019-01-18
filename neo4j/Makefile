repo=tudelft
name=neo4j

ROOT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

.PHONY:run
run:
	docker run \
		--rm -d \
		--name ${repo}-${name}-dev \
    -p 7474:7474 -p 7687:7687 \
		--volume=${ROOT_DIR}/DATA:/var/lib/neo4j/data \
    --volume=${ROOT_DIR}/LOGS:/logs \
		--env NEO4J_AUTH=none \
		-e NEO4J_dbms_active__database="ecommerce" \
		neo4j:3.4.1

# Use this to restore a database (db cannot be connected when restoring)
.PHONY:run-nodb
run-nodb:
	mkdir -p ${ROOT_DIR}/DATA
	mkdir -p ${ROOT_DIR}/LOGS
	docker run \
		--rm -d \
		--name ${repo}-${name}-dev \
    -p 7474:7474 -p 7687:7687 \
		--volume=${ROOT_DIR}/DATA:/var/lib/neo4j/data \
    --volume=${ROOT_DIR}/LOGS:/logs \
    --volume=${ROOT_DIR}/neo4j_ecommerce.dump:/backup.dump \
		--env NEO4J_AUTH=none \
		neo4j:3.4.1

.PHONY:connect
connect:
	cypher-shell

.PHONY:restore
restore:
	docker exec \
		$$(docker ps -aq --filter="name=${repo}-${name}-dev") \
		neo4j-admin load \
			--from=/backup.dump \
			--database=ecommerce \
			--force=true \
	&& \
		echo "restore successfull - shutdown (make kill) and start normally (make)"

.PHONY:kill
kill:
	docker kill $$( \
	docker ps -aq \
	--filter="name=${repo}-${name}-dev" )

