# escape=`

FROM octopuslabs/workertools:latest-windows.2019
SHELL ["powershell", "-Command"]

ARG GOOGLE_CLOUD_CLI_VERSION=362.0.0
ARG PYTHON_VERSION=3.8.5

# Install Terraform
RUN choco install terraform -y --no-progress

# Install python
RUN choco install -y python3 --version $Env:PYTHON_VERSION --no-progress; `
    refreshenv

# Install gcloud
RUN $GCLOUD_VERSION = $env:GOOGLE_CLOUD_CLI_VERSION; `
    Write-Host "GCLOUD_VERSION: ${env:GOOGLE_CLOUD_CLI_VERSION}"; `
    Write-Host "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip"; `
    Invoke-WebRequest "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip" -OutFile google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip
