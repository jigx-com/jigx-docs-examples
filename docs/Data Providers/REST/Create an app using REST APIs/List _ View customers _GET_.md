---
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

# List & View customers (GET)

## Scenario

In this scenario, records are limited to return only fifty from the REST service. Continuation is used to ensure all customer records are returned. By pressing on the customer in the [list of customers](<List customers _GET_.md>) loads that specific customer's details in a form.

## How does this work

The REST APIs GET operator is used in a Jigx function with an `outputTransform` to specify the exact data to be returned. A `continuation` is added to return all records; the records property specifies all records in the customer's table. A global action is configured to sync the data in the app with the REST data provider calling the function. In turn, the global action is called in the index.jigx file to load the data when the app is opened. In the list jig the local data provider is used to configure the list-item component. In the view-customer jig `jsonProperties` are used for address and phone to return the nested object.

<figure><img src="../../../../.gitbook/assets/REST-ListView.png" alt="List &#x26; view customer details" width="375"><figcaption><p>List &#x26; view customer details</p></figcaption></figure>

{% hint style="info" %}
This code sample builds upon the previous [List customers (GET)](<List customers _GET_.md>) step, to develop a complete and functional solution.
{% endhint %}

## REST API

<table><thead><tr><th width="180.8515625">REST</th><th>Detail</th></tr></thead><tbody><tr><td>URL</td><td>https://[your_rest_service]/api/customers</td></tr><tr><td>Operation/Method</td><td>GET</td></tr></tbody></table>

## Function

Specify the REST API url and operation (method), parameters to include authentication in the header and in the `outputTransform` define the data properties to be returned. Add a `continuation` and `record` cofiguartion to return all records from the customers table.

{% code title="rest-get-customer-cont.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
# Fetches data from the REST Service.
method: GET
# Use your REST service URL.  
url: https://[your_rest_service]/api/customers?continuation_enabled=true 
# Return data for rows with matching ids.
forRowsWithMatchingIds: true
# Direct the function call to use remote execution between the device
# and the REST service.
useLocalCall: false 

parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution.
    value: service.oauth 

  myparam:
    type: string
    location: query
    required: false
    value: myParamValue
# Continuation ensures all records are returned from the REST Service.
continuation:
  when: =$.next_link
  url: =$.next_link
# Specify that the records are from the customers table.
records: =$.customers
# Define the customer fields that must be fetched from the REST Service.
outputTransform: |
  {
    "customers": customers.{
        "id": custId,
        "firstName": firstName,
        "lastName": lastName,
        "companyName": companyName,
        "addresses": addresses,
        "phones": phones,
        "email": email,
        "web": web,
        "region": region,
        "customerType": customerType,
        "jobTitle": jobTitle
    },
    "next_link": next_link
  }
```
{% endcode %}

## Action (global)

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or is in focus on the device.

{% code title="load-data.jigx" %}
```yaml
# The sync-entities action is used to get the data from the REST data
# provider using the function. The global action can be referenced 
# throughout the solution for effieicency and performance. The data is
# synced from the REST data provider to a local data provider on the device.
action: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: customers
        function: rest-get-customers-cont
      - entity: us-states
        function: rest-get-usStates  
        
```
{% endcode %}

## Jig (screen)

* Use a list jig type to configure a list of customers.
* Since the data is already synced to the local Sqlite data provider, the jigs datasource is configured with a query to provide the data for use in the list.
* Add an `onPress` to link to the view-customer jig.
* In the datasource query of the view-customer jig use `jsonProperties` to return the complex structure for address and phone.
* configure a `queryParameter` using `inputs` to return the customer details by id.
* Expressions are used to reference the exact data property required in each component.

{% tabs %}
{% tab title="view-customer-details.jigx" %}
```yaml
title: Customer Details
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.location
      options:
        viewPoint: 
          centerPosition: middle
          # Use the JsonProperty to return nested objects in the REST JSON.
          address: =@ctx.datasources.customer-hr2.addresses[0].address & ' ' & @ctx.datasources.customer-hr2.addresses[0].city & ', ' & @ctx.datasources.customer-hr2.addresses[0].state & ', ' & @ctx.datasources.customer-hr2.addresses[0].zip
  
# Define the data to use in the jig, the data has been synced 
# by the global action to the local data provider from the REST Service.
datasources: 
  customer: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers 
      query: |
        SELECT 
          cus.id AS id, 
          json_extract(cus.data, '$.firstName') AS firstName, 
          json_extract(cus.data, '$.lastName') AS lastName,
          json_extract(cus.data, '$.companyName') AS companyName,
          json_extract(cus.data, '$.address') AS address,
          json_extract(cus.data, '$.city') AS city,
          json_extract(cus.data, '$.state') AS state,
          json_extract(cus.data, '$.zip') AS zip,
          json_extract(cus.data, '$.phone1') AS phone1,
          json_extract(cus.data, '$.phone2') AS phone2,
          json_extract(cus.data, '$.email') AS email,
          json_extract(cus.data, '$.web') AS web,
          json_extract(cus.data, '$.customerType') AS customerType,
          json_extract(cus.data, '$.jobTitle') AS jobTitle
        FROM 
          [customers] AS cus
        WHERE
          id = @custId
        ORDER BY 
          json_extract(cus.data, '$.companyName')
      queryParameters:
        custId: =@ctx.jig.inputs.customer.id
      # Use jsonProperties to return the complex structure for address 
      # and phone.      
      jsonProperties: 
        - addresses
        - phones
       
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Name
            value: =@ctx.datasources.customer.companyName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Contact
                  value: =@ctx.datasources.customer.firstName & ' ' & @ctx.datasources.customer.lastName
              - type: component.entity-field
                options:
                  label: Job Title
                  value: =@ctx.datasources.customer.jobTitle
        - type: component.entity-field
          options:
            contentType: email
            label: Email
            rightIcon: email
            value: =@ctx.datasources.customer.email
        - type: component.entity-field
          options:
            contentType: phone
            label: Phone
            rightIcon: phone
            value: =@ctx.datasources.customer.phone1
        - type: component.entity-field
          options:
            contentType: link
            label: Web
            value: =@ctx.datasources.customer.web      
```
{% endtab %}

{% tab title="list-customers.jigx" %}
```yaml
title: Global Customers
type: jig.list
icon: global-accelerator

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/ha9zh6wnixblrbubrfg3e/business-5475661_640.jpg?rlkey=anemjh5c9qsspvzt5ri0i9hva&raw=1
# Define the data to use in the jig, the data has been synced by the global 
# action to the local data provider from the REST Service.
datasources:
  customers: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers  
      query: |
        SELECT 
          cus.id AS id, 
          json_extract(cus.data, '$.firstName') AS firstName, 
          json_extract(cus.data, '$.lastName') AS lastName,
          json_extract(cus.data, '$.companyName') AS companyName,
          json_extract(cus.data, '$.address') AS address,
          json_extract(cus.data, '$.city') AS city,
          json_extract(cus.data, '$.state') AS state,
          json_extract(cus.data, '$.zip') AS zip,
          json_extract(cus.data, '$.phone1') AS phone1,
          json_extract(cus.data, '$.phone2') AS phone2,
          json_extract(cus.data, '$.email') AS email,
          json_extract(cus.data, '$.web') AS web,
          json_extract(cus.data, '$.customerType') AS customerType,
          json_extract(cus.data, '$.jobTitle') AS jobTitle,
          json_extract(cus.data, '$.logo') AS logo
        FROM 
          [customers] AS cus
        -- ORDER BY 
        --  json_extract(cus.data, '$.companyName')

data: =@ctx.datasources.customers
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.companyName
    subtitle: =@ctx.current.item.firstName & ' ' & @ctx.current.item.lastName
    leftElement: 
      element: avatar
      text: =@ctx.current.item.state
      uri: =@ctx.current.item.logo
    label:
      title: =$uppercase((@ctx.current.item.customerType = 'Silver' ? @ctx.current.item.customerType:@ctx.current.item.customerType = 'Gold' ? @ctx.current.item.customerType:''))
      color:
        - when: =@ctx.current.item.customerType = 'Gold'
          color: color3
        - when: =@ctx.current.item.customerType = 'Silver'
          color: color14
    onPress: 
      type: action.go-to
      options:
        linkTo: update-customer
        inputs:
          customer: =@ctx.current.item
          
    swipeable:
      left:
# Add an onPress event to view the customer's details.      
        - onPress: 
            type: action.go-to
            options:
              inputs:
               customer: =@ctx.current.item
               id: =@ctx.current.item.id    
              linkTo: view-customer-details
          label: View
          icon: view
        - label: DELETE
          icon: delete-2
          color: negative
          onPress: 
            type: action.confirm
            options:
              isConfirmedAutomatically: false
              onConfirmed:
               # Action to execute the delete. 
               type: action.execute-entity 
                options:
                  # Use the REST data provider to call the delete function.                  
                  provider: DATA_PROVIDER_REST
                  entity: customers
                  # Delete the record from the local SQLite table.
                  method: delete 
                  goBack: stay
                  # Delete the record from the REST service.
                  function: rest-delete-customer 
                  #Specifiy the function parameters required by the function
                  # to delete the customer, in this example custId.                 
                  parameters:
                  # id of customer record to be deleted in REST service. 
                    custId: =$number(@ctx.current.item.id)                 
                  data:
                    # id of customer to be deleted from local data provider.  
                    id: =@ctx.current.item.id 
              modal:
                title: Are you sure?
                description: =('Press Confirm to permanently delete ' & @ctx.current.item.companyName)

actions:
  - children:
      - type: action.go-to
        options:
          title: Add Customer
          linkTo: new-customer
```
{% endtab %}
{% endtabs %}

## Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or receives focus. This is achieved by calling the global action in the `OnFocus` and `onLoad` events.

{% code title="index.jigx" %}
```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onFocus is triggered whenever the jig is displayed.
# The sync-entities action in the global action calls the Jigx REST function 
# and populates the local SQLite tables on the device with the data returned 
# from REST service. 
onFocus: 
  type: action.execute-action
  options:
    action: load-data
# onLoad is triggered when the solution is loaded on the device. 
# The sync-entities action in the global action calls the Jigx REST function
# and populates the local SQLite tables on the device with the data returned 
# from REST service.        
onLoad: 
  type: action.execute-action
  options:
    action: load-data
    
tabs:
  home:
    jigId: list-customers
    icon: home-apps-logo
```
{% endcode %}
