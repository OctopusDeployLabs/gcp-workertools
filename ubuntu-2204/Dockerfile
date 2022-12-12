FROM octopuslabs/workertools:latest-ubuntu.2204

ARG DEBIAN_FRONTEND noninteractive
ARG GOOGLE_CLOUD_CLI_VERSION=362.0.0-0

# Get Terraform
# https://developer.hashicorp.com/terraform/downloads
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform

# Install Google Cloud CLI
# https://cloud.google.com/sdk/docs/downloads-apt-get
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    apt-get install -y ca-certificates gnupg && \
    wget -q -O - https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
    apt-get update && apt-get install -y google-cloud-sdk=${GOOGLE_CLOUD_CLI_VERSION}