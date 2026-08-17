bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)

update:
	docker compose down
	git pull --rebase
	docker compose pull
	docker compose up -d --wait

start:
	docker compose up -d --wait

pause:
	docker compose stop

stop:
	docker compose down