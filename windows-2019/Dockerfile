# escape=`

FROM octopuslabs/workertools:latest-windows.2019
SHELL ["powershell", "-Command"]

ARG GOOGLE_CLOUD_CLI_VERSION=362.0.0

# Install Terraform
RUN choco install terraform -y --no-progress

# Install gcloud
RUN $GCLOUD_VERSION = $env:GOOGLE_CLOUD_CLI_VERSION; `
    Write-Host "GCLOUD_VERSION: $GCLOUD_VERSION"; `
    $GOOGLE_CLOUD_DOWNLOAD_URI = "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-$GCLOUD_VERSION-windows-x86_64.zip"; `
    Write-Host "GOOGLE_CLOUD_DOWNLOAD_URI: $GOOGLE_CLOUD_DOWNLOAD_URI"; `
    Invoke-WebRequest -Uri $GOOGLE_CLOUD_DOWNLOAD_URI -OutFile google-cloud-sdk-$GCLOUD_VERSION-windows-x86_64.zip; `
    # UNZIP AND INSTALL gcloud
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$GCLOUD_VERSION-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$GCLOUD_VERSION-windows-x86_64.zip
