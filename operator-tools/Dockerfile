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

RUN export KUBEBUILDER_VERSION=4.5.0
RUN export KUBEBUILDER_URL=https://github.com/kubernetes-sigs/kubebuilder/archive/refs/tags/v$KUBEBUILDER_VERSION.tar.gz

# Install Kubebuilder
RUN curl -Lo /tmp/kubebuilder.tar.gz $KUBEBUILDER_URL \
    && tar -zxvf /tmp/kubebuilder.tar.gz -C /tmp/ \
    && ls -la /tmp \
    && mv /tmp/kubebuilder_$KUBEBUILDER_VERSION/kubebuilder /usr/local/bin/ \
    && rm -rf /tmp/kubebuilder.tar.gz /tmp/kubebuilder_$KUBEBUILDER_VERSION

# Ensure git and kubebuilder are on the PATH
ENV PATH="/usr/local/bin:${PATH}"

# Verify installations
RUN git --version && kubebuilder version

# Set default command
CMD [ "bash" ]