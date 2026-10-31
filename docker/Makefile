BESZEL_MODE ?= agent

bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	make stop
	git pull --rebase
	docker compose --profile $(BESZEL_MODE) pull
	make start
	docker system prune -a -f

start:
	docker compose --profile $(BESZEL_MODE) up -d --wait

pause:
	docker compose --profile $(BESZEL_MODE) stop

stop:
	docker compose --profile $(BESZEL_MODE) down