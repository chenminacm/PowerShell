# Docker image file that describes an fedora 25 image with PowerShell installed from Microsoft YUM Repo

FROM fedora:26

ARG POWERSHELL_VERSION=6.0.0-beta.8
ARG IMAGE_NAME=microsoft/powershell:fedora26

LABEL maintainer="PowerShell Team <powershellteam@hotmail.com>" \
      readme.md="https://github.com/PowerShell/PowerShell/blob/master/docker/README.md" \
      description="This Dockerfile will install the latest release of PS." \
      org.label-schema.usage="https://github.com/PowerShell/PowerShell/tree/master/docker#run-the-docker-image-you-built" \
      org.label-schema.url="https://github.com/PowerShell/PowerShell/blob/master/docker/README.md" \
      org.label-schema.vcs-url="https://github.com/PowerShell/PowerShell" \
      org.label-schema.name="powershell" \
      org.label-schema.vendor="PowerShell" \
      org.label-schema.version=${POWERSHELL_VERSION} \
      org.label-schema.schema-version="1.0" \
      org.label-schema.docker.cmd="docker run ${IMAGE_NAME} powershell -c '$psversiontable'" \
      org.label-schema.docker.cmd.devel="docker run ${IMAGE_NAME}" \
      org.label-schema.docker.cmd.test="docker run ${IMAGE_NAME} powershell -c Invoke-Pester" \
      org.label-schema.docker.cmd.help="docker run ${IMAGE_NAME} powershell -c Get-Help"

# TODO: addd LABEL org.label-schema.vcs-ref=${VCS_REF}

# Install dependencies and clean up
RUN dnf install -y \       
        curl \
        glibc-locale-source \
    && dnf clean all

# Setup the locale
ENV LANG en_US.UTF-8
ENV LC_ALL $LANG
RUN localedef --charmap=UTF-8 --inputfile=en_US $LANG

# Download and configure Microsoft Repository config file
RUN curl https://packages.microsoft.com/config/rhel/7/prod.repo | tee /etc/yum.repos.d/microsoft.repo

# Install latest powershell from Microsoft YUM Repo
RUN dnf install -y powershell

# Use array to avoid Docker prepending /bin/sh -c
CMD [ "powershell" ]
