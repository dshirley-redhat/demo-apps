# Use a base image, such as ubuntu
FROM ubuntu:24.04

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

ENV GO_VERSION=1.23.1
ENV GO_DL_LOCATION=/tmp/go

RUN curl -Lo ${GO_DL_LOCATION} https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local/bin -xzf ${GO_DL_LOCATION} && \
    rm -rf ${GO_DL_LOCATION}
RUN ls -la /usr/local/bin

#ENV KUBEBUILDER_VERSION=4.5.0 \
#    KUBEBUILDER_URL=https://github.com/kubernetes-sigs/kubebuilder/archive/refs/tags/v${KUBEBUILDER_VERSION}.tar.gz
#RUN echo "url ${KUBEBUILDER_URL}"

RUN curl -L -o kubebuilder "https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH)"

# Install Kubebuilder
#RUN curl -Lo /tmp/kubebuilder.tar.gz https://github.com/kubernetes-sigs/kubebuilder/archive/refs/tags/v4.5.0.tar.gz \
#    && tar -zxvf /tmp/kubebuilder.tar.gz -C /tmp/ \
#    && ls -la /tmp \
#    && mv /tmp/kubebuilder_4.5.0/kubebuilder /usr/local/bin/ \
#    && rm -rf /tmp/kubebuilder.tar.gz /tmp/kubebuilder_4.5.0

# Ensure git and kubebuilder are on the PATH
ENV PATH="/usr/local/bin:${PATH}"

# Verify installations
RUN git --version && kubebuilder version

# Set default command
CMD [ "bash" ]