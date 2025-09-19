---
title: Terraforming into Azure
categories:
tags: terraform
aliases:
share: true
---
# 2025-07-12-Deploy Uptime Kuma in Azure App Service Plan

I have been exploring the possibility of integrating an open-source project into an enterprise environment. When self-hosting such a project, you assume full responsibility for ongoing maintenance and troubleshooting, as there is no vendor support to call upon.

One project that recently caught my attention is Uptime Kuma, a straightforward synthetic monitoring tool. It monitors website status, certificate expirations, DNS record validations, and more. There are multiple notification options available; I chose to use a webhook to send instant alerts to a Microsoft Teams channel.

I have already created an Azure DevOps project and begun developing Terraform deployment files for automation. I will share the project files in due course.

A high level solution design.

![Terraform2Azure-AppService-Docker-UptimeKuma.png](/images/Terraform2Azure-AppService-Docker-UptimeKuma.png)

Consider restricting access to the web application if you only want to use it internally, you can limit the access from specific IP address from the Networking blade of the App Service. Or use Private Endpoint.
