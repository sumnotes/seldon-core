CHARTS=seldon-core-crd seldon-core seldon-core-analytics seldon-core-kafka seldon-core-loadtesting seldon-single-model seldon-abtest seldon-mab seldon-od-vae seldon-od-if seldon-od-s2s-lstm seldon-od-md


build_all:
	make clean package get_index update_index

push_all:
	gsutil cp build/index.yaml build/*.tgz gs://seldon-charts/


package:
	mkdir -p build && \
		helm package $(CHARTS) && \
		mv *.tgz build/

get_index:
	mkdir -p build && \
		wget https://storage.googleapis.com/seldon-charts/index.yaml && \
		mv index.yaml build/ && \
		cp -v ./build/index.yaml ./build/index.yaml.orig

update_index:
	cd build && \
		helm repo index --merge index.yaml --url https://storage.googleapis.com/seldon-charts ./

clean:
	rm -rfv build

