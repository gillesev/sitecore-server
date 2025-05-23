# sitecore-server
Containerized Sitecore XM with JSS

# WARNING
You need a valid Sitecore license under c:\license\license.xml to use this sample application.

# Instructions
This sample will setup the required configuration to build and run the minimum Sitecore XM set of containers to enable the JSS Headless engine.
The images also make use of the sitecore-docker-tools-assets image used to deploy files into the containers: See https://doc.sitecore.com/xp/en/developers/latest/developer-tools/deploying-files-into-running-containers.html#apply-to-sitecore-runtime-images

## Initialize the configuration
in PS>
./init.ps1 -LicenseXmlPath "c:\license\license.xml" -AdminPassword "Password12345"

## Build and Run the containers
in PS>
docker compose up -d

## Tear down the container environment
in PS>
docker compose down
