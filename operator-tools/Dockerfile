# Use a base image, such as ubuntu
FROM ubuntu:20.04

USER root

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y \
    curl \
    git \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    lsb-release \
    sudo \
    && rm -rf /var/lib/apt/lists/*

RUN KUBEBUILDER_URL=https://github.com/kubernetes-sigs/kubebuilder/archive/refs/tags/v4.5.0.tar.gz

# Install Kubebuilder
RUN curl -Lo /tmp/kubebuilder.tar.gz $KUBEBUILDER_URL \
    && tar -zxvf /tmp/kubebuilder.tar.gz -C /tmp/ \
    && mv /tmp/kubebuilder_3.3.0_linux_amd64/kubebuilder /usr/local/bin/ \
    && rm -rf /tmp/kubebuilder.tar.gz /tmp/kubebuilder_3.3.0_linux_amd64

# Ensure git and kubebuilder are on the PATH
ENV PATH="/usr/local/bin:${PATH}"

# Verify installations
RUN git --version && kubebuilder version

# Set default command
CMD [ "bash" ]