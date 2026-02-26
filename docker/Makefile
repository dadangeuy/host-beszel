bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	docker compose --profile $(HOSTNAME) down
	git pull --rebase
	docker compose --profile $(HOSTNAME) pull
	docker compose --profile $(HOSTNAME) up -d --wait

start:
	docker compose --profile $(HOSTNAME) up -d --wait

pause:
	docker compose --profile $(HOSTNAME) stop

stop:
	docker compose --profile $(HOSTNAME) down

