# This is used by the image building script referenced below. Normally it just takes the directory name but in this
# case we want it to be called something else.
IMAGE_NAME=flytecookbook
VERSION=$(shell ./version.sh)

# The Flyte project that we want to register under
PROJECT=flytesnacks

# Uncomment after adding the NOPUSH option to the build script
# REGISTRY=docker.io/lyft

.PHONY: docker_build
docker_build:
	IMAGE_NAME=${IMAGE_NAME} flytekit_build_image.sh .

.PHONY: docker_build
docker_push:
	IMAGE_NAME=${IMAGE_NAME} REGISTRY=docker.io/lyft flytekit_build_image.sh .

.PHONY: in_container_register_sandbox
in_container_register_sandbox:
	pyflyte -p ${PROJECT} -d development --config /root/sandbox.config register workflows

.PHONY: register_sandbox
register_sandbox: docker_push
	docker run docker.io/lyft/flytecookbook:${VERSION} /usr/local/bin/flytekit_venv make in_container_register_sandbox

.PHONY: in_container_serialize_sandbox
in_container_serialize_sandbox:
	pyflyte -p ${PROJECT} -d development --config /root/sandbox.config serialize workflows

.PHONY: serialize_sandbox
serialize_sandbox: docker_push
	docker run docker.io/lyft/flytecookbook:${VERSION} -v .:/root make in_container_serialize_sandbox

.PHONY: book
book:
	@docker run -t -v `pwd`:/base lyft/docbuilder:v2.2.0 sphinx-build -E -b html /base/ /base/_build