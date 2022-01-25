
ARG CUDA_VERSION=11.3
ARG PYTORCH_VERSION=1.10.0

ARG CUDA_IMAGE=hub.gexcp.com/docker/nvidia/cuda:11.3.1-base-ubuntu20.04
#ARG CUDA_IMAGE=hub.gexcp.com/docker/pytorch/pytorch:${PYTORCH_VERSION}-cuda${PYTORCH_CUDA}-cudnn8-devel
ARG BASE_CONTAINER=hub.gexcp.com/elyra/elyra:latest

FROM $CUDA_IMAGE as BUILD


FROM $BASE_CONTAINER

ENV CUDA_HOME=/usr/local/cuda
ENV CUDA_ROOT=$CUDA_HOME
ENV PATH=$PATH:$CUDA_ROOT/bin
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CUDA_ROOT/lib64

COPY --from=build /usr/local/cuda $CUDA_HOME

RUN conda install -c pytorch -c conda-forge -c nvidia -y \
    magma-cuda113 \
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

