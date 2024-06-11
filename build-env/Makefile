###
# Makefile to build and release Docker images used in our CI/CD build pipeline and deployments
###

.DEFAULT_GOAL := Dockerfile

SHELL := /bin/bash

.PHONY: help
help:
	@echo ""
	@echo "Makefile to build Docker base container images"
	@echo ""
	@echo "Targets:"
	@echo "  help:             Show this help."
	@echo "  deps:             Verify if dependencies to build container images are available."
	@echo "  Dockerfile:       Generate Dockerfile for the project for local build and development."
	@echo "  clean:            Delete Dockerfile"
	@echo ""

.PHONY: deps
deps:
	command -v envsubst;
	command -v docker;

Dockerfile: deps
	@echo -n "Generating Dockerfile:        "
	@source ./version-lock.sh && envsubst < "Dockerfile.tpl" > "Dockerfile"
	@echo -e "\033[0;32mDONE\033[0m"

.PHONY: clean
clean:
	@echo -n "Delete Dockerfile:            "
	@rm Dockerfile
	@echo -e "\033[0;32mDONE\033[0m"
