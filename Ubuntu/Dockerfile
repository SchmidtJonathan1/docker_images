# Use latest Container
FROM ubuntu:latest

# Install system packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       openssh-server \
       vim \
       curl\
       git \
       net-tools \
       build-essential \
       locales \
       libffi-dev \
       libssl-dev \
       libyaml-dev \
       python3-dev \
       python3-setuptools \
       python3-pip \
       python3-apt \
       python3-yaml \
       software-properties-common \
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Update pip and install python dependencies
RUN python3 -m pip install --no-cache-dir -U pip

# Create user and group
RUN useradd -rm -d /home/ansible -s /bin/bash -g root -G sudo -u 1000 ansible 

# Change password after ansible: on line 34
RUN  echo 'ansible:tEsT!' | chpasswd

# Change workdir to ansible user
WORKDIR /home/ansible