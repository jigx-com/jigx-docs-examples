# External push notifications (API)

External push notifications are messages sent from a backend system or third-party service to a mobile application, without any action required from within the app itself. These notifications are essential for delivering timely updates, alerts, and personalized content that enhance user engagement and keep your app connected to external workflows and systems.

When using the Jigx API, external push notifications are triggered through a dedicated **notification endpoint**, which allows for flexible targeting across multiple levels of your app’s user base. The endpoint supports four scopes for delivering messages:

* **USR (Users)** – Target specific individual users.
* **SLN** **(Solution)**– Notify all users within a particular solution.
* **SLN\_GRP (Solution Groups)** – Send messages to predefined groups within a solution.
* **ORG (Organization)** – Broadcast notifications to all users across the entire organization.

This scope-based approach gives you and system integrators fine-grained control over who receives what message, making it easy to tailor communication for different roles, departments, or use cases.

## API Notification Endpoint&#x20;

{% code title="POST" %}
```none
POST {{baseURL}}/tool/organizations/{{orgId}}/notifications
```
{% endcode %}

## Base URL

Replace \{{baseUrl\}} with the appropriate URL for your region.

<table><thead><tr><th width="233.80859375">Region</th><th>URL</th></tr></thead><tbody><tr><td>US</td><td><a href="https://us-east-1.api.jigx.com/v2.0">https://us-east-1.api.jigx.com/v2.0</a></td></tr><tr><td>South East (e.g. Australia)</td><td><a href="https://ap-southeast-2.api.jigx.com/v2.0">https://ap-southeast-2.api.jigx.com/v2.0</a></td></tr><tr><td>Europe</td><td><a href="https://eu-central-1.api.jigx.com/v2.0">https://eu-central-1.api.jigx.com/v2.0</a></td></tr></tbody></table>

## Functional Areas

<table><thead><tr><th width="95.8984375">Area</th><th width="192.15625">URL</th><th>Description</th></tr></thead><tbody><tr><td>tool</td><td>{{baseURL}}/tool</td><td>Endpoint covering: - notifications - members</td></tr></tbody></table>

## Authentication

* A **Personal Access Token (PAT)** is required. Get your PAT from [My profile](https://docs.jigx.com/administration/my-profile#personal-access-tokens-pat) in Jigx Management.
* Enter the PAT as an API key with the prefix BEARER, for example, BEARER XXXXXXXXXX.

## Responses

201 Created 401 Unauthorized

## JSON elements

<table><thead><tr><th width="144.7734375">Element</th><th>Where to find it</th></tr></thead><tbody><tr><td>organizationId</td><td>In Jigx Management under <a href="https://docs.jigx.com/administration/organization-settings">organization settings.</a></td></tr><tr><td>solutionId</td><td>In Jigx Management under <a href="https://docs.jigx.com/administration/solutions/solution-details">solution settings</a></td></tr><tr><td>baseURL</td><td>Refer to the Base URL table above to find the URL for your region.</td></tr><tr><td>scope</td><td>- <strong>USR</strong> – Target specific individual users. <br>- <strong>SLN</strong> – Notify all users within a particular solution. <br>- <strong>SLN_GRP</strong> – Send messages to predefined groups within a solution. <br>- <strong>ORG</strong> – Broadcast notifications to all users across the entire organization.</td></tr><tr><td>jigId</td><td>Target a specific jig with input parameters.When the user taps on the notification (either on the native push notification or the in-app notification), the app will navigate to the specific jig.</td></tr><tr><td>screen</td><td>Default value = "jig"</td></tr><tr><td>title</td><td>Title that shows in the notification message.</td></tr><tr><td>text</td><td>Subtitle text displays under the title in the notification message.</td></tr><tr><td>inputs</td><td>Provide the input parameters to send into the jig specified in the jigId property.</td></tr><tr><td>emails</td><td>Specific the users' email addresses (array) to send the notification to.</td></tr></tbody></table>

## Examples and code snippets

1. [Send notification to users (USR)](<External push notifications _API_/Send notification to users _USR_.md>)
2. [Send notification to all solution users (SLN)](<External push notifications _API_/Send notification to all solution users _SLN_.md>)
3. [Send notification to solution groups (SLN\_GRP)](<External push notifications _API_/Send notification to solution groups _SLN_GRP_.md>)
4. [Send notification to the organization (ORG)](<External push notifications _API_/Send notification to the organization _ORG_.md>)
5. [Target a specific jig with inputs](<External push notifications _API_/Target a specific jig with inputs.md>)
