# escape=`

FROM octopuslabs/workertools:latest-windows.2019
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install terraform -y --no-progress

# Install Google Cloud CLI
RUN choco install gcloudsdk -y --no-progress
