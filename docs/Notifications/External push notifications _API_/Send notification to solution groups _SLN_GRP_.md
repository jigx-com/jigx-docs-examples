---
title: Send notification to solution groups (SLN_GRP)
slug: v3H4-send-notification-to-solution-groups-slngrp
createdAt: Fri Apr 04 2025 11:32:23 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Apr 04 2025 11:34:50 GMT+0000 (Coordinated Universal Time)
---

# Send notification to solution groups (SLN\_GRP)

## Send notification to solution groups (SLN\_GRP)

<mark style="color:green;">`POST`</mark> `{{baseURL}}/tool/organizations/{{orgId}}/notifications`

Send messages to predefined groups within a solution.&#x20;

**Headers**

| Name          | Value                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------- |
| Authorization | <p><code>Bearer &#x3C;token></code></p><p>Bearer Token - format:<br>BEARER XXXXXXXXXXXXXX</p> |

**Body**

Configure the following properties in the JSON body:

<table><thead><tr><th width="144.2109375">Name</th><th width="118.19140625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>Title of the notification.</td></tr><tr><td><code>text</code></td><td>string</td><td>Notification message.</td></tr><tr><td><code>scope</code></td><td>string</td><td>"SLN_GRP" -groups: list solution groups using a comma-delimited format for multiple groups. Solution groups defined in Jigx Management> Solution > Groups</td></tr><tr><td><code>solutionId</code></td><td>string</td><td>"{{solutionId}}", available in Jigx Management> Solution Details</td></tr></tbody></table>

{% code title="JSON body" %}
```json
{
  "content": {
    "title": "Sales target",
    "text": "This quarter's sale target has been reached",
    "screen":"jig"
  },
  "scope": "SLN_GRP",
  "groups": [
    "sales","finance"
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
  "id": 1,
{
    "organizationId": "{{orgId}}",
    "region": "us-east-1",
    "notificationId": "85f22fef-1ebc-4dcd-961c-cf8b915c3245",
    "scope": "SLN_GRP",
    "solutionId": "{{solutionId}}",
    "state": "QUEUED",
    "startAt": "2025-04-04T09:04:33.446Z",
    "content": {
        "title": "Sales target",
        "text": "This quarter's sale target has been reached",
        "screen": "jig",
        "inputs": {}
    },
    "createdAt": "2025-04-04T09:04:33.446Z",
    "createdBy": "{{userId}}",
    "updatedAt": "2025-04-04T09:04:33.446Z",
    "updatedBy": "{{userid}}"
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
