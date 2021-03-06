include ../misc/Makefile

VERSION       := 3.12.1
IMAGE_NAME    := chtison/rpi-rqlite

RQLITE_TAR_GZ := v$(VERSION).tar.gz
URL           := https://github.com/rqlite/rqlite/archive

DOCKER_BUILD_OPTIONS := --build-arg RQLITE_TAR_GZ=$(RQLITE_TAR_GZ)

TMP := $(USAGE)
define USAGE
$(TMP)
make fclean           # remove: $(RQLITE_TAR_GZ) and .dockerignore
endef

.PHONY: fclean
fclean:
	rm -f -- $(RQLITE_TAR_GZ) .dockerignore

define RUN
@[ "$(IP)" ] || (echo '+ IP parameter is required, example: make run IP=192.168.0.42' && false)
docker run -d                     \
	--restart=unless-stopped  \
	--name rqlited            \
	--net=host                \
	--volume rqlited:/data    \
	$(IMAGE_NAME)             \
	-http $(IP):4001          \
	-raft $(IP):4002          \
	-ondisk /data
endef

build: $(RQLITE_TAR_GZ) .dockerignore

$(RQLITE_TAR_GZ):
	$(CURL) $(URL)/$(RQLITE_TAR_GZ)

.dockerignore:
	echo -e '*\n!$(RQLITE_TAR_GZ)' > .dockerignore
