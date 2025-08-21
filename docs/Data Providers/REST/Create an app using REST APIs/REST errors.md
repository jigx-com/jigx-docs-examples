# REST errors

## Scenario

{% columns %}
{% column %}
When trying to view a customer and their details or create a new customer in the app, the app can fail to retrieve or create the required data, and various errors are returned. In this example, we add error handling to the REST endpoint function to cater for the following errors:

* 401 Unauthorized
* 403 Forbidden
* Unexpected error&#x20;
{% endcolumn %}

{% column %}
<figure><img src="../../../../.gitbook/assets/REST-errors.gif" alt="REST Error handling" width="326"><figcaption><p>REST Error handling</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## How does this work

An `error` section is added to the REST endpoint functions for creating customers (POST), viewing customers (GET), and updating customers (PUT). In this section, the `when` property is configured with an expression that returns the response status from the endpoint, for example, `=@ctx.response.status = 403`. There are multiple `when` properties configured to catch a 401 and 403 error; all other response statuses are caught in the Unexpected error. Each `when` property has a `title`, `icon`, and `description`, which provides a user-friendly explanation of the error. Errors are written to the customers\_error `table`, and the data written to the table is configured in the `transform` property. The `table,` in conjunction with the `commandQueue` is used to troubleshoot the error and create jigs that allows you to retry the REST call or delete the error from the `commandQueue`. See [REST error handling](<REST errors.md>) for more information.

## REST API

<table><thead><tr><th width="216.125">REST</th><th>Detail</th></tr></thead><tbody><tr><td>URL</td><td>https://[your_rest_service]/api/customers</td></tr><tr><td>Operation/Method</td><td>POST,GET,PUT</td></tr></tbody></table>

## Function

In each of the REST function files (GET, POST, PUT), add an `error` section and configure the YAML to cater for a 401 and 403 error, and a section to cater for all other response errors.

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
    # Configure the specific REST endpoint error that is returned. 
  - when: =@ctx.response.status = 401
    # Choose an icon to show in the error message.  
    icon: on-error-sad
    # Provide a short meaningful title for the error.    
    title: Oops! Something Went Wrong
    # Describe a user-friendly explanation for the error.     
    description: "It seems like you don’t have permission to Add customers.
      If you think this is a mistake, please contact support. We’re here to help!"
    details: =('Error:' & ' ' & @ctx.response.statusText & ' (' &
      @ctx.response.status & ')')
    # Write the error to the customer_error table      
    table: =@ctx.entity & "_error"
    # Send a notification to the app user using the title, description, 
    #detail and icon properties.    
    notification: true
    # Specifiy what data must be written in the error table.     
    transform: 
      '={ "id": @ctx.commandId, "type": "System Offline", 
      "screen": "system-offline",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # Add the number of retries and the time between each retry.   
    retry:
      delay: "=(@ctx.response.headers.'retry-after' ? $number(@ctx.response.headers.'retry-after') : 5) * 1000"
      maxRetries: 3  
    # Configure the next error that could be returned from the REST endpoint. 
  - when: =@ctx.response.status = 403
    title: System Offline
    description: 
      It looks like our system is temporarily unavailable. 
      We're working hard to fix this and get things back on 
      track. Please try again in a little while. Thank you 
      for your patience!
    details: =@ctx.response.body
    icon: server-error-403-hand-forbidden
    notification: true
    table: =@ctx.entity & "_error"
    transform: 
      '={ "id": @ctx.commandId, "type": "System Offline", 
      "screen": "system-offline",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # All other returned REST endpoint errors will be caught
    # under the Unexpected error section. 
  - title: Unexpected error
    description: 
      An unexpected error occurred. Support has been notified and will
      reach out via email once the issue is resolved.
    details: =@ctx.response.body
    # Set an automatic retry, specify the delay befre the retry is actioned,
    # Set the number of retries allowed.        
    retry:
      delay: "=(@ctx.response.headers.'retry-after' ? $number(@ctx.response.headers.'retry-after') : 5)*1000"
      maxRetries: 3
    icon: 
    table: =@ctx.entity & "_error"
    notification: true
    transform: 
      '={ "id": @ctx.commandId, "type": "nexpected error", 
      "screen": "customer-error-500", "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
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
    # Configure the specific REST endpoint error that is returned. 
  - when: =@ctx.response.status = 403
    # Provide a short meaningful title for the error.   
    title: System Offline
    # Describe a user-friendly explanation for the error.     
    description: 
      It looks like our system is temporarily unavailable. 
      We're working hard to fix this and get things back on 
      track. Please try again in a little while. Thank you 
      for your patience!
    details: =@ctx.response.body
    # Choose an icon to show in the error message.    
    icon: server-error-403-hand-forbidden
    # Send a notification to the app user using the title, description, 
    # detail and icon properties.        
    notification: true
    table: datasync-error
    transform: 
      '={ "id": @ctx.parameters.syncId, "type": "System Offline", 
      "screen": "system-offline",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # Specifiy what data must be written in the error table.     
  - when: =@ctx.response.status = 401
    title: Access Denied
    description: 
      "It seems like you don’t have permission to sync data 
      right now. If you think this is a mistake, please contact 
      support or try again later. We’re here to help!"
    # details: =@ctx.response
    icon: on-error-sad
    notification: true
    table: datasync-error
    transform: 
      '={ "id": @ctx.parameters.syncId, "type": "Unauthorized", 
      "screen": "access-denied",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # All other returned REST endpoint errors will be caught
    # under the Unexpected error section.     
  - title: Oops! Something Went Wrong
    description: 
      "We’re not sure what happened, but we’re working on it. Please 
      try again later. If the problem persists, feel free to reach out 
      to our support team. Thanks for your understanding!"
    icon: on-error-sad
    notification: true
    table: datasync-error
    transform: 
      '={ "id": @ctx.parameters.syncId, "type": "Unknown", 
      "screen": "error",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
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
    # Configure the specific REST endpoint error that is returned. 
  - when: =@ctx.response.status = 401
    # Choose an icon to show in the error message.  
    icon: on-error-sad
    # Provide a short meaningful title for the error.    
    title: Oops! Something Went Wrong
    # Describe a user-friendly explanation for the error.     
    description: "It seems like you don’t have permission to Add customers.
      If you think this is a mistake, please contact support. We’re here to help!"
    details: =('Error:' & ' ' & @ctx.response.statusText & ' (' &
      @ctx.response.status & ')')
    # Write the error to the customer_error table.      
    table: =@ctx.entity & "_error"
    # Send a notification to the app user using the title, description,
    # detail and icon properties.    
    notification: true
    # Specifiy what data must be written in the error table.     
    transform: 
      '={ "id": @ctx.commandId, "type": "System Offline", 
      "screen": "system-offline",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # Configure the next error that could be returned from the REST endpoint 
  - when: =@ctx.response.status = 403
    title: System Offline
    description: 
      It looks like our system is temporarily unavailable. 
      We're working hard to fix this and get things back on 
      track. Please try again in a little while. Thank you 
      for your patience!
    details: =@ctx.response.body
    icon: server-error-403-hand-forbidden
    notification: true
    
    table: =@ctx.entity & "_error"
    transform: 
      '={ "id": @ctx.commandId, "type": "System Offline", 
      "screen": "system-offline",  "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
    # All other returned REST endpoint errors will be caught
    # under the Unexpected error section. 
  - title: Unexpected error
    description: 
      An unexpected error occurred. Support has been notified and will
      reach out via email once the issue is resolved.
    details: =@ctx.response.body
    icon: 
    table: =@ctx.entity & "_error"
    notification: true
    transform: 
      '={ "id": @ctx.commandId, "type": "nexpected error", 
      "screen": "customer-error-500", "response": @ctx.response, 
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
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
# Return the details that you specificied in the function transform property 
  query: 
    SELECT 
      id,
      json_extract(err.data, '$.response.ok') as ok, 
      json_extract(err.data, '$.response.status') as status, 
      json_extract(err.data, '$.response.statusText') as statusText, 
      json_extract(err.data, '$.response.headers') as headers, 
      json_extract(err.data, '$.response.body') as body,
      json_extract(err.data, '$.screen') as screen,
      json_extract(err.data, '$.type') as type
    FROM 
      [customers_error] AS error
```
{% endcode %}

## Jigs (screens)

There are a number of options available to process items that are in an error state.

1. Use the **commandQueue**. Items that return an error from the REST endpoint will remain on the commandQueue and are not automatically processed by the queue. You must configure an action to either retry the item or delete the item from the queue. The retry executes the REST call again.
2. Use the _**customer\_error**_ table configured in the function. Use the data from the table in a jig to allow app users to resolve the error or delete the item in error.

## Use the commandQueue

Create two jigs to work with the items in the [commandQueue](<REST errors.md>). This is helpful for the solution owner or administrator to take action and `delete` errors in the queue or possibly `retry` the REST call to process the items in the queue that are in an error state. Configure a list jig containing all items in the commandQueue, add a left `swipeable` action to cater for the delete and retry actions, also add an `onPress` event to go to view the payload details of the item in error.

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

{% tab title="view-command-queue.jigx" %}
```yaml
title: View Queue Command
type: jig.default

# The command queue requires the CommandId as an input,
# set as a parameter from in the list jig.
inputs:
  commandId:
    type: string
    required: true
# Configure a datasource to return the data for the selected 
# item from the system table.
datasources:
  queued-command:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _commandQueue
      query: |
        SELECT
          id, queue, type, payload, state, error
        FROM [_commandQueue]
        WHERE id = @id;
      queryParameters:
        id: =@ctx.inputs.commandId
      isDocument: true
  
# Configure the fields to be jig to show the data from the table.        
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: General
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      instanceId: commandId
                      options:
                        label: Id
                        value: =@ctx.jig.inputs.commandId
                    - type: component.entity-field
                      instanceId: state
                      options:
                        label: State
                        value: =@ctx.datasources.queued-command.state
                        style:
                          isPrimary: true
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      instanceId: queue
                      options:
                        label: Queue
                        value: =@ctx.datasources.queued-command.queue
                    - type: component.entity-field
                      instanceId: type
                      options:
                        label: Type
                        value: =@ctx.datasources.queued-command.type
                        style:
                          isPrimary: true

        - type: component.section
          options:
            title: Details
            children:
              - type: component.entity-field
                instanceId: error
                options:
                  label: Error
                  value: =@ctx.datasources.queued-command.error
                  isMultiline: true
              - type: component.entity-field
                instanceId: payload
                options:
                  label: Payload
                  value: =@ctx.datasources.queued-command.payload
                  isMultiline: true
                  contentType: json
# Add a rety and delete button at the bottom of the jig.                  
actions:
  - children:
      - type: action.retry-queue-command
        options:
          title: Retry
          id: =@ctx.jig.inputs.commandId
      - type: action.delete-queue-command
        options:
          title: Delete
          id: =@ctx.jig.inputs.commandId
```
{% endtab %}
{% endtabs %}

## Use the customers\_error table

Create a list jig to list the records in the customers\_error table. Provide detail of the error in the `title` and `subtitle` properties.

{% tabs %}
{% tab title="list-customer-errors.jigx" %}
```javascript
title: Issues
description: A list of customer records that failed to be created successfully and need manual intervention for resolution.
type: jig.list
icon: on-error-1
# Show the number of issues in the list, in a badge on the home widget.  
badge: =$count(@ctx.datasources.customer-errors)

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/vurcs49k07rna87zuhdsc/customer_issues.png?rlkey=b23lhiqprqie55v2x99u2otyy&st=upbpp2hk&raw=1

datasources:
  customer-errors:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL 
      entities:
        - entity: customers_error
      query: 
        SELECT 
          id,
          json_extract(err.data, '$.response.ok') as ok, 
          json_extract(err.data, '$.screen') as screen,
          json_extract(err.data, '$.type') as type,
          json_extract(err.data, '$.entity') as entity,
          json_extract(err.data, '$.response') as response,
          json_extract(err.data, '$.request') as request,
          json_extract(err.data, '$.solution') as solution,
          json_extract(err.data, '$.user') as user,
          json_extract(err.data, '$.request.body') as body
        FROM
          [customers_error] AS err
        ORDER BY id
        
      jsonProperties: 
        - body
        - response
    
data: =@ctx.datasources.customer-errors
item:
  type: component.list-item
  options:
    title: =('Creating "' & @ctx.current.item.body.companyName & '" failed')
    subtitle: =(@ctx.current.item.response.status = 401 ? 'You dont have the required permission':@ctx.current.item.response.status = 403 ? 'The system was offline, try again':'')
    description: =('Error:' & ' ' & @ctx.current.item.response.statusText & ' - ' & @ctx.current.item.response.status)
    onPress: 
      type: action.go-to
      options:
        linkTo: =(@ctx.current.item.response.status = 401 ? 'customer-error-401':@ctx.current.item.response.status = 403 ? 'customer-error-403':'customer-error-500')
        inputs:
          commandId: =@ctx.current.item.id
    leftElement: 
      element: icon
      icon: =(@ctx.current.item.response.status = 401 ? 'lock-1':@ctx.current.item.response.status = 403 ? 'server-error-403-hand-forbidden':'on-error-1')
    rightElement: 
      element: icon
      icon: arrow-right

widgets:
  errorStatus: 
    type: widget.status
    options:
      statuses:
        - when: true
          icon: on-error-1
```
{% endtab %}

{% tab title="customer-error-401.jigx" %}
```yaml
title: Resolve Issue
type: jig.default

inputs:
  commandId:
    type: string
    required: true

datasources:
  customer-errors:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers_error
      query: 
        SELECT 
          id,
          json_extract(err.data, '$.response.ok') as ok, 
          json_extract(err.data, '$.screen') as screen,
          json_extract(err.data, '$.type') as type,
          json_extract(err.data, '$.entity') as entity,
          json_extract(err.data, '$.response') as response,
          json_extract(err.data, '$.request') as request,
          json_extract(err.data, '$.solution') as solution,
          json_extract(err.data, '$.user') as user,
          json_extract(err.data, '$.request.body') as body
        FROM
          [customers_error] AS err
        WHERE
          id = @commandId         
      queryParameters:
        commandId: =@ctx.jig.inputs.commandId      
      jsonProperties: 
        - body
        - response  
      isDocument: true

  queued-command:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _commandQueue
      query: |
        SELECT
          id, 
          queue, 
          type, 
          payload, 
          state, 
          error
        FROM 
          [_commandQueue]
        WHERE 
          id = @id;
      queryParameters:
        id: =@ctx.jig.inputs.commandId 
      isDocument: true
  
children:
  - type: component.custom-component
    componentId: error-component
    inputs:
      icon: on-error-sad
      iconColor: negative
      errorTitle: 
        =@ctx.datasources.customer-errors.response.statusText & ' (' & 
        @ctx.datasources.customer-errors.response.status & ')'
      errorDescription: 
        "It seems you don’t have permission to create customers at the moment. 
        If you believe this is an error, please contact support.    
        We're here to assist!"
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.datasources.customer-errors.body.companyName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.customer-errors.body.firstName
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.customer-errors.body.lastName
        - type: component.entity-field
          options:
            label: Job Title
            value: =@ctx.datasources.customer-errors.body.jobTitle
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.customer-errors.body.email
            contentType: email
        - type: component.entity-field
          options:
            label: Web
            value: =@ctx.datasources.customer-errors.body.web
            contentType: link
                  
actions:
  - children:
      - type: action.info-modal
        options:
          title: Contact Support
          modal:
            title: Not yet implemented
            buttonText: comming soon
      - type: action.action-list
        options:
          title: Try again
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_LOCAL
                entity: customers_error
                method: delete
                goBack: previous
                data:
                  id: =@ctx.jig.inputs.commandId
            - type: action.retry-queue-command
              options:
                id: =@ctx.jig.inputs.commandId
      - type: action.action-list
        options:
          title: Delete
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_LOCAL
                entity: customers_error
                method: delete
                goBack: previous
                data:
                  id: =@ctx.jig.inputs.commandId
            - type: action.delete-queue-command
              options:
                id: =@ctx.jig.inputs.commandId
```
{% endtab %}

{% tab title="customer-error-403.jigx" %}
```yaml
title: Resolve Issue
type: jig.default

inputs:
  commandId:
    type: string
    required: true

datasources:
  customer-errors:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL   
      entities:
        - entity: customers_error
      query: 
        SELECT 
          id,
          json_extract(err.data, '$.response.ok') as ok, 
          json_extract(err.data, '$.screen') as screen,
          json_extract(err.data, '$.type') as type,
          json_extract(err.data, '$.entity') as entity,
          json_extract(err.data, '$.response') as response,
          json_extract(err.data, '$.request') as request,
          json_extract(err.data, '$.solution') as solution,
          json_extract(err.data, '$.user') as user,
          json_extract(err.data, '$.request.body') as body
        FROM
          [customers_error] AS err
        WHERE
          id = @commandId          
      queryParameters:
        commandId: =@ctx.jig.inputs.commandId        
      jsonProperties: 
        - body
        - response      
      isDocument: true

  queued-command:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _commandQueue
      query: |
        SELECT
          id, 
          queue, 
          type, 
          payload, 
          state, 
          error
        FROM 
          [_commandQueue]
        WHERE 
          id = @id;      
      queryParameters:
        id: =@ctx.jig.inputs.commandId 
      isDocument: true
  
children:
  - type: component.custom-component
    componentId: error-component
    inputs:
      icon: server-error-403-hand-forbidden
      iconColor: negative
      errorTitle: 
        =@ctx.datasources.customer-errors.response.statusText & ' (' & 
        @ctx.datasources.customer-errors.response.status & ')'
      errorDescription: 
        It looks like our system is temporarily unavailable. We're working
        hard to fix this and get things back on track. Please try again
        in a little while. Thank you for your patience!
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.datasources.customer-errors.body.companyName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.customer-errors.body.firstName
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.customer-errors.body.lastName
        - type: component.entity-field
          options:
            label: Job Title
            value: =@ctx.datasources.customer-errors.body.jobTitle
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.customer-errors.body.email
            contentType: email
        - type: component.entity-field
          options:
            label: Web
            value: =@ctx.datasources.customer-errors.body.web
            contentType: link
                  
actions:
  - children:
      - type: action.action-list
        options:
          title: Try again
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_LOCAL 
                entity: customers_error
                method: delete
                goBack: previous
                data:
                  id: =@ctx.jig.inputs.commandId
            - type: action.retry-queue-command
              options:
                id: =@ctx.jig.inputs.commandId
            
      - type: action.action-list
        options:
          title: Delete
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_LOCAL
                entity: customers_error
                method: delete
                goBack: previous
                data:
                  id: =@ctx.jig.inputs.commandId
            - type: action.delete-queue-command
              options:
                id: =@ctx.jig.inputs.commandId
```
{% endtab %}

{% tab title="customer-error-500.jigx" %}
```yaml
title: Resolve Issue
type: jig.default

inputs:
  commandId:
    type: string
    required: true

datasources:
  customer-errors:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers_error
      query: 
        SELECT 
          id,
          json_extract(err.data, '$.response.ok') as ok, 
          json_extract(err.data, '$.screen') as screen,
          json_extract(err.data, '$.type') as type,
          json_extract(err.data, '$.entity') as entity,
          json_extract(err.data, '$.response') as response,
          json_extract(err.data, '$.request') as request,
          json_extract(err.data, '$.solution') as solution,
          json_extract(err.data, '$.user') as user,
          json_extract(err.data, '$.request.body') as body
        FROM
          [customers_error] AS err
        WHERE
          id = @commandId          
      queryParameters:
        commandId: =@ctx.jig.inputs.commandId       
      jsonProperties: 
        - body
        - response     
      isDocument: true

  queued-command:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        # jigx-ignore
        - _commandQueue
      # jigx-ignore
      query: |
        SELECT
          id, 
          queue, 
          type, 
          payload, 
          state, 
          error
        FROM 
          [_commandQueue]
        WHERE 
          id = @id;     
      queryParameters:
        id: =@ctx.jig.inputs.commandId      
      isDocument: true
  
children:
  - type: component.custom-component
    componentId: error-component
    inputs:
      icon: server-error-500-desktop
      iconColor: negative
      errorTitle: 
        =@ctx.datasources.customer-errors.response.statusText & ' (' & 
        @ctx.datasources.customer-errors.response.status & ')'
      errorDescription: 
        An unexpected error occurred. Support has been notified and will
        reach out via email once the issue is resolved.
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.datasources.customer-errors.body.companyName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.customer-errors.body.firstName
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.customer-errors.body.lastName
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.customer-errors.body.email
            contentType: email
        - type: component.entity-field
          options:
            label: Web
            value: =@ctx.datasources.customer-errors.body.web
            contentType: link
```
{% endtab %}
{% endtabs %}

## Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or receives focus. This is achieved by calling the global action in the `onFocus` events. The `action.sync-entities` action will delete any items from the local data provider that were deleted from the commandQueue.

{% code title="index.jigx" %}
```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onFocus is triggered when the home hub loads. 
# The sync-entities action in the global action (load-data)
# calls the Jigx REST function,
# and populates the local SQLite tables on the device
# with the data returned from REST service.
onFocus: 
  type: action.execute-action
  options:
    action: load-data
    
tabs:
  home:
    # Jig listing customers.
    jigId: list-customers
    icon: home-apps-logo
  errors:   
    # Jig listing errors from the customers_error table.  
    jigId: customer-errors
    icon: on-error-1
  list:
    # Jig listing items on the commandQueue that need to be processed. 
    jigId: list
    icon: list  
```
{% endcode %}
