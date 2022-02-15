# use some sensible default shell settings
SHELL := /bin/bash
$(VERBOSE).SILENT:
.DEFAULT_GOAL := help

# used by docker-compose to run containers with current user ID
CURRENT_UID := $(shell id -u)
CURRENT_GID := $(shell id -g)

DOCKER_COMPOSE_PULL := $(shell docker-compose pull || true)

# reusable docker-compose command
DOCKER_COMPOSE := docker-compose run --user="$(CURRENT_UID)"

GENERATE_PASSWD_RESULT:=$(shell $(DOCKER_COMPOSE) -e USER_ID=$(CURRENT_UID) -e GROUP_ID=$(CURRENT_GID)  passwd-gen > passwd)

# docker-compose calls
ANSIBLE := $(DOCKER_COMPOSE) ansible
ANSIBLE_BASH := $(DOCKER_COMPOSE) --entrypoint="/bin/bash" ansible
ANSIBLE_PLAYBOOK := $(DOCKER_COMPOSE) --entrypoint="ansible-playbook" ansible

##@ Entry Points

.PHONY: ansible-logging-deploy
ansible-api-certificate:
	$(ANSIBLE_PLAYBOOK) -vvv "./playbook.yaml"

.PHONY: ansible-bash
ansible-bash: 
	$(ANSIBLE_BASH)