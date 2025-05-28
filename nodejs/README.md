
# ML runtimes with nodejs 
Good as a base image for AMP apps

*Pro tip -*
CAI_STUDIO_AGENT need a base image with python 11 and node.

## Build Examples

```
docker build -t <image name>:<TAG> .
docker build -t <my docker repos>/ml_runtime_node:<TAG> .
```


## Prebuilt
A prebuilt version is available on : `docker.io/22adc/ml_runtime_node:22-2025.01.3`

built by `docker build -t docker.io/22adc/ml_runtime_node:22-2025.01.3 --build-arg ML_RUNTIME_WORKBENCH_TYPE=python3.11-standard .`

## build option

The docker file expose 3 main argument with defualt value:

```
ARG ML_RUNTIME_BASE_VERSION=2025.01.3-b8
ARG ML_RUNTIME_WORKBENCH_TYPE=python3.11-standard
ARG NODEJS_VERSION=22
```

Feel free to override them with `--build-arg` or edit them directly in the docker file.