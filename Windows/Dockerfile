# Dockerfile for windows container with winrm
# Size from image ~ 3.8 GB
# Use " docker.exe build -t winrm . " to build
# Run container in WSL2 with "docker.exe run -it --rm --network WSL winrm powershell"

# Microsoft artifact registry container images: https://mcr.microsoft.com/en-us/catalog?page=8
# For more informations https://learn.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility

# Use servercor 2019 image
ARG TAG=ltsc2019
FROM mcr.microsoft.com/windows/servercore:$TAG

# Metadata indicating an image maintainer.
LABEL maintainer="Jonathan Schmidt"

# Supress progress and error
RUN ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Configure WinRM HTTP
RUN powershell.exe winrm quickconfig -q ; \
    winrm set winrm/config/service/Auth '@{Basic=\"true\"}' ; \
    winrm set winrm/config/service '@{AllowUnencrypted=\"true\"}' ; \
    winrm set winrm/config/winrs '@{MaxMemoryPerShellMB=\"1024\"}'

# Add localuser to administrator group
# Change Password at line 27, after ConvertTo-SecureString
RUN powershell.exe $Password = ConvertTo-SecureString tEsT! -AsPlainText -Force ; \
    New-LocalUser Ansible -Password $Password ; \
    Add-LocalGroupMember -Group Administrators -Member Ansible