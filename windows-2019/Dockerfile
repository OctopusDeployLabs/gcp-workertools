# escape=`

FROM octopuslabs/workertools:latest-windows.2019
SHELL ["powershell", "-Command"]

ARG 7Zip_Version=19.0
ARG Google_Cloud_Cli_Version=362.0.0

# Install Terraform
RUN choco install terraform -y --no-progress

# # Install 7ZIP because gcloud
RUN choco install 7zip -y --version $Env:7Zip_Version --no-progress

# # Install gcloud
RUN Invoke-WebRequest "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-$Env:Google_Cloud_Cli_Version-windows-x86_64.zip" -OutFile google-cloud-sdk-$Env:Google_Cloud_Cli_Version-windows-x86_64.zip; `
    # # UNZIP AND INSTALL gcloud
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$Env:Google_Cloud_Cli_Version-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$Env:Google_Cloud_Cli_Version-windows-x86_64.zip
