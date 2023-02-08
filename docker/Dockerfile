FROM nvidia/cuda:12.0.0-devel-ubuntu20.04

# bypass any required inputs
ENV DEBIAN_FRONTEND=noninteractive

# Set up dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential \ 
    wget curl software-properties-common git unzip

# install python
RUN apt-get update && \
    apt-get install -y --no-install-recommends \ 
    python-is-python3 python3-pip

# install the python libraries we want
RUN python3 -m pip --no-cache-dir install --upgrade \
    notebook matplotlib 

WORKDIR /root

RUN git clone https://github.com/huggingface/ml-agents/

WORKDIR /root/ml-agents

RUN pip3 install -e ./ml-agents-envs && \
    pip3 install -e ./ml-agents && \
    mkdir -p ./trained-envs-executables/linux && \
    wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1zv3M95ZJTWHUVOWT6ckq_cm98nft8gdF' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1zv3M95ZJTWHUVOWT6ckq_cm98nft8gdF" \
    -O ./trained-envs-executables/linux/Huggy.zip && \
    rm -rf /tmp/cookies.txt && \
    unzip -d ./trained-envs-executables/linux/ ./trained-envs-executables/linux/Huggy.zip

RUN chmod +rwx -R /root/ml-agents/trained-envs-executables/linux/Huggy