FROM pytorch/pytorch:2.4.1-cuda12.1-cudnn9-devel

SHELL ["/bin/bash", "-lc"]

ARG USERNAME="vscode"
ARG DEVELOPER_HOME="/home/${USERNAME}"

VOLUME ["/models"]

# Install updates
RUN apt update && apt upgrade -y
RUN apt install -y git libgl1
RUN apt clean

# Update pip
ENV PIP_BREAK_SYSTEM_PACKAGES=1
RUN python -m pip install -q --upgrade pip

RUN pip install -q torch-scatter --no-build-isolation
RUN pip install -q https://github.com/Dao-AILab/flash-attention/releases/download/v2.8.3.post2/flash_attn-2.8.3.post2+cu12torch2.4cxx11abiFALSE-cp311-cp311-linux_x86_64.whl

# Install requirements
COPY ./requirements.txt ${DEVELOPER_HOME}/workspace/
RUN pip install -q -r ${DEVELOPER_HOME}/workspace/requirements.txt
