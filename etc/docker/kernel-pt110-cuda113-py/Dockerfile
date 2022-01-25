
ARG BASE_CONTAINER=hub.gexcp.com/elyra/elyra:dev
ARG CUDA_VERSION=11.3
ARG PYTHON_VERSION=1.10.0

FROM $BASE_CONTAINER as BUILD

RUN apt-get update && \
    apt-get install -y --no-install-recommends git curl wget unzip bzip2 build-essential ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN conda install -y pytorch==$PYTHON_VERSION cudatoolkit=$CUDA_VERSION cudatoolkit-dev -c pytorch && \
    conda install -y scikit-learn pandas mkl-service cython && \
    conda clean -tipsy

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

