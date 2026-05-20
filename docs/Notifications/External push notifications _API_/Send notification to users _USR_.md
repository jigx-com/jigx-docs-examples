---
title: Send notification to users (USR)
slug: OVjW-send-notification-to-users-usr
createdAt: Fri Apr 04 2025 11:31:28 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Apr 04 2025 11:32:03 GMT+0000 (Coordinated Universal Time)
---

# Send notification to users (USR)

## Send notification to users (USR)

<mark style="color:green;">`POST`</mark> `{{baseURL}}/tool/organizations/{{orgId}}/notifications`

Target specific users to send a notification to.

**Headers**

<table><thead><tr><th width="302.91796875">Name</th><th>Value</th></tr></thead><tbody><tr><td>Authorization</td><td><p><code>Bearer &#x3C;token></code></p><p>Bearer Token - format:<br>BEARER XXXXXXXXXXXXXX</p></td></tr></tbody></table>

**Body**

Configure the following properties in the JSON body:

<table><thead><tr><th width="163.51953125">Name</th><th width="136.359375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>Title of the notification.</td></tr><tr><td><code>text</code></td><td>string</td><td>Notification message.</td></tr><tr><td><code>scope</code></td><td>string</td><td>"USR" for individual users.</td></tr><tr><td><code>emails</code> </td><td>string</td><td>List users' email addresses using a comma-delimited format for multiple addresses.</td></tr></tbody></table>

{% code title="JSON body" %}
```json
{
  "content": {
    "title": "Approved",
    "text": "Your overtime for this month has been approved",
    "screen":"jig"
    
  },
  "scope": "USR",
  "emails": [
    "username@jigx.com"
  ]
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
    "notificationId": "fdb9af93-100a-4b1b-8135-972bcfe4a5df",
    "scope": "USR",
    "emails": [
        "username@jigx.com"
    ],
    "state": "QUEUED",
    "startAt": "2025-04-04T08:18:54.435Z",
    "content": {
        "text": "Your overtime for this month has been approved",
        "title": "Approved",
        "screen": "jig",
        "inputs": {}
    },
    "createdAt": "2025-04-04T08:18:54.435Z",
    "createdBy": "{{userId}}",
    "updatedAt": "2025-04-04T08:18:54.435Z",
    "updatedBy": "{{userid}}"
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
