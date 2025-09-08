---
title: Send notification to all solution users (SLN)
slug: c6b5-send-notification-to-all-solution-users-sln
createdAt: Fri Apr 04 2025 11:32:25 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Apr 04 2025 11:33:14 GMT+0000 (Coordinated Universal Time)
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

# Send notification to all solution users (SLN)

## Send notification to all solution users (SLN)

<mark style="color:green;">`POST`</mark> `{{baseURL}}/tool/organizations/{{orgId}}/notifications`

Notify all users within a particular solution.

**Headers**

| Name          | Value                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------- |
| Authorization | <p><code>Bearer &#x3C;token></code></p><p>Bearer Token - format:<br>BEARER XXXXXXXXXXXXXX</p> |

**Body**

Configure the following properties in the JSON body:

<table><thead><tr><th width="136.6640625">Name</th><th width="118.67578125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>Title of the notification.</td></tr><tr><td><code>text</code></td><td>string</td><td>Notification message.</td></tr><tr><td><code>scope</code></td><td>string</td><td>"SLN" for users of the solution.</td></tr><tr><td><code>solutionId</code></td><td>string</td><td>"{{solutionId}}", available in Jigx Management> Solution Details.</td></tr></tbody></table>

{% code title="JSON body" %}
```json
{
  "content": {
    "title": "Weekly timesheets",
    "text": "Reminder to log your time for the week",
    "screen":"jig"
  },
  "scope": "SLN",
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
    "notificationId": "85f22fef-1ebc-4dcd-961c-cf8b915c3245",
    "scope": "SLN",
    "solutionId": "{{solutionId}}",
    "state": "QUEUED",
    "startAt": "2025-04-04T09:04:33.446Z",
    "content": {
        "text": "Reminder to log your time for the week",
        "title": "Weekly timesheets",
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
