# Acumatica Push Notifications

:::hint{type="info"}
The following information applies specifically to Acumatica integration.
:::

## Acumatica

### Push Notifications

- In Acumatica, configure *push notification definitions* to send updates to a notification destination (Jigx API endpoint) when specific data changes occur. For more information on setting up push notifications in Acumatica, refer to [Acumatica's Push Notifications](https://help.acumatica.com/\(W\(261\)\)/Wiki/ShowWiki.aspx?pageid=ba35054f-3485-415e-9785-da1195cb708b) documentation.

### Generic Inquiry (GI)

- Create a *Generic Inquiry (GI)* in Acumatica with the following three output columns:
  - \_tab = 'Customer'
  - \_del (db deleted)
  - \_mod (time)
- Create a *push* using the GI to the Jigx API endpoint.

![Acumatica Generic Inquiries](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-8a0TyTsRhDsD2sWCMnaZq-20250403-190245.png "Acumatica Generic Inquiries")

## Jigx

### API Endpoint

:::CodeblockTabs
POST

```none
POST {{baseUrl}}/tool/organizations/:organizationId/solutions/:solutionId/acumatica/cdc?table=<table>
```
:::
### Base URL
Replace \{\{baseUrl}} with the appropriate URL for your region.
<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="237">
  <tr>
    <td selected="false" align="left">
      <p><strong>Region</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>URL</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>US</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://us-east-1.api.jigx.com/v2.0">https://us-east-1.api.jigx.com/v2.0</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>South East (e.g. Australia)</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://ap-southeast-2.api.jigx.com/v2.0">https://ap-southeast-2.api.jigx.com/v2.0</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Europe</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://eu-central-1.api.jigx.com/v2.0">https://eu-central-1.api.jigx.com/v2.0</a></p>
    </td>
  </tr>
</table>

### Authentication

- A **Personal Access Token (PAT)** is required. Get your PAT from [My Profile](https://docs.jigx.com/my-profile#ytp5o) in :Link[Jigx Management]{href="https://manage.jigx.com" newTab="true" hasDisabledNofollow="false"}.
- Enter the PAT as an API key with the prefix BEARER, for example, BEARER XXXXXXXXXX.

### Core elements

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="142">
  <tr>
    <td selected="false" align="left">
      <p><strong>Element</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Description</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>organizationId</p>
    </td>
    <td selected="false" align="left">
      <p>In Jigx Management under </p><div>organization details</div>.<p></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>solutionId</p>
    </td>
    <td selected="false" align="left">
      <p>In Jigx Management under </p><div>Solution Details</div>.<p></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>baseURL</p>
    </td>
    <td selected="false" align="left">
      <p>Refer to the Base URL table above to find the URL for your region.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>acumatica-cdc</p>
    </td>
    <td selected="false" align="left">
      <p>cdc is a standard term for change data capture.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>&#x3C;table></p>
    </td>
    <td selected="false" align="left">
      <p>The table created in Dynamic Data receives data changes pushed from Acumatica, which in turn updates the app. You can name the table whatever you like.</p>
    </td>
  </tr>
</table>

### Dynamic Data

The Acumatica *GI* pushes data to the Jigx API endpoint, which then updates the corresponding table in Dynamic Data in :Link[Jigx Management > Solution > Data >]{href="https://docs.jigx.com/_5W2-data" newTab="true" hasDisabledNofollow="false"}&#x20;

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
    </td>
  </tr>
</table>

![Dynamic Data](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Av2YtmfA_XiXtOkBVQmeh-20250402-091743.png "Dynamic Data")

### Solutions

In the index.jigx file of the Jigx solution in Jigx Builder , configure the [onTableChange](./../onTableChange.md) event. This event allows mobile updates in Jigx by monitoring data changes in the Dynamic Data table.
