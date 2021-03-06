# Variables can be overridden by setting environment variables

FACTORIO_PATH ?= ~/.factorio
SECURITY_PATH ?= $(FACTORIO_PATH)/security
SAVES_PATH ?= $(FACTORIO_PATH)/saves
MODS_PATH ?= $(FACTORIO_PATH)/mods
ADMIN_PASS ?= "" # Left empty to allow password to be autogenerated
PORT_FORWARD ?= -p 80:80 -p 443:443 -p 34197:34197/udp

build:
	docker build -t factorio-server-manager .

logs:
	docker logs factorio-server
	echo "Nginx Access Logs"
	docker exec -it factorio-server cat /var/log/nginx/access.log
	echo "Nginx Error Logs"
	docker exec -it factorio-server cat /var/log/nginx/error.log

run:
	docker run -d --name factorio-server -v $(SECURITY_PATH):/security -v $(SAVES_PATH):/opt/factorio/saves -v $(MODS_PATH):/opt/factorio/mods $(PORT_FORWARD) -e ADMIN_PASSWORD=$(ADMIN_PASS) factorio-server-manager

stop:
	docker stop factorio-server
	docker rm factorio-server

clean:
	docker rmi factorio-server-manager
