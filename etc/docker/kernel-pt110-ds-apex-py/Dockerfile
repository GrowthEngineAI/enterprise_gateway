

ARG CUDA_VERSION=11.3
ARG PYTHON_VERSION=1.10.0
ARG BASE_CONTAINER=hub.gexcp.com/elyra/kernel-pt110-cuda113-py:latest
FROM $BASE_CONTAINER


RUN pip install --upgrade pip && \
    pip install triton==1.0.0 ninja --extra-index-url https://pypi.ngc.nvidia.com

RUN mkdir -p /tmp/ds && \
    cd /tmp/ds && git clone https://github.com/NVIDIA/apex && \
    TORCH_CUDA_ARCH_LIST="7.0 7.5 8.0" pip install --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./apex

RUN cd /tmp/ds && git clone https://github.com/microsoft/DeepSpeed && \
    apt-get update && apt-get install -y --no-install-recommends libaio-dev && \
    TORCH_CUDA_ARCH_LIST="7.0 7.5 8.0" DS_BUILD_CPU_ADAM=1 DS_BUILD_UTILS=1 DS_BUILD_OPS=1 pip install \
    -v --global-option="build_ext" --global-option="-j4" --no-cache-dir --extra-index-url https://pypi.ngc.nvidia.com \
    --disable-pip-version-check ./DeepSpeed
