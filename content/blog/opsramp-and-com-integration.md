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

**For establishing outbound connection between COM/OpsRamp following steps required.**

Step #1: Generate GLCP Access Token for authenticating to COM webhook

GLCP access token is required for authenticating to COM webhook. Please login to GLCP to fetch [Access Token](https://developer.greenlake.hpe.com/docs/greenlake/services/#generate-an-access-token).

Step #2: Generate Access Token for authenticating to OpsRamp customer integration

Customer require OpsRamp access token for pushing data to OpsRamp end point. Customer has to login to [ OpsRamp ](https://hpepcepoc.app.pov.opsramp.com/setupHome.do)to fetch Access Token.

Setup → Accounts → "Integration and Apps" → Custom → ADD → Install → Install Custom Integration



Step #3: Run POST request on COM webhook to register for events to OpsRamp end point

The  curl request is as follows:

curl -i -X POST \

  https://<COM_URL>/compute-ops-mgmt/v1beta1/webhooks \

\-H 'Authorization: Bearer <COM Access Token>' \

\-H 'Content-Type: application/json' \

\-d '{

    "name": “com_webhook",

    "destination": "https://<OpsRamp_URL/integrations/alertsWebhook/{tenantId}/alerts?vtoken={OpsRamp Access Token}",

    "state": “Enabled”,

    "eventFilter": "type eq '\''compute-ops/server'\''",

    "headers": {

      "Content-Type”: “application/json”,

      "Accept”, “application/json”,

      “Authorization”: “ Bearer <Access Token>”

    }

  }'

Different eventFilters are as follows:

*type eq 'compute-ops/server' or*

*type eq 'compute-ops/job' or*

*type eq 'compute-ops/alert' or*

*type eq 'compute-ops/group' or*

*type eq 'compute-ops/server-setting' or*

*type eq 'compute-ops/group/compliance' or*

*type eq 'compute-ops/firmware-bundle'*



Step #4: Map attributes in OpsRamp for the COM payload



**For establishing inbound connection between COM/OpsRamp following steps are required.**



Step #1: Customers GLCP Client ID and Client Secret for authenticating to COM service

Customer has to login to GLCP to fetch [Client ID and Client Secret ](https://developer.greenlake.hpe.com/docs/greenlake/services/#configuring-api-client-credentials)



Step #2: Customers Access Token for authenticating to OpsRamp customer integration

Customer has to login to [OpsRamp ](https://hpepcepoc.app.pov.opsramp.com/setupHome.do)to fetch Access Token.

Setup → Accounts → "Integration and Apps" → Custom → ADD → Install → Install Custom Integration

Step #3: In OpsRamp provide COM endpoint and Token URL POST 

Here is the snapshot with all details