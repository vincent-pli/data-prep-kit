
# Define the root of the local git clone for the common rules to be able 
# know where they are running from.
REPOROOT=../../../..
# Include a library of common .transform.* targets which most
# transforms should be able to reuse.  However, feel free
# to override/redefine the rules below. 
include $(REPOROOT)/transforms/.make.transforms

TRANSFORM_NAME=filter

BASE_IMAGE=${RAY_BASE_IMAGE}
venv::	.transforms.ray-venv

test::	.transforms.ray-test

clean:: .transforms.clean

image:: .transforms.ray-image

test-src:: .transforms.test-src

setup:: .transforms.setup

test-image:: .transforms.ray-test-image

build:: build-dist image

publish: publish-image

publish-image:: .transforms.publish-image-ray

set-versions:
	$(MAKE) TRANSFORM_PYTHON_VERSION=$(FILTER_PYTHON_VERSION) TOML_VERSION=$(FILTER_RAY_VERSION) .transforms.set-versions
        
build-dist:: .defaults.build-dist 

publish-dist:: .defaults.publish-dist

run-cli-sample: 
	$(MAKE) RUN_FILE=$(TRANSFORM_NAME)_transform_ray.py \
                RUN_ARGS="--run_locally True --data_local_config \"{ 'input_folder' : '../test-data/input', 'output_folder' : '../output'}\"  \
                --filter_criteria_list \"[ 'docq_total_words > 100 AND docq_total_words < 200', 'ibmkenlm_docq_perplex_score < 230']\"	\
		--filter_columns_to_drop \"[ 'extra', 'cluster' ]\" "	\
                .transforms.run-src-file

run-local-sample: .transforms.run-local-ray-sample

run-s3-sample: .transforms.run-s3-ray-sample

minio-start:	.minio-start

kind-load-image:: .transforms.kind-load-image

docker-load-image: .defaults.docker-load-image

docker-save-image: .defaults.docker-save-image
