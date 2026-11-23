.SHELLFLAGS := -ec
SECRET_KEY ?= /etc/default/secret.key
export STAGE ?= development
export MACHINE_ID := $(shell cat /etc/machine-id 2>/dev/null)

bootstrap:
	test $${STORAGE_PATH?Missing environment variable}
	mkdir -p $(abspath $(STORAGE_PATH))
	ln -s $(abspath $(STORAGE_PATH)) $(abspath storage)
	make decrypt-secret

update:
	make stop
	git pull --rebase
	git pull --rebase --depth=1 --allow-unrelated-histories
	make decrypt-secret
	docker compose --profile $(MACHINE_ID) pull
	make start
	docker system prune -a -f

start:
	echo $(MACHINE_ID)
	docker compose --profile $(MACHINE_ID) up -d --wait

pause:
	docker compose --profile $(MACHINE_ID) stop

stop:
	docker compose --profile $(MACHINE_ID) down

create-secret-key:
	openssl rand -out $(SECRET_KEY) -hex 64

encrypt-secret:
	for file in storage/secret/*; do \
		gpg --batch --pinentry-mode loopback --passphrase-file $(SECRET_KEY) -c --cipher-algo AES256 -o secret/$$(basename "$$file").gpg "$$file"; \
	done

decrypt-secret:
	mkdir -p storage/secret/
	for file in secret/*.gpg; do \
		gpg --batch --yes --pinentry-mode loopback --passphrase-file $(SECRET_KEY) -o storage/secret/$$(basename "$$file" .gpg) -d "$$file"; \
	done

scan:
	ggshield secret scan repo .