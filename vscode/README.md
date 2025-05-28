# Build Examples

# VsCode for ML runtimes


docker build -t <my docker repos>/vscode:<TAG> .

An prebuilt version is available on : docker.io/22adc/ml_runtime_vscode:2025.01.1

the docker file expose 3 main argument with defualt value:

ARG ML_RUNTIME_BASE_VERSION=2025.01.3-b8
ARG ML_RUNTIME_WORKBENCH_TYPE=python3.10-standard
ARG VSCODE_SERVER_VERSION=4.100.2

feel free to override them with `--build-arg` or edit them directly in the docker file.