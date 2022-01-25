
ARG BASE_CONTAINER=hub.gexcp.com/elyra/torch110-cuda113-py
ARG CUDA_VERSION=11.3
ARG PYTHON_VERSION=1.10.0

FROM $BASE_CONTAINER as BUILD


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

RUN pip install --upgrade \
    jupyterlab \
    elyra[all] \
    jupyterlab_tabnine \
    jupyterlab-horizon-theme \
    jupyterlab-github \
    jupyterlab_s3_browser \
    jlab-enhanced-launcher
 
RUN jupyter server extension enable jupyterlab_github && \
    jupyter lab build

