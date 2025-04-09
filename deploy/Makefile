.PHONY: build

IMAGE := ghcr.io/sios-technology-inc/covas-docker-deploy:1.7.0

build:
	docker build -t $(IMAGE) .

push:
	docker push $(IMAGE)