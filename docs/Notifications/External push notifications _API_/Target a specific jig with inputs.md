---
title: Target a specific jig with inputs
slug: f4Ei-target-a-specific-jig-with-inputs
createdAt: Fri Apr 04 2025 11:35:22 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu May 01 2025 08:11:49 GMT+0000 (Coordinated Universal Time)
---

# Target a specific jig with inputs

## Target a specific jig with inputs

<mark style="color:green;">`POST`</mark> `{{baseURL}}/tool/organizations/{{orgId}}/notifications`

\<Description of the endpoint>

**Headers**

| Name          | Value                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------- |
| Authorization | <p><code>Bearer &#x3C;token></code></p><p>Bearer Token - format:<br>BEARER XXXXXXXXXXXXXX</p> |

**Body**

Configure the following properties in the JSON body:

<table><thead><tr><th width="141.86328125">Name</th><th width="153.484375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>Title of the notification.</td></tr><tr><td><code>text</code></td><td>string</td><td>Notification message.</td></tr><tr><td><code>jigId</code></td><td>string</td><td>Provide the jigId of the jig you want to open when the notification is tapped</td></tr><tr><td><code>inputs</code></td><td>string</td><td>Define the values for the jig inputs</td></tr><tr><td><code>scope</code></td><td>string</td><td>Can use any of the scopes USR, ORG, SLN, or SLN_GRP</td></tr><tr><td><code>solutionId</code></td><td>string</td><td>"{{solutionId}}", available in Jigx Management> Solution Details</td></tr></tbody></table>

{% code title="JSON body" %}
```json
/{
  "content": {
    "title": "🎉 New product promotion",
    "text": "Check it out now",
    "jigId": "view-promotion-details",
    "screen":"jig",
    "inputs": {
      "promo-code": "x-3654",
      "name": "20% on all Winter stock",
      "price": 34
    }
  },
  "scope": "SLN_GRP",
  "groups": [
    "customers"
  ],
  "solutionId": "{{solutionId}}"
}
```
{% endcode %}

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "organizationId": "{{orgId}}",
    "region": "us-east-1",
    "notificationId": "02817dcd-175c-4d0f-8c47-f1838c8e628c",
    "scope": "ORG",
    "state": "QUEUED",
    "startAt": "2025-04-04T10:06:50.444Z",
    "content": {
        "text": "We released a new version of the app",
        "title": "Update your app",
        "screen": "jig",
        "inputs": {}
    },
    "createdAt": "2025-04-04T10:06:50.444Z",
    "createdBy": "{{userId}}",
    "updatedAt": "2025-04-04T10:06:50.444Z",
    "updatedBy": "{{userId}}"
}

```
{% endtab %}

{% tab title="400" %}
```json
{
    "message": "Unauthorized"
}
```
{% endtab %}
{% endtabs %}
