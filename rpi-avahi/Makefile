include ../misc/Makefile

VERSION    := 0.6.31
IMAGE_NAME := chtison/rpi-avahi

NAME :=
HOST := example.$(shell hostname).local
IP   := $(shell ifconfig eth0 | grep 'inet addr:' | awk -F'[ :]+' '{print $$4}')
define RUN
@[ "$(HOST)" ] || (echo '+ HOST parameter is required, example: make run HOST=docker.local' && false)
docker run -d                                           \
	-v /var/run/dbus:/var/run/dbus                  \
	`[ "$(NAME)" ] && echo --name $(NAME)`          \
	$(IMAGE_NAME) avahi-publish -a -R $(HOST) $(IP)
endef
