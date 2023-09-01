# マウント先は `SELECT @@plugin_dir;` して確認した
.PHONY: run
run:
	docker run --rm -dit --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v $(PWD)/../../build/plugin_output_directory/:/usr/lib64/mysql/plugin:ro mysql:8.1.0

.PHONY: install
install:
	docker exec -it mysql mysql -e "INSTALL PLUGIN foo SONAME 'ha_foo.so';"
	docker exec -it mysql mysql -e "SHOW ENGINES;" | grep -e FOO -e Engine

.PHONY: exec
exec:
	docker exec -it mysql bash

.PHONY: stop
stop:
	docker stop mysql

.PHONY: clean
clean:
	cd "$(PWD)/../../build/" && \
	make clean && \
	rm CMakeCache.txt; \
	cmake .. -DDOWNLOAD_BOOST=1 -DWITH_BOOST=./boost

.PHONY: build
build:
	cd "$(PWD)/../../build/" && \
	make foo