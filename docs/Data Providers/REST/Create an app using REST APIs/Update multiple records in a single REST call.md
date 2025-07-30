# Update multiple records in a single REST call

## Why would you want to update multiple records in a single REST call?

**API Rate Limits** - Many APIs enforce rate limits on the number of requests a client can make. Updating multiple records in a single call reduces the number of API requests made and avoids hitting rate limits.

**Improved performance** - Updating multiple records in a single call reduces the round-trip time between the client and server, improving overall performance.

## How does this work

- To update multiple records in a single REST call, use the [execute-entities](./../../../Actions/execute-entities.md) action to call the REST function.
- It is important to know what method your function call is using. For example, using PUT will overwrite all values in the record, while using PATCH will only update the new or changed values in the record.
- There are two ways to configure the `execute-entities` action.
  - Use `parameters` for values that must be evaluated statically across all the records.
  - Values that are dynamic per record are configured in the `data` property.

:::CodeblockTabs
parameters

```yaml
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Update Record
          provider: DATA_PROVIDER_REST
          entity: customers
          method: update
          function: rest-update-customer
          # All records will be updated with Bronze tag
          # CustomerType is the same (static) across all records         
          parameters:
            customerType: Bronze    
```

data

```yaml
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Update Record
          provider: DATA_PROVIDER_REST
          entity: customers
          method: update
          goBack: stay
          function: rest-update-customer
          # All records will be updated dynamically per record.
          # Define the properties to be updated in the records.
          # Data must include all required properties on the record 
          # in the datasource.          
          data: =@ctx.datasources.customers.{"id":id, "firstName":firstName, "lastName":lastName, "companyName":companyName}[]           
```

:::

- The properties defined in the `data` property are determined by the REST call. This means that if the only required property is id you can simply use id, such as:
  `data: =@ctx.datasources.customers.{"id":id}[]`
  However, if you have multiple required properties in the REST call you need to define all of them under data, such as:
  `data: =@ctx.datasources.customers.{"id":id, "firstName":firstName, "lastName":lastName, "companyName":companyName}[]`
- Using JSONata expressions can further simplify updating mutiple records, for example, using the following expression will update all records in the customer list to Bronze.
  `data: =ctx.datasources.customers ~> | $ | { "customerType": "Bronze "} |`
  See the [Jsonata transform operator](https://docs.jsonata.org/other-operators#-------transform) for more information.

## Scenario

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
This example lists all customers without a label (`CustomerType` property). Using the `execute-entities` action all customers without a label are updated to show a Bronze label.
:::

:::VerticalSplitItem
![Update multiple records](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-5nIdPIlzJ5yk8C2piaNsh-20240926-075550.png "Update multiple records")
:::
::::

### How is this scenario configured

1. The customer list is loaded from the *customers* datasource, the query returns all records WHERE `customerType` IS NULL.
2. An `execute-entities` action is configured to update multiple records with a single REST call. The update function calls the REST APIs PATCH operation.
3. The `execute-entities` action is configured using `parameters` to update the `customerType` property to Bronze. This is a static value and will be the same for all the customers in the list.
4. The `execute-entities` action is configured using `data` to define the required REST properties for the customers' records. In this example, `id`, `firstName`, `lastName` and `companyName` are required parameters in the REST function.
5. When the Update records button is pressed all customers with no `customerType` property (label) is updated to *Bronze*.

## REST API

| **REST**         | **Detail**                                    |
| ---------------- | --------------------------------------------- |
| URL              | https\://\[your\_rest\_service]/api/customers |
| Operation/Method | PATCH                                         |

## Function

The REST APIs PATCH operator is used in a Jigx function with body parameters to specify the exact columns to be updated for the record. The `inputTransform` specifies how the data should be structured or formatted when being sent to the REST service. This transformation process ensures that the data adheres to the expected schema or format required by the REST service for processing the request. Take note of the required parameters in the function as these are required in the `data` property of the `execute-entities` action.

:::CodeblockTabs
rest-update-customer.jigx

```yaml
provider: DATA_PROVIDER_REST
# Updates data in the REST Service 
# PATCH modifies only the specified fields or properties of the resource.
method: PATCH 
# Use your REST service URL 
url: https://[your_rest_service]/api/customers 
# Direct the function call to use local execution between the mobile device
# and the REST service.
format: text
useLocalCall: true 

parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution.
    value: service.oauth 

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
# Define the customer data to be updated in the record in the REST Service.  
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
```

:::

## Action (global)

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or is in focus on the device.

:::CodeblockTabs
load-data.jigx

```yaml
# The sync-entities action gets the data from the REST data provider 
# using the function.
# The global action can be referenced throughout the solution,
# for effieicency and performance.
# Data is synced from the REST data provider to a local data provider,
# on the device.
action: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: customers
        function: rest-get-customers
      - entity: us-states
        function: rest-get-usStates  
        
```

:::

## Jig (screen)

- Create a customers list jig where the *customer* datasource query is configured to return all customers with no label.
- Add an `execute-entities` action to call the function that will update all the customer records in the local table (using `method: update`) and in the REST service (`function: rest-update-customer`). Define the `parameter` property to update the `customerType` property to Bronze. Configuring the `data` property is used to configure the properties that are required to update all records in the list.

:::hint{type="success"}
An alternate option would be to use the following expression under data, removing the need for functionParameter:
`data: =ctx.datasources.customers ~> | $ | { "customerType": "Bronze "} |`
:::

:::CodeblockTabs
update-customerType.jigx

```yaml
title: Update Customer type
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/ha9zh6wnixblrbubrfg3e/business-5475661_640.jpg?rlkey=anemjh5c9qsspvzt5ri0i9hva&raw=1

onFocus:
  type: action.execute-action
  options:
    action: load-data

datasources:
   region:
    type: datasource.static
    options:
      data:
        - id: 1
          region: US Central
        - id: 2
          region: US East
        - id: 3
          region: US West
   customerType:
    type: datasource.static
    options:
      data:
        - id: 1
          type: New
          value:
        - id: 2
          type: Gold
          value: Gold
        - id: 3
          type: Silver
          value: Silver
        - id: 4
          type: Bronze
          value: Bronze  
   customers: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers
      # Configure the WHERE statement to return all customers,
      # without a value (NULL) for for the customerType property.
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
          json_extract(cus.data, '$.region') AS region,
          json_extract(cus.data, '$.logo') AS logo
        FROM 
          [customers] AS cus
        WHERE json_extract(cus.data, '$.customerType') IS NULL 

children:
  - type: component.list
    options:
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
                    
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Update Record
          provider: DATA_PROVIDER_REST
          entity: customers
          method: update
          function: rest-update-customer
          # Use parameters for values that must be evaluated 
          # statically, across all the records. 
          # All records in the list will be updated to Bronze.          
          parameters:
            customerType: Bronze 
          # Use data to define the required REST paramameter fields
          # to be updated.             
          data: =@ctx.datasources.customers.{"id":id, "firstName":firstName, "lastName":lastName, "companyName":companyName}[]
```

:::

## Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or receives focus. This is achieved by calling the global action in the `OnFocus` and `onLoad` events.

:::CodeblockTabs
index.jigx

```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onFocus is triggered whenever the jig is displayed. 
# The sync-entities action in the global action calls the Jigx REST function
# and populates the local SQLite tables on the device
# with the data returned from REST service.
onFocus: 
  type: action.execute-action
  options:
    action: load-data
# onLoad is triggered when the solution is loaded on the device. 
# The sync-entities action in the global action calls the Jigx REST function 
# and populates the local SQLite tables on the device with the data 
# returned from REST service.        
onLoad: 
  type: action.execute-action
  options:
    action: load-data
    
tabs:
  home:
    jigId: list-customers
    icon: home-apps-logo
```

:::
