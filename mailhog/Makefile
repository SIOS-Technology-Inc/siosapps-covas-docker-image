.PHONY: build push

IMAGE := ghcr.io/sios-technology-inc/covas-docker-mailhog:0.3.0

build:
	docker build -t $(IMAGE) .

push:
	docker push $(IMAGE)
