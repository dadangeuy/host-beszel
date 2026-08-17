BESZEL_MODE ?= agent

bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	docker compose --profile $(BESZEL_MODE) down
	git pull --rebase
	docker compose --profile $(BESZEL_MODE) pull
	docker compose --profile $(BESZEL_MODE) up -d --wait

start:
	docker compose --profile $(BESZEL_MODE) up -d --wait

pause:
	docker compose --profile $(BESZEL_MODE) stop

stop:
	docker compose --profile $(BESZEL_MODE) down