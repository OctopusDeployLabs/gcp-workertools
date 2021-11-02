# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019
SHELL ["powershell", "-Command"]

ARG GOOGLE_CLOUD_CLI_VERSION=362.0.0

# Python Greater than 3.9 will not work with Google Cloud SDK 
# https://github.com/googleapis/google-auth-library-python/issues/418
ARG PYTHON_VERSION=3.8.5

# Install Choco
RUN $ProgressPreference = 'SilentlyContinue'; `
    Set-ExecutionPolicy Bypass -Scope Process -Force; `
    [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Install 7ZIP
RUN choco install 7zip -y --no-progress

# Install Powershell Core
RUN choco install powershell-core -y --no-progress

# Install python
RUN choco install -y python3 --version $env:PYTHON_VERSION --no-progress; `
    refreshenv

# Install Terraform
RUN choco install terraform -y --no-progress

# Install gcloud
RUN $GCLOUD_VERSION = $env:GOOGLE_CLOUD_CLI_VERSION; `
    Write-Host "GCLOUD_VERSION: ${env:GOOGLE_CLOUD_CLI_VERSION}"; `
    Write-Host "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip"; `
    Invoke-WebRequest "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip" -OutFile google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip

# Update Path
RUN $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $gcloudPath = ';C:\google-cloud-sdk\bin'; `    
    $new = $old + $gcloudPath; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    refreshenv