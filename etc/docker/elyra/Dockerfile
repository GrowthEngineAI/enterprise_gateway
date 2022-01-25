# Elyra Dev Base Container
ARG BASE_CONTAINER=elyra/elyra:dev
FROM $BASE_CONTAINER

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends fuse s3fs git curl wget unzip bzip2 build-essential ca-certificates && \
    export GCSFUSE_REPO=gcsfuse-`lsb_release -c -s` && \
    echo "deb http://packages.cloud.google.com/apt $GCSFUSE_REPO main" | sudo tee /etc/apt/sources.list.d/gcsfuse.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - && \
    apt-get -qq update && sudo apt-get install -y -qq gcsfuse && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

RUN pip install --upgrade \
    jupyterlab \
    gsutil \
    elyra[all] \
    jupyterlab_tabnine \
    jupyterlab-horizon-theme \
    jupyterlab-github \
    jupyterlab_s3_browser \
    jlab-enhanced-launcher
 
RUN jupyter server extension enable jupyterlab_github && \
    jupyter lab build
