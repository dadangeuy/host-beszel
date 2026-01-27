STORAGE_PATH ?= /home/rizaldi/storages/beszel

bootstrap:
	mkdir -p $(abspath $(STORAGE_PATH)); \
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	docker compose -f docker-compose.yml --profile "*" pull

start: start-hub start-agent

start-hub:
	docker compose -f docker-compose.yml --profile hub up -d --wait

start-agent:
	docker compose -f docker-compose.yml --profile agent up -d --wait

pause:
	docker compose -f docker-compose.yml --profile "*" agent stop

stop:
	docker compose -f docker-compose.yml --profile "*" down
