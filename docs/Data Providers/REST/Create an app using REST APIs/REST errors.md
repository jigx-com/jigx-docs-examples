# REST errors

## Scenario

{% columns %}
{% column %}
When trying to view a customer and their details or create a new customer in the app, the app can fail to retrieve or create the required data, and various errors are returned. In this example, we add error handling to the REST endpoint functions to cater for the following errors:

* 401 Unauthorized
* 403 Forbidden
* Unexpected error
{% endcolumn %}

{% column %}
<figure><img src="../../../../.gitbook/assets/REST- errorCenter.gif" alt="REST Error handling" width="188"><figcaption><p>Error REST handling</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## How does this work

An `error` section is added to the REST endpoint functions for creating customers (POST), viewing customers (GET), and updating customers (PUT). In this section, the `when` property is configured with an expression that returns the response status from the endpoint, for example, `=@ctx.response.status = 403`. There are multiple `when` properties configured to catch a 401 and 403 error; all other response statuses are caught in the Unexpected error. Each `when` property has:

* An `alert` notification message configured which is displayed either as a `toast` or `modal` to the user in the app.
* An `operation`  which writes the details to the customers\_error `table` for logging and debugging purposes, which provides an explanation of the error.  The data written to the table is configured in the `records` property. The `table` in conjunction with the `commandQueue` is used to troubleshoot the error and create jigs that allows you to retry the REST call or delete the error from the `commandQueue`. See [REST error handling](<REST errors.md>) for more information.

### Consideration

* Use `groupId` to manage multiple alerts for the same issue. When using `modal` presentation, alerts with the same `groupId` are grouped so that only the first alert appears and subsequent ones are automatically skipped. When using `toast` presentation, alerts are also grouped, preventing duplicates. Users can tap the `toast` to view details, if multiple alerts exist, they stack and display a count at the top. Swiping left lets users view each alert’s details within the stack.&#x20;
* When configuring error handling with alerts, ensure that HTTP 200 (success) responses are excluded. If not, the app may treat successful responses as errors, preventing data from loading.&#x20;

## REST API

<table><thead><tr><th width="216.125">REST</th><th>Detail</th></tr></thead><tbody><tr><td>URL</td><td>https://[your_rest_service]/api/customers</td></tr><tr><td>Operation/Method</td><td>POST,GET,PUT</td></tr></tbody></table>

## Function

In each of the REST function files (GET, POST, PUT), add an `error` section with `alerts` and configure the YAML to cater for a 401 and 403 error, and a section to cater for all other response errors.

{% tabs %}
{% tab title="rest-create-customer.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
# Create new record in the backend
method: POST 
# Use your REST service URL 
url: https://[your_rest_service]/api/customers 
# Direct the function call to use local execution,
# between the mobile device and the REST service.
useLocalCall: true 

parameters:
  x-functions-key:
    location: header
    required: false
    type: string
    # Use manage.jigx.com to define credentials for your solution.
    value: service.oauth 
  firstName:
    type: string
    location: body
    required: true
  lastName:
    type: string
    location: body
    required: true
  companyName:
    type: string
    location: body
    required: true
  address:
    type: string
    location: body
    required: false
  city:
    type: string
    location: body
    required: false
  state:
    type: string
    location: body
    required: false
  zip:
    type: string
    location: body
    required: false
  phone1:
    type: string
    location: body
    required: false
  phone2:
    type: string
    location: body
    required: false
  email:
    type: string
    location: body
    required: false
  web:
    type: string
    location: body
    required: false
  region:
    type: string
    location: body
    required: false
  customerType:
    type: string
    location: body
    required: false
  jobTitle:
    type: string
    location: body
    required: false

inputTransform: |
  {
    "firstName": firstName,
    "lastName": lastName,
    "companyName": companyName,
    "address": address,
    "city": city,
    "state": state, 
    "zip": zip,
    "phone1": phone1,
    "phone2": phone2,
    "email": email,
    "web": web,
    "region": region,
    "customerType": customerType,
    "jobTitle": jobTitle
  }

outputTransform: |
  {
    "id": custId,
    "status": status
  }

# Configure multiple REST error responses.
error:
  # Error handling with Alert 401.
  - when: =@ctx.response.status = 401
    # Enable notification to alert the user.
    notification: true
    # Configure the alert modal that appears to the user.
    alert:
      # Main heading displayed to the user.
      title: Insufficient Permissions
      # Detailed user-friendly explanation of the error and next steps.
      description: You don’t have permission to Add customers.
        Please contact support to assign you the correct permissions.
      # Dynamic subtitle showing the actual HTTP status text and code.
      subtitle: =('Error:' & ' ' & @ctx.response.statusText & ' (' &
        @ctx.response.status & ')')
      # Icon to visually represent the error state.
      icon: lock-2
      style:
        isNegative: true
      presentAs: modal
    # Operations to execute when this error occurs.
    operations:
      # Log the error to a database table for tracking and debugging.
      - type: operation.upsert-merge
        # Dynamic table name based on the entity (e.g., "customers_error").
        table: =@ctx.entity & "_error"
        # Error record containing all relevant context information.
        records: '={ "id": @ctx.commandId, "type": "Unauthorized",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user,
          "solution": @ctx.solution.name, "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
        # Timestamp when the error was logged.
        timestamp: =$now()

  # Error handling with Alert 403
  - when: =@ctx.response.status = 403
    notification: true
    alert:
      title: System Offline
      description: Our system is temporarily unavailable.
        Please try again in a few minutes. Thank you
        for your patience!
      subtitle: =@ctx.response.body
      icon: server-error-403-hand-forbidden
      style:
        isWarning: true
      presentAs: modal
      # Modal can be dismissed.
      dismiss:
        isEnabled: true
      # Configure an action to retry the POST or cancel and go back to the form.
      actions:
        - type: action.retry-queue-command
          options:
            id: =@ctx.commandId
            title: Retry Now
            style:
              isPrimary: true
        - type: action.go-to
          options:
            title: Cancel
            linkTo: new-customer-hr1
    # Log the error to a database table for tracking and debugging.
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.commandId, "type": "system-offline",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user,
          "solution": @ctx.solution.name, "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
        timestamp: =$now()
    # Error handling with Alert for all non-success responses.
    # Exclude the 200 (successful) response; otherwise, no data will load in the app.
    # A 200 status is considered a valid response and should not trigger an error alert.
    # Without this exclusion, it would be treated as an error, preventing data from loading.
  - when: =@ctx.response.status != 403 or @ctx.response.status != 401 or @ctx.response.status != 200
    notification: true
    alert:
      title: Unexpected error
      description: An unexpected error occurred. Please try again.
      subtitle: =@ctx.response.body
      icon: on-error-1
      presentAs: toast
      group:
        id: unexpectedErrors
      # Configure an action to retry the POST or cancel and go back to the form.
      actions:
        - type: action.retry-queue-command
          options:
            id: =@ctx.commandId
            title: Retry again
            style:
              isPrimary: true
        - type: action.go-to
          options:
            title: Cancel
            linkTo: new-customer-hr1
    # Log the error to a database table for tracking and debugging.
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.commandId, "type": "unexpected-error",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user,
          "solution": @ctx.solution.name, "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
```
{% endtab %}

{% tab title="rest-get-customers.jigx" %}
```python
provider: DATA_PROVIDER_REST
# Returns records from the backend
method: GET
url: https://[your_rest_service]/api/customers 
forRowsWithMatchingIds: true
# Direct the function call to use local execution,
# between the mobile device and the REST service.
useLocalCall: true

parameters:
  x-functions-key:
    location: header
    required: false
    type: string
    # Use manage.jigx.com to define credentials for your solution.    
    value: XXX
  syncId:
    type: number
    location: header
    required: false
    value: =$toMillis($now()) % 86400000

outputTransform: |
    $.customers.{
        "id": custId,
        "firstName": firstName,
        "lastName": lastName,
        "companyName": companyName,
        "address": addresses[0].address,
        "city": addresses[0].city,
        "state": addresses[0].state,
        "zip": addresses[0].zip,
        "phone1": phones[0].mobile,
        "phone2": phones[0].office,
        "email": email,
        "web": web,
        "region": region,
        "customerType": customerType,
        "jobTitle": jobTitle,
        "logo": logo
      }
      
conversions:
  - property: logo
    from: base64
    to: local-uri
    
# Configure multiple REST error responses.
error:
  # Error handling with Alert 403.
  - when: =@ctx.response.status = 403
    # Enable notification system to alert the user.
    notification: true
    # Configure the alert modal that appears to the user.
    alert:
      # Main heading displayed to the user.
      title: Error syncing customer list
      # Detailed user-friendly explanation of the error and next step
      description:
        Error syncing customers, our system is temporarily unavailable.
        Please try again.
      presentAs: modal
      # Dynamic details showing technical details, the actual HTTP status and body.
      details:
        Technical-info: =@ctx.response.body
        Status: =@ctx.response.status
      # Icon to visually represent the error state.
      icon: synchronize-arrows-1
      style:
        isWarning: true
      # Group to avoid multiple alerts for same issue, using the toast presentation groups the same error messages.
      # Tap the alert to see details. If multiple alerts, they stack and the number is shown at the top.
      # Swipe right to view each error details in the stack
      group:
        id: sync-error
      # Configure an action to retry the GET or cancel and go back to the list or form.
      actions:
        - type: action.execute-action
          options:
            title: Load Customers
            action: load-data
        - type: action.go-to
          options:
            title: Cancel
            linkTo: new-customer-hr1
      # Operations to execute when this error occurs.
    operations:
      # Log the error to a database table for tracking and debugging.
      # Static table name based on the entity (e.g., "customers_error").
      - table: =@ctx.entity & "_error"
        type: operation.upsert-merge
        # Error record containing all relevant context informatio
        records: '={ "id": @ctx.parameters.syncId, "type": "Sync-data",
          "response": @ctx.response,
          "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-customers"}'
        # Timestamp when the error was logged.
        timestamp: =$now()
  # Error handling with Alert 401.
  - when: =@ctx.response.status = 401
    notification: true
    alert:
      title: Access Denied
      description: "You don’t have permission to see the customer list. Contact support."
      details:
        Technical-info: =@ctx.response.body
        status: =@ctx.response.status
      icon: breached-password-authentication-lock-warning
      presentAs: modal
      style:
        isNegative: true
      # Configure a share action to email support and get the right permissions.
      actions:
        - type: action.share
          options:
            title: Email Support
            email: companysupport.com
            subject: Access Denied Error - Help Needed
            message: "Hi Support Team,
              I'm experiencing an 'Access Denied' error when trying to view customer data. Could you please assist me."
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.parameters.syncId, "type": "Unauthorized",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-customers"}'
        timestamp: =$now()
   # Error handling with Alert for all other errors.
  - when: =@ctx.response.status != 403 or @ctx.response.status != 401 or @ctx.response.status != 200
    notification: true
    alert:
      title: Oops! Something Went Wrong
      description: "An unexpected error occurred. Please
        try again. If the problem persists, reach out to support."
      icon: on-error-sad
      presentAs: toast
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.parameters.syncId, "type": "unexpected-error",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-customers"}'
        timestamp: =$now()
```
{% endtab %}

{% tab title="rest-update-customer.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
# Update the customer data
method: PUT
# Use your REST service URL 
url: https://[your_rest_service]/api/customers 
# Direct the function call to use local execution,
# between the mobile device and the REST service.
useLocalCall: true
format: text

parameters:
  x-functions-key:
      location: header
      required: false
      type: string
      # Use manage.jigx.com to define credentials for your solution.      
      value: XXXX
  id:
    type: int
    location: body
    required: true
  firstName:
    type: string
    location: body
    required: true
  lastName:
    type: string
    location: body
    required: true
  companyName:
    type: string
    location: body
    required: true
  address:
    type: string
    location: body
    required: false
  city:
    type: string
    location: body
    required: false
  state:
    type: string
    location: body
    required: false
  zip:
    type: string
    location: body
    required: false
  phone1:
    type: string
    location: body
    required: false
  phone2:
    type: string
    location: body
    required: false
  email:
    type: string
    location: body
    required: false
  web:
    type: string
    location: body
    required: false
  region:
    type: string
    location: body
    required: false
  customerType:
    type: string
    location: body
    required: false
  jobTitle:
    type: string
    location: body
    required: false
   
inputTransform: |
  {
    "custId": id,
    "firstName": firstName,
    "lastName": lastName,
    "companyName": companyName,
    "address": address,
    "city": city,
    "state": state, 
    "zip": zip,
    "phone1": phone1,
    "phone2": phone2,
    "email": email,
    "web": web,
    "region": region,
    "customerType": customerType,
    "jobTitle": jobTitle
  }
  
# Configure multiple REST error responses.
error:
  # Error handling with Alert 401.
  - when: =@ctx.response.status = 401
    # Enable notification system to alert the user
    notification: true
    # Configure the alert modal that appears to the user.
    alert:
      # Main heading displayed to the user.
      title: Insufficient Permissions
      # Detailed user-friendly explanation of the error and next steps.
      description: You don’t have permission to Update customers.
        Please contact support to assign you the correct permissions.
      # Dynamic subtitle showing the actual HTTP status text and code.
      subtitle: =('Error:' & ' ' & @ctx.response.statusText & ' (' &
        @ctx.response.status & ')')
      # Icon to visually represent the error state.
      icon: lock-2
      style:
        isNegative: true
      presentAs: modal
      # Configure an action to retry the Put or cancel and go back to the form
      actions:
        - type: action.retry-queue-command
          options:
            id: =@ctx.commandId
            title: Retry Now
            style:
              isPrimary: true
        - type: action.go-back
          options:
            title: Cancel
            style:
              isSecondary: true
    # Operations to execute when this error occurs.
    operations:
      # Log the error to a database table for tracking and debugging
      - type: operation.upsert-merge
        # Dynamic table name based on the entity (e.g., "customers_error").
        table: =@ctx.entity & "_error"
        # Error record containing all relevant context information.
        records: '={ "id": @ctx.commandId, "type": "Unauthorized",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-update-customer"}'
        # Timestamp when the error was logged.
        timestamp: =$now()

  # Error handling with Alert 403
  - when: =@ctx.response.status = 403
    notification: true
    alert:
      title: System Offline
      description: Our system is temporarily unavailable.
        Please try again in a few minutes. Thank you
        for your patience!
      subtitle: =@ctx.response.body
      icon: server-error-403-hand-forbidden
      style:
        isWarning: true
      presentAs: modal
      # Modal will auto dismiss after 3 seconds.
      dismiss:
        autoAfter: 3
        isEnabled: true
    # Operations to log the error in a table
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.commandId, "type": "system-offline",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-update-customer"}'
        timestamp: =$now()
    # Error handling with Alert for all other errors.
  - when: =@ctx.response.status != 403 or @ctx.response.status != 401 or @ctx.response.status != 200
    notification: true
    alert:
      title: Unexpected error
      description: An unexpected error occurred. Please try again.
      subtitle: =@ctx.response.body
      icon: on-error-1
      presentAs: modal
      # Group to avoid multiple alerts for same issue, using the modal presentation groups the same error messages.
      # Only the first alert appears, and the rest are automatically skipped.
      group:
        id: unexpectedErrors
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: '={ "id": @ctx.commandId, "type": "unexpected-error",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "get-update-customer"}'

```
{% endtab %}

{% tab title="rest-upload-customer-images.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
method: POST
url: https://[your_rest_service]/api/images
useLocalCall: true

parameters:
  x-functions-key:
    location: header
    required: false
    type: string
    # Use manage.jigx.com to define credentials for your solution.      
      value: XXXX
  custId:
    type: string
    location: body
    required: false
  createdBy:
    type: string
    location: body
    required: false
  description:
    type: string
    location: body
    required: false
  createdDate:
    type: string
    location: body
    required: false
    value: =$now()
  image:
    type: image
    location: body
    required: false

inputTransform: |
  {
    "custId": custId,
    "createdBy": createdBy,
    "description": description,
    "createdDate": createdDate,
    "image": image
  }

outputTransform: |
  $.{
      "id": image_id
    }

conversions:
  - property: image
    from: local-uri
    to: base64
    convertHeicToJpg: true

# Error handling with Alert 401
error:
  - when: =@ctx.response.status = 401
    notification: true
    alert:
      title: Insufficient Permission
      description: "You don’t have permission to upload images. Contact support."
      subtitle: =('Error:' & ' ' & @ctx.response.statusText & ' (' &
        @ctx.response.status & ')')
      icon: on-error-sad
      style:
        isNegative: true
      presentAs: modal

    # Operations to log the error in a local table.
    operations:
      - type: operation.upsert-merge
        table: customers_error
        records:
          '={ "id": @ctx.commandId, "type": "Unauthorized-image-upload",  "response": @ctx.response,
          "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "upload-customer-images"}'
        timestamp: =$now()

  # Error handling with Alert 403
  - when: =@ctx.response.status = 403
    notification: true
    alert:
      title: System Offline
      description: Our system is temporarily unavailable.
        Please try again in a few minutes. Thank you for your patience!
      subtitle: =@ctx.response.body
      icon: server-error-403-hand-forbidden
      style:
        isWarning: true
      presentAs: modal
      dismiss:
        autoAfter: 3
        isEnabled: true
      # Configure an action to retry the GET or cancel and go back to the list or form
      actions:
        - type: action.retry-queue-command
          options:
            id: =@ctx.commandId
            title: Retry Now
            style:
              isPrimary: true
        - type: action.go-to
          options:
            title: Cancel
            linkTo: add-customer-images

    # Operations to log the error in a local table
    operations:
      - type: operation.upsert-merge
        table: customers_error
        records: '={ "id": @ctx.commandId, "type": "System-offline",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "upload-customer-images"}'
        timestamp: =$now()

    # All other errors
  - when: =@ctx.response.status != 403 or @ctx.response.status != 401 or @ctx.response.status != 200
    notification: true
    alert:
      title: Oops! Something Went Wrong
      description: An unexpected error occurred. Please try again.
      subtitle: =@ctx.response.body
      icon: on-error-1
      presentAs: modal
      group:
        id: unexpectedErrors
      # Configure an action to retry the GET or cancel and go back to the list or form
      actions:
        - type: action.retry-queue-command
          options:
            id: =@ctx.commandId
            title: Retry Now
            style:
              isPrimary: true
        - type: action.go-to
          options:
            title: Cancel
            linkTo: add-customer-images
    # Operations to log the error in a local table
    operations:
      - type: operation.upsert-merge
        table: customers_error
        records:
          '={ "id": @ctx.commandId, "type": "unexpected-error-image-upload",
          "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution.name,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId, "function": "upload-customer-images"}'

```
{% endtab %}
{% endtabs %}

## Datasources

Add a file under the datasource folder to configure the local data provider with the data returned from the customers\_error table. This data is used to provide detail of the error in a jig and to configure actions allowing the item to be retried or deleted.

{% code title="customer-errors.jigx" %}
```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_LOCAL
# Configure the datasource for the customer_error table
  entities:
    - entity: customers_error
# Return the details that you specified in the function transform property 
  query: 
    SELECT 
      id,
      json_extract(data, '$.response.ok') as ok, 
      json_extract(data, '$.response.status') as status, 
      json_extract(data, '$.response.statusText') as statusText, 
      json_extract(data, '$.response.headers') as headers, 
      json_extract(data, '$.response.body') as body,
      json_extract(data, '$.type') as type
    FROM 
      [customers_error]
```
{% endcode %}

## Error Center - Jigs (screens)

{% columns %}
{% column %}
There are a number of options available to process items that are in an error state.

1. Use the **commandQueue**. Items that return an error from the REST endpoint will remain on the commandQueue and are not automatically processed by the queue. You must configure an action to either retry the item or delete the item from the queue. The retry executes the REST call again.
2. Use the _**customers\_error**_ table configured in the function. Use the data from the table in a jig to allow app users to resolve the error or delete the item in error.
3. Add a `banner` component to the home screen with a `when` condition that displays when errors exist in the `customers_error` table. Add an action to `go-to` the issues (error center) list.
{% endcolumn %}

{% column %}
<figure><img src="../../../../.gitbook/assets/REST- errorCenter.gif" alt="Error center" width="188"><figcaption><p>Error Center</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

### Add a banner to the customer list

Add a `banner` component with a `when` condition that displays when errors exist in the `customers_error` table. Use an expression with _$count_ in the banner `title` to show the number of errors. Include a `go-to` action that navigates to the list of issues and errors. Configure the list to display the error `type`, `statusText`, and `status`.

Enable **Retry** and **Delete** swipe actions. When deleting an error, ensure the delete action removes the record from both the `commandQueue` and the `customers_error` table.

{% code title="home.jigx" %}
```yaml
title: Global Inc
type: jig.default

children:
  # Error Banner - only shows when errors exist in the queue
  - type: component.banner
    # Use 'when' to conditionally display banner only when errors exist
    when: =$count(@ctx.datasources.customers-errors) != 0
    options:
      title:
        # Expression to show the number of current errors.
        text: ="Errors " & ($count(@ctx.datasources.customers-errors.id))
        fontSize: medium
        isBold: true
        color: negative
      subtitle:
        text: Errors detected, review and resolve issues.
        fontSize: regular
      leftElement:
        element: icon
        icon: on-error-1
        type: contained
        shape: circle
        color: negative
      style:
        isNegative: true
      actions:
        - type: action.action-list
          options:
            title: See All
            actions:
              - type: action.go-to
                options:
                  linkTo: customer-errors
  - type: component.grid
    options:
      children:
        - type: component.grid-item
          options:
            size: "2x2"
            children:
              type: component.jig-widget
              options:
                jigId: list-customers-hr1
        - type: component.grid-item
          options:
            size: "2x2"
            children:
              type: component.jig-widget
              options:
                jigId: list-customers-hr2
        - type: component.grid-item
          options:
            size: "2x2"
            children:
              type: component.jig-widget
              options:
                jigId: list-customers-hr3

```
{% endcode %}

### Use the commandQueue

Create a jig to work with the items in the [commandQueue](<REST errors.md>). This is helpful for the solution owner or administrator to take action and `delete` errors in the queue or possibly `retry` the REST call to process the items in the queue that are in an error state. Configure a list jig containing all items in the commandQueue, add a left `swipeable` action to cater for the delete and retry actions.

{% tabs %}
{% tab title="list-command-queue.jigx" %}
```yaml
title: CommandQ
description: List of commands in the queue
type: jig.list
icon: command-button-keyboard

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg
# Configure a datasource to return the data available in the system table.
datasources:
  queued-commands:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _commandQueue
      query: |
        SELECT
          id, queue, type, payload, state, error
        FROM [_commandQueue]
        ORDER BY id;
      jsonProperties:
        - payload
# Create a list of the items on the queue.
data: =@ctx.datasources.queued-commands
item:
  type: component.list-item
  options:
    title: =(@ctx.current.item.payload.functionId = 'rest-create-customer' ? 'Create Customer Failed':@ctx.current.item.id & " - " & @ctx.current.item.queue & " - " & @ctx.current.item.type & " - " & @ctx.current.item.state)
    subtitle: =@ctx.current.item.payload.data.companyName & ' could not be created'
    description: =@ctx.current.item.payload.data.internalRef
    # Configure an onPress to view all the details of the individual item
    # in a separate jig.    
    onPress:
      type: action.go-to
      options:
        linkTo: item
        inputs:
          commandId: =@.current.item.id
          internalRef: =@ctx.current.item.payload.data.internalRef
    # Add two actions for the items, a retry and a delete.          
    swipeable:
      left:
        - icon: close
          label: Delete
          color: negative
          onPress:
            type: action.delete-queue-command
            options:
              id: =@.current.item.id
        - icon: button-refresh-arrow
          label: Retry
          onPress:
            type: action.retry-queue-command
            options:
              id: =@.current.item.id
```
{% endtab %}
{% endtabs %}

### Use the customers\_error table

Create a list jig to list the records in the `customers_error` table.&#x20;

* Provide detail of the error in the `title` and `subtitle` properties.
* Add a swipeable event and configure a `retry-queue-command` action, and two execute-entity actions to delete the records from the `commandQueue` and the `customers_error` tables.
* Similarly, add actions to the list that retry or delete all errors in the list. The execute-entities action is used with specific expressions that include multiple records:
  * `=@ctx.datasources.command-queue.id` - retries multiple items in the `CommandQueue` at the same time. &#x20;
  * `=@ctx.datasources.customers-errors.{"id":id}[]` - deletes all records in the `customers_error` table.

{% tabs %}
{% tab title="customer-errors.jigx" %}
```yaml
title: Issues
description: A list of errors that failed to be created successfully and need manual intervention for resolution.
type: jig.list
icon: on-error-1

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/vurcs49k07rna87zuhdsc/customer_issues.png?rlkey=b23lhiqprqie55v2x99u2otyy&st=upbpp2hk&raw=1

data: =@ctx.datasources.customers-errors
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.type
    subtitle: =@ctx.current.item.statusText & ' - ' & @ctx.current.item.status
    leftElement:
      element: icon
      icon: =(@ctx.current.item.status = 401 ? 'lock-1':@ctx.current.item.status = 403 ? 'server-error-403-hand-forbidden':'on-error-1')
      color: negative
    rightElement:
      element: icon
      icon: arrow-left-diagram
    swipeable:
      left:
        - label: Retry
          icon: synchronize-arrow
          color: primary
          onPress:
            type: action.retry-queue-command
            options:
              id: =@ctx.current.item.id
        - label: Delete
          icon: bin-2-alternate
          color: negative
          onPress:
            type: action.action-list
            options:
              isSequential: true
              actions:
                - type: action.execute-entity
                  options:
                    provider: DATA_PROVIDER_LOCAL
                    entity: _commandQueue
                    method: delete
                    data:
                      id: =@ctx.current.item.id
                - type: action.execute-entity
                  options:
                    provider: DATA_PROVIDER_LOCAL
                    method: delete
                    entity: customers_error
                    data:
                      id: =@ctx.current.item.id

actions:
  - numberOfVisibleActions: 2
    children:
      - type: action.retry-queue-command
        options:
          title: Retry all
          # Retry all items in the queue.
          id: =@ctx.datasources.command-queue.id
      - type: action.action-list
        options:
          title: Delete all
          isSequential: true
          actions:
            - type: action.delete-queue-command
              options:
                # Delete all items in the queue.
                id: =@ctx.datasources.command-queue.id
            - type: action.execute-entities
              options:
                provider: DATA_PROVIDER_LOCAL
                method: delete
                entity: customers_error
                # Delete multiple (all) records in the table.
                data: =@ctx.datasources.customers-errors.{"id":id}[]
```
{% endtab %}

{% tab title="datasource" %}
```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_LOCAL

  entities:
    - entity: customers_error

  query: |
    SELECT
      id,
      json_extract(data, '$.response.ok') as ok,
      json_extract(data, '$.response.status') as status,
      json_extract(data, '$.response.statusText') as statusText,
      json_extract(data, '$.response.headers') as headers,
      json_extract(data, '$.response.body') as body,
      json_extract(data, '$.type') as type
      FROM
      [customers_error]
```
{% endtab %}
{% endtabs %}

## Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or receives focus. This is achieved by calling the global action in the `onFocus` events.&#x20;

{% tabs %}
{% tab title="index.jigx" %}
```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onLoad is triggered when the app loads. 
# The sync-entities action in the global action (load-data)
# calls the Jigx REST function,
# and populates the local SQLite tables on the device
# with the data returned from REST service.
onLoad:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.execute-action
        options:
          action: load-data
      - type: action.execute-action
        options:
          action: load-us-states
          
onRefresh:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.execute-action
        options:
          action: load-data
      - type: action.execute-action
        options:
          action: load-us-states    
tabs:
  Home:
    jigId: home
    icon: home-apps-logo
    label: Home
  customers1:
    jigId: list-customers-hr1
    icon: number-one-square
    label: Customers
  customers2:
    jigId: list-customers-hr2
    icon: number-two-square
    label: All Customers
  customers3:
    jigId: list-customers-hr3
    icon: number-three-square
    label: Customers & Images
  errors:
    jigId: customer-errors
    icon: on-error-1
  listCommandQueue:
    jigId: list-command-queue
    icon: command-button-keyboard  
```
{% endtab %}

{% tab title="load-data.jigx" %}
```yaml
action:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: customers
              function: new-rest-get-customers
```
{% endtab %}

{% tab title="load-states.jigx" %}
```ruby
action:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: us-states
        function: new-rest-get-usStates
```
{% endtab %}
{% endtabs %}

### See Also

* [Configuring OAuth error messages](ttps://docs.jigx.com/administration/organization-settings/oauth-configurations#configuring-oauth-error-messages)
