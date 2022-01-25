
ARG CUDA_VERSION=11.3
ARG PYTHON_VERSION=1.10.0
ARG BASE_CONTAINER=hub.gexcp.com/elyra/elyra:latest

FROM $BASE_CONTAINER

RUN conda install -y pytorch==$PYTHON_VERSION cudatoolkit=$CUDA_VERSION cudatoolkit-dev -c pytorch && \
    conda install -y scikit-learn pandas mkl-service cython && \
    conda clean -tipsy


