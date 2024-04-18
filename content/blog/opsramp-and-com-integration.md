---
title: COM and OpsRamp custom integration
date: 2024-04-18T04:56:08.289Z
author: Mahesh T R
authorimage: /img/mahesh_photo.jpeg
thumbnailimage: /img/com_opsramp_logo.jpeg
disable: false
---
OpsRamp and COM integration has following advantages

* Multi-vendor view of basic hardware metrics of HPE servers and non-HPE servers in OpsRamp dashboard.
* Multi-vendor view of OS and workload level metrics of HPE servers and non-HPE servers in OpsRamp dashboard.
* OpsRamp will aggregate the metrics ingested from COM and metrics ingested from 3rd party servers and show an aggregate view in OpsRamp dashboard.

Broadway service in COM allowing customers to register a webhook to receive events from COM. Also, OpsRamp provide the capability to build integration using the [Custom Integration framework](https://docs.opsramp.com/integrations/a2r/custom-integration/custom-integration).

Both components provide interfaces for loose integration. If any data sent from COM to OpsRamp is called as outbound. If any data received from COM is called as inbound.



For establishing outbound connection between COM/OpsRamp following steps required.

Step #1: Generate GLCP Access Token for authenticating to COM webhook

GLCP access token is required for authenticating to COM webhook. Please login to GLCP to fetch [Access Token](https://developer.greenlake.hpe.com/docs/greenlake/services/#generate-an-access-token).



Step #2: Generate Access Token for authenticating to OpsRamp customer integration

Customer require OpsRamp access token for pushing data to OpsRamp end point. Customer has to login to [ OpsRamp ](https://hpepcepoc.app.pov.opsramp.com/setupHome.do)to fetch Access Token.



Setup → Accounts → "Integration and Apps" → Custom → ADD → Install → Install Custom Integration