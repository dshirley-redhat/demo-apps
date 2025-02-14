# Use a base image, such as ubuntu
FROM image-registry.openshift-image-registry.svc:5000/cicd-tools/ubuntu:24.04

USER root

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -y \
    curl \
    git \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    lsb-release \
    sudo \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

ENV GO_VERSION=1.23.1 \
    GO_DL_LOCATION=/tmp/go

RUN curl -Lo ${GO_DL_LOCATION} https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf ${GO_DL_LOCATION} && \
    rm -rf ${GO_DL_LOCATION} && \
    export PATH=$PATH:/usr/local/go/bin
ENV PATH=$PATH:/usr/local/go/bin

RUN curl -L -o /tmp/kubebuilder "https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH)" && \
    chmod +x /tmp/kubebuilder && \
    mv /tmp/kubebuilder /usr/local/bin

WORKDIR /workspaces

RUN useradd -ms /bin/bash apprunner
RUN alias ll='ls -alF'
USER apprunner

# Set default command

CMD ["/bin/bash", "-c", "while true; do sleep 1; done"]
ENTRYPOINT ["/bin/bash"]