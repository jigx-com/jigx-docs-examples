# Notifications

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
You can send Notifications using Jigx Management or programmatically in your solutions, see [Notifications](https://docs.jigx.com/notifications). Notifications can be configured to be sent to a single user, the entire organization, users of a specific solution, and even users of a specific jig in a specific solution.
:::

:::VerticalSplitItem
::Image[]{alt="In-app & push notifications" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7b3RWMHmrLLf2Li44h3sC_jm-notifications.PNG" size="74" caption="In-app & push notifications" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7b3RWMHmrLLf2Li44h3sC_jm-notifications.PNG" width="800" height="787" darkWidth="800" darkHeight="787"}
:::
::::

## Configuration options

| **Core structure** |                                                                                                                                                                                                                                                                        |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| function           | Define a function in the *Functions* folder of your solution. The function has input parameters such as the notification `title`, the notification `text` and requires a Jigx `accessToken` or [personal access token (PAT)](https://docs.jigx.com/my-profile#yepji) . |
| jig                | jigs will invoke the function for sending notifications either via submitting form values to the function or by using an [execute-entity](./Actions/execute-entity.md) action for invoking the function.                                                               |

## Notification URL per region

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="126">
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
      <p><a href="https://us-east-1.api.jigx.com/v2.0/tool/organizations/%7BorganizationId%7D/notifications">https://us-east-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>South East </p>
      <p>(e.g. Australia)</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://ap-southeast-2.api.jigx.com/v2.0/tool/organizations/%7BorganizationId%7D/notifications">https://ap-southeast-2.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Europe</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://eu-central-1.api.jigx.com/v2.0/tool/organizations/%7BorganizationId%7D/notifications">https://eu-central-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications</a></p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::hint{type="info"}
In the code examples below replace `YOUR_ORG_ID` with your actual Organization Id. You can find it in the Organization Settings section of the Jigx Management or use the expression `=@ctx.organization.id`.

Click here to go there directly: [https://manage.jigx.com/settings/org-details](https://manage.jigx.com/organization/org-details)
:::

::::ExpandableHeading
### Notification sent when submitting a form

In this example we are using hidden form components (e.g. `organizationId`) to pass required parameters to the function. The emails field contains a comma-separated list of recipients. You could also use [Expressions](https://docs.jigx.com/expressions) to create that comma-separated string dynamically at runtime.

Once you submitted the form, the recipients should receive both a push notification and an in-app notification. You can also check the delivery status of your notification in the [Notifications](https://docs.jigx.com/notifications) section of the Jigx Management.

Add a function definition called *send-notification.jigx* to the *functions* folder of your solution and copy & paste the following snippet into it. Replace the \{organizationId} in the `url` with your organization's Id.

![Submit form to send notification](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5slfiQWIuZSdPSI5768Ku_notification-submit-form.png "Submit form to send notification")

See the code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-notifications/basic/send-submit-form.jigx).

:::CodeblockTabs
send-notification

```yaml
# Add this file under the functions folder
provider: DATA_PROVIDER_REST
method: POST
url: https://us-east-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications
inputTransform: >-
  $.{
    "content": {
      "title":title,
      "text":text,
      "jigId":jigId,
      "screen":"jig" 
    },
    "scope":scope,
    "emails":emails,
    "description": "description",
    "solutionId": solutionId
  }
parameters:
  solutionId:
   type: string
   location: body
   required: false 
  jigId:
    type: string
    location: body
    required: false
    value: notification-form
  deviceId:
    location: body
    type: string
    required: true
    value: jig
  command:
    location: body
    type: string
    required: false
    value: createNotification
  organizationId:
    location: path
    type: string
    required: true
  scope:
    location: body
    type: string
    required: false
    value: USR
  emails:
    location: body
    type: array
    required: true
  title:
    location: body
    type: string
    required: true
  text:
    location: body
    type: string
    required: true
  accessToken:
    location: header
    type: jigx
    value: jigx
    required: true
  
```

Send-submit-form.jigx

```yaml
title: Send Notification (submit-form)
icon: alert-circle
type: jig.default

actions:
  - children:
      - type: action.submit-form
        options:
          title: Send notification
          formId: send-form
          provider: DATA_PROVIDER_REST
          method: functionCall
          function: send-notification
          entity: send-notification
          onSuccess:
            title: Message sent
                
children:
  - type: component.form
    instanceId: send-form
    options:
      children:
        - type: component.text-field
          instanceId: title
          options:
            label: Title
        - type: component.text-field
          instanceId: text
          options:
            label: Text
        - type: component.text-field
          instanceId: organizationId
          options:
            label: organizationId
            initialValue: =@ctx.organization.id
            isHidden: true
        - type: component.text-field
          instanceId: solutionId
          options:
            label: solutionId
            initialValue: =@ctx.solution.id
            isHidden: true    
        - type: component.text-field
          instanceId: emails
          options:
            label: emails
            initialValue: =@ctx.user.email
            isHidden: true
        - type: component.text-field
          instanceId: accessToken
          options:
            label: accessToken
            initialValue: jigx
            isHidden: true
```
:::
::::

::::ExpandableHeading
### Send notification with execute-entity

You can also send notifications using an [execute-entity](./Actions/execute-entity.md) action if you want to have more control over what's being sent to the function.

In this example we are using state to access the two form fields `title` and `text`. All other function's parameters are set in the execute-entity action. Note that you don't have to use form fields as you could also assign all `parameters` in the action itself.

![Notification sent with execute entity](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2i6PSLJ_8e_lEs6fQxyS5_notification-execute-entity.png "Notification sent with execute entity")

:::CodeblockTabs
send-notification.jigx (function)

```yaml
# Add this file under the functions folder
provider: DATA_PROVIDER_REST
method: POST
url: https://us-east-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications
inputTransform: >-
  $.{
    "content": {
      "title":title,
      "text":text,
      "jigId":jigId,
      "screen":"jig" 
    },
    "scope":scope,
    "emails":emails,
    "description": "description",
    "solutionId": solutionId
  }
parameters:
  solutionId:
   type: string
   location: body
   required: false 
  jigId:
    type: string
    location: body
    required: false
    value: notification-form
  deviceId:
    location: body
    type: string
    required: true
    value: jig
  command:
    location: body
    type: string
    required: false
    value: createNotification
  organizationId:
    location: path
    type: string
    required: true
  scope:
    location: body
    type: string
    required: false
    value: USR
  emails:
    location: body
    type: array
    required: true
  title:
    location: body
    type: string
    required: true
  text:
    location: body
    type: string
    required: true
  accessToken:
    location: header
    type: jigx
    value: jigx
    required: true
    
```

send-execute-entity.jigx

```yaml
title: Send Notification (execute-entity)
icon: alert-circle
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Send now
          provider: DATA_PROVIDER_REST
          method: functionCall
          entity: send-notification
          function: send-notification
          parameters:
            deviceId: jig
            organizationId: =@ctx.organization.id 
            solutionId: =@ctx.solution.id
            emails: =@ctx.user.email
            title: =@ctx.components.title.state.value
            text:  =@ctx.components.text.state.value
            accessToken: jigx
          onSuccess: 
            title: Message sent
                
children:
  - type: component.form
    instanceId: send-form
    options:
      children:
        - type: component.text-field
          instanceId: title
          options:
            label: Title
        - type: component.text-field
          instanceId: text
          options:
            label: Text
```
:::
::::

:::::ExpandableHeading
### Send notification with a target jig with input parameters

You can also target a specific jig with input parameters from your push notification. An example of this would be a notification about a new product promotion with the promotion detail jig as the target. When the user taps on the notification (either on the native push notification or the in-app notification), the app will navigate to the specific promotion

![Target a jig with a notification](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/n8OyVvUVWmJdUI2wsfefh_notification-target-jig.png "Target a jig with a notification")

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{alt="Push Notification" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Sd0XI6wwYa6AQ3W7iKK_k_notifications3iphone13blueportrait.png" size="90" caption="Push Notification" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Sd0XI6wwYa6AQ3W7iKK_k_notifications3iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
::Image[]{alt="Target Jig" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-7AaQQ4OLs957bbfIyQln_notifications4iphone13blueportrait.png" size="90" caption="Target Jig" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-7AaQQ4OLs957bbfIyQln_notifications4iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::
::::

For this, you need an adjusted REST function definition (see 1), a Jig that invokes the REST function (see 2), and a target jig that will be displayed when the user taps on the notification (see 3).

Replace the \{organizationId} in the `url` with your organization's Id.

See the code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/functions/Notifications/send-notification-target-jig.jigx).

:::CodeblockTabs
1-send-notification-target-jig.jigx (function)

```yaml
# Add this file under the functions folder
provider: DATA_PROVIDER_REST
method: POST
url: https://us-east-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications
inputTransform: >
  $.{
      "content": {
        "title": title,
        "text": text, 
        "screen": "jig",
        "jigId": jigId,
        "inputs":{
          "promotionId":promotionId
        }  
    },
      "scope": scope,
      "emails": emails,
      "solutionId": solutionId
  }
parameters:
  deviceId:
    location: body
    type: string
    required: true
    value: jig
  command:
    location: body
    type: string
    required: false
    value: createNotification
  organizationId:
    location: path
    type: string
    required: true
  scope:
    location: body
    type: string
    required: false
    value: USR
  emails:
    location: body
    type: array
    required: true
  title:
    location: body
    type: string
    required: true
  text:
    location: body
    type: string
    required: true
  promotionId:
    location: body
    type: string
    required: true
  solutionId:
    location: body
    type: string
    required: true
  jigId:
    location: body
    type: string
    required: true
  accessToken:
    location: header
    type: jigx
    value: jigx
    required: true
    
```

2-view-promotion-details.jigx (sending jig)

```yaml
title: Send Notification (target jig)
icon: alert-circle
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Send now
          provider: DATA_PROVIDER_REST
          method: functionCall
          entity: send-notification-target-jig
          function: send-notification-target-jig
          parameters:
            deviceId: jig
            organizationId: =@ctx.organization.id 
            emails: =@ctx.user.email
            title: 🎉 New product promotion
            text:  Check it out now
            solutionId: =@ctx.solution.id 
            promotionId: promo12345
            jigId: view-promotion-details
            accessToken: jigx
          onSuccess: 
            title: Message sent
                
children:
  - type: component.form
    instanceId: send-form
    options:
      children:
        - type: component.text-field
          instanceId: title
          options:
            label: Title
        - type: component.text-field
          instanceId: text
          options:
            label: Text
```

3-view-promotion-details.jigx (target jig)

```yaml
title: Promotion Details
icon: zoom-in
type: jig.default

datasources:
  promotions:
    type: datasource.static
    options:
      data:
        - promotionId: promo12345
          name: Stylish Teapot Promo
          price: 25
          image: https://picsum.photos/id/225/500/300
                
children:
  - type: component.image
    options:
      source:
        uri: =@ctx.datasources.promotions[promotionId = @ctx.jig.inputs.promotionId].image
      resizeMode: cover
      height: 300
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Promotion
                  value: =@ctx.datasources.promotions[promotionId = @ctx.jig.inputs.promotionId].name
              - type: component.entity-field
                options:
                  label: Promotion #
                  value: =@ctx.jig.inputs.promotionId
        - type: component.entity-field
          options:
            label: Price
            value: 
              text: =@ctx.datasources.promotions[promotionId = @ctx.jig.inputs.promotionId].price
              format:
                numberStyle: currency
                currency: USD            
```
:::
:::::

:::ExpandableHeading
### Sending push notifications  using the Jigx notification  Endpoint

See [External push notifications (API)](<./Notifications/External push notifications _API_.md>) for more information and examples.
:::

