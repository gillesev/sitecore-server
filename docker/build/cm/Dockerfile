# escape=`

ARG NODEJS_VERSION
ARG PARENT_IMAGE
ARG TOOLS_IMAGE
ARG HEADLESS_SERVICES_IMAGE

FROM ${TOOLS_IMAGE} as tools
FROM ${HEADLESS_SERVICES_IMAGE} AS headless_services
FROM ${PARENT_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

WORKDIR C:\inetpub\wwwroot

# Install nodejs
RUN curl.exe -o C:\node.msi https://nodejs.org/v%NODEJS_VERSION%/node-v%NODEJS_VERSION%-x64.msi
RUN Start-Process msiexec.exe -ArgumentList '/i', 'c:\\node.msi', '/quiet', '/norestart' -NoNewWindow -Wait;

# Copy developer tools and entrypoint
COPY --from=tools C:\tools C:\tools

# Copy and init the JSS / Headless Services Module
COPY --from=headless_services C:\module\cm\content C:\inetpub\wwwroot
COPY --from=headless_services C:\module\tools C:\module\tools
RUN C:\module\tools\Initialize-Content.ps1 -TargetPath C:\inetpub\wwwroot; `
    Remove-Item -Path C:\module -Recurse -Force;
