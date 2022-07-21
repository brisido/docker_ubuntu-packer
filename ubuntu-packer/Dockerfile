FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PACKER_VERSION="1.8.2"
ENV HOME=/tmp

# Update, upgrade and install basic packages
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y curl wget zip python3 ansible && \
    apt-get autoremove && apt-get autoclean

# Create symbolic link to python3
RUN ln -sf python3 /usr/bin/python

# Install AWS Session Manager Plugin
RUN curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb" && \
    dpkg -i session-manager-plugin.deb && \
    rm session-manager-plugin.deb

# Install Packer
RUN wget https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip && \
    unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin && \
    rm packer_${PACKER_VERSION}_linux_amd64.zip

ENTRYPOINT ["bin/packer"]