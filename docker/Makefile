bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	docker compose -f docker-compose.yml --profile $(HOSTNAME) down
	git pull --rebase
	docker compose -f docker-compose.yml --profile $(HOSTNAME) pull
	docker compose -f docker-compose.yml --profile $(HOSTNAME) up -d --wait

start:
	docker compose -f docker-compose.yml --profile $(HOSTNAME) up -d --wait

pause:
	docker compose -f docker-compose.yml --profile $(HOSTNAME) stop

stop:
	docker compose -f docker-compose.yml --profile $(HOSTNAME) down

