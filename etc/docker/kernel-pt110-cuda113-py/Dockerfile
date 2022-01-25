
ARG CUDA_VERSION=11.5
ARG PYTORCH_VERSION=1.10.0
ARG BASE_CONTAINER=hub.gexcp.com/elyra/elyra:latest

FROM $BASE_CONTAINER

RUN conda install -c pytorch -c conda-forge -c nvidia -y \
    magma-cuda115 \
    pytorch=$PYTORCH_VERSION \
    astunparse \
    ninja pyyaml mkl mkl-include setuptools cmake cffi typing_extensions future six requests dataclasses \
    cudatoolkit=$CUDA_VERSION \
    cudatoolkit-dev \
    scikit-learn \
    pandas \
    gcc_linux-64 \
    cxx-compiler \
    pyyaml \
    cython && \
    conda clean -tipsy


