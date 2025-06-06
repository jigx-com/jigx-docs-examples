# External push notifications (API)

External push notifications are messages sent from a backend system or third-party service to a mobile application, without any action required from within the app itself. These notifications are essential for delivering timely updates, alerts, and personalized content that enhance user engagement and keep your app connected to external workflows and systems.

When using the Jigx API, external push notifications are triggered through a dedicated **notification endpoint**, which allows for flexible targeting across multiple levels of your app’s user base. The endpoint supports four scopes for delivering messages:

- **USR (Users)** – Target specific individual users.
- **SLN** **(Solution)**– Notify all users within a particular solution.
- **SLN\_GRP (Solution Groups)** – Send messages to predefined groups within a solution.
- **ORG (Organization)** – Broadcast notifications to all users across the entire organization.

This scope-based approach gives you and system integrators fine-grained control over who receives what message, making it easy to tailor communication for different roles, departments, or use cases.

## API Notification Endpoint

:::CodeblockTabs
POST

```none
POST {{baseURL}}/tool/organizations/{{orgId}}/notifications
```
:::

### Base URL

Replace \{\{baseUrl}} with the appropriate URL for your region.

| **Region**                  | **URL**                                                                                                                                                                                               |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| US                          | <a href="https://us-east-1.api.jigx.com/v2.0" target="_blank">https\://us-east-1.api.jigx.com/v2.0</a> [https://us-east-1.api.jigx.com/v2.0](https://us-east-1.api.jigx.com/v2.0)                     |
| South East (e.g. Australia) | <a href="https://ap-southeast-2.api.jigx.com/v2.0" target="_blank">https\://ap-southeast-2.api.jigx.com/v2.0</a>[https://ap-southeast-2.api.jigx.com/v2.0](https://ap-southeast-2.api.jigx.com/v2.0)  |
| Europe                      | <a href="https://eu-central-1.api.jigx.com/v2.0" target="_blank">https\://eu-central-1.api.jigx.com/v2.0</a>[https://eu-central-1.api.jigx.com/v2.0](https://eu-central-1.api.jigx.com/v2.0)          |

## Functional Areas

| **Area** | **URL**            | **Description**                                      |
| -------- | ------------------ | ---------------------------------------------------- |
| tool     | \{\{baseURL}}/tool | Endpoint covering:&#xA;- notifications&#xA;- members |

## Authentication

- A **Personal Access Token (PAT)** is required. Get your PAT from [My profile](docId\:PCpYqHu9kr0rFKl8V-kTw) in Jigx <a href="https://manage.jigx.com" target="_blank">Management</a>.
- Enter the PAT as an API key with the prefix BEARER, for example, BEARER XXXXXXXXXX.

## Responses

201 Created
401 Unauthorized

## JSON elements

| **Element**    | **Where to find it**                                                                                                                                                                                                                                                         |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| organizationId | In Jigx Management under [Organization details](#).                                                                                                                                                                                                                          |
| solutionId     | In Jigx Management under [Solution Details](#).                                                                                                                                                                                                                              |
| baseURL        | Refer to the Base URL table above to find the URL for your region.                                                                                                                                                                                                           |
| scope          | - **USR** – Target specific individual users.&#xA;- **SLN** – Notify all users within a particular solution.&#xA;- **SLN\_GRP** – Send messages to predefined groups within a solution.&#xA;- **ORG** – Broadcast notifications to all users across the entire organization. |
| jigId          | Target a specific jig with input parameters.When the user taps on the notification (either on the native push notification or the in-app notification), the app will navigate to the specific jig.                                                                           |
| screen         | Default value = "jig"                                                                                                                                                                                                                                                        |
| title          | Title that shows in the notification message.                                                                                                                                                                                                                                |
| text           | Subtitle text displays under the title in the notification message.                                                                                                                                                                                                          |
| inputs         | Provide the input parameters to send into the jig specified in the jigId property.                                                                                                                                                                                           |
| emails         | Specific the users' email addresses (array) to send the notification to.                                                                                                                                                                                                     |

## Examples and code snippets

1. [Send notification to users (USR)](<./External push notifications _API_/Send notification to users _USR_.md>)
2. [Send notification to all solution users (SLN)](<./External push notifications _API_/Send notification to all solution users _SLN_.md>)
3. [Send notification to solution groups (SLN\_GRP)](<./External push notifications _API_/Send notification to solution groups _SLN_GRP_.md>)
4. [Send notification to the organization (ORG)](<./External push notifications _API_/Send notification to the organization _ORG_.md>)
5. [Target a specific jig with inputs](<./External push notifications _API_/Target a specific jig with inputs.md>)

