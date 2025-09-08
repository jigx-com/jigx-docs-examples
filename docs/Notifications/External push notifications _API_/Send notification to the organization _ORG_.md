---
title: Send notification to the organization (ORG)
slug: Sily-send-notification-to-the-organization-org
createdAt: Fri Apr 04 2025 11:32:21 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Apr 04 2025 11:35:21 GMT+0000 (Coordinated Universal Time)
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Send notification to the organization (ORG)

## Send notification to the organization (ORG)

<mark style="color:green;">`POST`</mark> `{{baseURL}}/tool/organizations/{{orgId}}/notifications`

Broadcast notifications to all users across the entire organization.

**Headers**

| Name          | Value                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------- |
| Authorization | <p><code>Bearer &#x3C;token></code></p><p>Bearer Token - format:<br>BEARER XXXXXXXXXXXXXX</p> |

**Body**

Configure the following properties in the JSON body:

<table><thead><tr><th width="168.26953125">Name</th><th width="185.48046875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>Title of the notification.</td></tr><tr><td><code>text</code></td><td>string</td><td>Notification message.</td></tr><tr><td><code>scope</code></td><td>string</td><td>"ORG"</td></tr></tbody></table>

{% code title="JSON body" %}
```json
{
  "content": {
    "title": "Update your app",
    "text": "We released a new version of the app",
    "screen":"jig"
  },
  "scope": "ORG"
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
