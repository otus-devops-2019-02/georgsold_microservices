USER_NAME=georgsold

#собери их все

build_all: build_ui build_post build_comment build_prometheus build_mongodb_exporter
push_all: push_ui push_post push_comment push_prometheus push_mongodb_exporter

build_ui: 
	cd ../src/ui/ && bash docker_build.sh

build_post:
	cd ../src/post-py/ bash docker_build.sh

build_comment: 
	cd ../src/comment/ && bash docker_build.sh

build_prometheus: 
	cd ../monitoring/prometheus && docker build -t ${USER_NAME}/prometheus .

build_mongodb_exporter:
	# В домашке не указано, надо ли пушить это все в репу, поэтому храним в темпах и постоянно берем свежую

	rm -rf /tmp/mongodb_exporter && cd /tmp && git clone https://github.com/percona/mongodb_exporter.git
	cd /tmp/mongodb_exporter && make docker DOCKER_IMAGE_TAG="latest"

push_ui:
	docker push $(USER_NAME)/ui

push_post:
	docker push $(USER_NAME)/post

push_comment:
	docker push $(USER_NAME)/comment

push_prometheus:
	docker push $(USER_NAME)/prometheus

push_mongodb_exporter:
	docker push $(USER_NAME)/mongodb_exporter
