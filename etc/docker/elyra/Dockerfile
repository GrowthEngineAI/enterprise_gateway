# Elyra Dev Base Container
ARG BASE_CONTAINER=elyra/elyra:dev
FROM $BASE_CONTAINER

RUN pip install \
    jupyterlab_tabnine \
    jupyterlab-horizon-theme \
    jupyterlab-github \
    jupyterlab_s3_browser \
    jlab-enhanced-launcher
 
RUN jupyter server extension enable jupyterlab_github && \
    jupyter lab build
