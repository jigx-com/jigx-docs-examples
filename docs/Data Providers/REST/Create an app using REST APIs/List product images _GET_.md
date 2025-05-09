---
title: List product images (GET)
slug: 6OzZ-view
createdAt: Tue May 07 2024 09:03:17 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Oct 23 2024 11:46:08 GMT+0000 (Coordinated Universal Time)
---

## Scenario

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
From the list of customers, swipe left and select the *View* button. The customer's details are shown on a screen with the customer's location at the top, the contact person's details, and then a list of the customer's products with images.
:::

:::VerticalSplitItem
![List customer images](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CF8Qx6fZmON1dZIAYh5Ar_rest-list-images.png "List customer images")
:::
::::

### How does this work

The REST APIs GET operator for the customer and images table is used in the Jigx functions with an `outputTransform` to specify the exact data to be returned to be shown in the list and view. A `composite` jig with a `location` header, combines the view-customer.jigx and list-customer-images.jigx and uses `inputs` to know which customer's details to show. A global action is configured to sync the data in the app with the REST data provider calling the function. In turn, the global action is called in the index.jigx file to load the data when the app is opened. In the jigs the local data provider is used to configure the components.

:::hint{type="info"}
This code sample builds upon the previous [List customers (GET)](<./List customers _GET_.md>) step, to develop a complete and functional solution.
:::

## REST API

| **REST**         | **Detail**                                                                     |
| ---------------- | ------------------------------------------------------------------------------ |
| URL              | https\://\[your\_rest\_service]/api/images?custId=\{custId}\&includeImage=true |
| Operation/Method | GET                                                                            |

## Function

Specify the REST API url and operation (method), parameters to include authentication in the header and in the `outputTransform` define the image metadata properties to be returned. The customer images are stored in the REST service in base64, Jigx requires the logo in local-uri format for display. A `conversion` is configured in the function to change the base64 to local-uri.

:::CodeblockTabs
rest-get-customer-images.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET #Fetches data from the REST Service
url: https://[your_rest_service]/api/images?custId={custId}&includeImage=true #Use your REST service URL 
useLocalCall: true #Direct the function call to use local execution between the mobile device and the REST service
forRowsWithValues: #Use forRowsWithValues with the customer Id to only get images specific to that customer instead of all rows (images)
  custId: custId 
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: service.oauth #Use manage.jigx.com to define credentials for your solution

  custId:
    type: string
    location: query
    required: true
#Define the customer images that must be fetched from the REST Service
outputTransform: |
  $.images.
    {
        "id": id,
        "custId": $$.inputs.custId,
        "createdDate": createdDate,
        "createdBy": createdBy,
        "description": description,
        "image": image
    }[]
#Convert the images returned from the REST service to local-uri which the jig expects to be able to display the image
conversions:
  - property: image
    from: base64
    to: local-uri
```
:::

## Action (global)&#x20;

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or  is in focus on the device.

The *rest-get-customers-images* function is NOT added to the `sync-entities` action due to the large number of images that will be returned. Rather the images are returned on demand in the jig per customer which reduces the number of images loaded on the device ensuring that the performance is not affected.

:::CodeblockTabs
load-data.jigx

```yaml
# The sync-entities action is used to get the data from the REST data provider using the function.
# The global action can be referenced throughout the solution for effieicency and performance.
# The data is synced from the REST data provider to a local data provider on the device.
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

- Use a list jig type to configure a list of customers.
- Use a list jig type to configure a list of customer product images.
- Use a default jig type to configure the customer details view.
- Since the data is already synced to the local Sqlite data provider, the jig's datasource is configured with a query to provide the data for use in the lists and view.
- &#x20;Create a `composite` jig and combine the default and image list jigs. In the header use a `location` component and an expression that uses `inputs` from the default jig's `jsonProperties` to show the address, city, state, and zip code of the customer.
- In the datasource query of the view-customer jig use `jsonProperties` to return the complex structure for address and phone.
- Configure a `queryParameter` using `inputs` to return the customer details by id in the datasource for the view-customer jig.
- Expressions are used to reference the exact data property required in each component of the view-customer jig.

:::CodeblockTabs
list-customer-images.jigx

```yaml
title: Products and Services
type: jig.list
icon: image-file-camera-alternate
#Add a placeholder if there are no images to return
placeholders:
  - title: It seems we're fresh out of visuals here
    when: =$count(@ctx.datasources.customerImages) = 0
    icon: loading-data
#Define the data to use in the jig, the data has been synced by the global action to the local data provider from the REST Service
datasources:
  customerImages: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
  
      entities:
        - entity: customer-images
  
      query: |
        SELECT 
          cim.id AS id,
          json_extract(cim.data, '$.createdDate') AS createdDate,
          json_extract(cim.data, '$.custId') AS custId,
          json_extract(cim.data, '$.createdBy') AS createdBy,
          json_extract(cim.data, '$.description') AS description,
          json_extract(cim.data, '$.image') AS image
        FROM 
          [customer-images] AS cim
        WHERE 
          json_extract(cim.data, '$.custId') = @custId
        ORDER BY 
          json_extract(cim.data, '$.createdDate') DESC

      queryParameters:
        custId: =@ctx.jig.inputs.customer.id

data: =@ctx.datasources.customerImages
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.description
    subtitle: =@ctx.current.item.createdBy
    leftElement: 
      element: image
      text: ''
      uri: =@ctx.current.item.image
                   
```

view-customer-details.jigx

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
        address: =@ctx.jig.inputs.customer.address & ' ' & @ctx.jig.inputs.customer.city & ', ' & @ctx.jig.inputs.customer.state & ', ' & @ctx.jig.inputs.customer.zip
#Define the data to use in the jig, the data has been synced by the global action to the local data provider from the REST Service
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
#Use jsonProperties to return the complex structure for address and phone      
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

customer-composite.jigx

```yaml
title: Customer Details
type: jig.composite

onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: customer-images
        function: rest-get-customer-images
        functionParameters:
          custId: =@ctx.jig.inputs.customer.id

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.location
      options:
        address: =@ctx.jig.inputs.customer.address & ' ' & @ctx.jig.inputs.customer.city & ', ' & @ctx.jig.inputs.customer.state & ', ' & @ctx.jig.inputs.customer.zip

children:
  - jigId: view-customer-details
    inputs:
      customer: =@ctx.jig.inputs.customer
  - jigId: list-customer-images
    inputs:
      customer: =@ctx.jig.inputs.customer
```

list-customers.jigx

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
#Define the data to use in the jig, the data has been synced by the global action to the local data provider from the REST Service
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
        parameters:
          customer: =@ctx.current.item
    swipeable:
      left:
        - onPress: 
            type: action.go-to
            options:
              parameters:
               customer: =@ctx.current.item  
# link to the composite to see the customer details and images                 
              linkTo: customer-composite
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
                type: action.execute-entity #action to execute the delete
                options:
#Use the REST data provider to call the delete function.                  
                  provider: DATA_PROVIDER_REST
                  entity: customers
                  method: delete #Delete the record from the local SQLite table
                  goBack: stay
                  function: rest-delete-customer #Delete the record from the REST service
#Specifiy the function parameters required by the function to delete the customer, in this example custId                 
                  functionParameters:
                    custId: =$number(@ctx.current.item.id) #id of customer record to be deleted in REST service                 
                  data:  
                    id: =@ctx.current.item.id #id of customer to be deleted from local data provider
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
:::

## Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or recieves focus. This is achieved by calling the global action in the `OnFocus` and `onLoad` events.

:::CodeblockTabs
index.jigx

```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onFocus is triggered whenever the jig is displayed. The sync-entities action in the global action calls the Jigx REST function and populates the local SQLite tables on the device with the data returned from REST service
onFocus: 
  type: action.execute-action
  options:
    action: load-data
# onLoad is triggered when the solution is loaded on the device. The sync-entities action in the global action calls the Jigx REST function and populates the local SQLite tables on the device with the data returned from REST service        
onLoad: 
  type: action.execute-action
  options:
    action: load-data
    
widgets:
  - size: 1x1 
    jigId: list-customers
```
:::

