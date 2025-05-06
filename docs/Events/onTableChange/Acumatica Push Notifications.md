---
title: Acumatica Push Notifications
slug: WjRH-push
createdAt: Wed Apr 02 2025 07:51:38 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 07 2025 09:26:17 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="info"}
The following information applies specifically to Acumatica integration.
:::

## Acumatica

### &#x20;Push Notifications

- In Acumatica, configure *push notification definitions* to send updates to a notification destination (Jigx API endpoint) when specific data changes occur. For more information on setting up push notifications in Acumatica, refer to <a href="https://help.acumatica.com/(W(261))/Wiki/ShowWiki.aspx?pageid=ba35054f-3485-415e-9785-da1195cb708b" target="_blank">Acumatica's Push Notifications</a> documentation.

### Generic Inquiry (GI)

- Create a *Generic Inquiry (GI)*** **in Acumatica with the following three output columns:
  - \_tab = 'Customer'
  - \_del (db deleted)&#x20;
  - \_mod (time)
- Create a *push* using the GI to the Jigx API endpoint.

![Acumatica Generic Inquiries](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-8a0TyTsRhDsD2sWCMnaZq-20250403-190245.png "Acumatica Generic Inquiries")

## Jigx&#x20;

### API Endpoint

:::CodeblockTabs
POST

```none
POST {{baseUrl}}/tool/organizations/:organizationId/solutions/:solutionId/acumatica/cdc?table=<table>
```
:::

### Base URL

Replace \{\{baseUrl}} with the appropriate URL for your region.

| **Region**                  | **URL**                                                                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| US                          | <a href="https://us-east-1.api.jigx.com/v2.0" target="_blank"> https\://us-east-1.api.jigx.com/v2.0</a>          |
| South East (e.g. Australia) | <a href="https://ap-southeast-2.api.jigx.com/v2.0" target="_blank">https\://ap-southeast-2.api.jigx.com/v2.0</a> |
| Europe                      | <a href="https://eu-central-1.api.jigx.com/v2.0" target="_blank">https\://eu-central-1.api.jigx.com/v2.0</a>     |

### Authentication

- A **Personal Access Token (PAT)** is required. Get your PAT from [My Profile]() in Jigx <a href="https://manage.jigx.com" target="_blank">Management</a>.&#x20;
- Enter the PAT as an API key with the prefix BEARER, for example, BEARER XXXXXXXXXX.

### Core elements

| **Element**    | **Description**                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| organizationId | In Jigx Managementunder [Organization details]().                                                                                                       |
| solutionId     | In Jigx Managementunder [Solution Details]().                                                                                                           |
| baseURL        | Refer to the Base URL table above to find the URL for your region.                                                                                      |
| acumatica-cdc  | cdc is a standard term for change data capture.                                                                                                         |
| \<table>       | The table created in Dynamic Data receives data changes pushed from Acumatica, which in turn updates the app. You can name the table whatever you like. |

### Dynamic Data&#x20;

&#x20;The Acumatica *GI* pushes data to the Jigx API endpoint, which then updates the corresponding table in Dynamic Data in <a href="https://docs.jigx.com/_5W2-data" target="_blank">Jigx Management > Solution > Data > \<table>.</a>

![Dynamic Data](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Av2YtmfA_XiXtOkBVQmeh-20250402-091743.png "Dynamic Data")

### Solutions

In the index.jigx file of the Jigx solution in Jigx Builder , configure the [onTableChange](./../onTableChange.md) event. This event allows mobile updates in Jigx by monitoring data changes in the Dynamic Data table.
