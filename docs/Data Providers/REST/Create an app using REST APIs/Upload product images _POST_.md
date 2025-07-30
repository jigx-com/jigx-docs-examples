# Upload product images (POST)

## Scenario

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
From the [view customer ](<./List _ View customers _GET_.md>) On the screen, tap the *Add Images* button, which will direct you to a screen that allows you to upload multiple images of products for each customer.
:::

:::VerticalSplitItem
![Upload images using REST](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9JpcY3lPb4m2WL0w-v4il_rest-image.PNG "Upload images using REST")
:::
::::

### How does this work

The REST APIs POST operator for the images table is used in a Jigx function with an `inputTransform` to capture the image metadata. configuring the `conversion` property ensures that the images are uploaded in the correct format to the REST service. Specifying the id in the `ouputTransform` in the function enables the local data provider temp\_id to be automatically updated with the REST id once the images are created in the datastore. The `media-field` takes a photo or selects from existing images on the device.

:::hint{type="info"}
This code sample builds upon the previous [List customers (GET)](<./List customers _GET_.md>) step, to develop a complete and functional solution.
:::

## REST API

| **REST**         | **Detail**                                 |
| ---------------- | ------------------------------------------ |
| URL              | https\://\[your\_rest\_service]/api/images |
| Operation/Method | POST                                       |

## Function

The REST APIs POST operator is used in a Jigx function with body parameters to specify the exact columns to be created for the image record. The `inputTransform` specifies the image metadata that is sent to the REST service. This transformation process ensures that the data adheres to the expected schema or format required by the REST service for processing the request. In the `outputTransform` the id is configured to ensure that the properties are automatically returned once the image is created and the local provider's temp\_id is updated with the actual id. The customer images are stored in the REST service in base64, Jigx stores the iamges in local-uri format for display. A `conversion` is configured in the function to change the images from local-uri to base64.

:::CodeblockTabs
rest-upload-customer-images.jigx

```yaml
provider: DATA_PROVIDER_REST
# Creates data in the backend.
method: POST 
# Use your REST service URL.
url: https://jigx-training.azurewebsites.net/api/images 
# Direct the function call to use local execution between the mobile device
# and the REST service.  
useLocalCall: true 
 
parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution.
    value: service.oauth 

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
# Define the image metadata that must be created in the record in the REST API.    
inputTransform: |
  {
    "custId": custId,
    "createdBy": createdBy,
    "description": description,
    "createdDate": createdDate,
    "image": image
  }
# Specifiying an outputTransform for the image_id ensure that the id created
# by the REST API is automatically synced back to the Jigx local datasource
# replacing the temp_id.    
outputTransform: |
  $.{
      "id": image_id
    }
# Convert the images to be uploaded to the REST service to base64 
# which the REST service expects to be able to store the image.  
conversions:
  - property: image
    from: local-uri
    to: base64
```
:::

## Action (global)&#x20;

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or  is in focus on the device.

The *rest-get-customers-images* function is NOT added to the `sync-entities` action due to the large number of images that will be returned. Rather the images are returned on demand in the jig per customer which reduces the number of images loaded on the device ensuring that the performance is not affected.

:::CodeblockTabs
load-data.jigx

```yaml
# The sync-entities action is used to get the data from the REST
# data provider using the function.
# The global action can be referenced throughout the solution 
# for effieicency and performance.
# The data is synced from the REST data provider to a local data provider
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

- On the customer-composite jig add a `go-to` action to add a button that links to the add-customer-images jig.
- Add parameters to the `go-to` action to use the customer id as `inputs`.
- Use a default jig with the `media-picker` component to capture or select images.
- Add an `execute-entities` action to call the rest-upload-customer-images function and use the `media-field`'s state to configure the metadata to be uploaded for the image.

:::CodeblockTabs
add-customer-images.jigx

```yaml
title: Upload images
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/o1gobv6lj1l3076veyaff/cloud-7906280_1280.png?rlkey=c5ad2oknpw5fju9qjlb1c2d2o&raw=1
# Set the onFocus to clear all data from the jig and reset it
# for the next upload.
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.newImage.state.data
    
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.jig.inputs.customer.companyName
  - type: component.form
    instanceId: newImage
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: description
          options:
            label: Add the product name
        - type: component.media-field
          instanceId: image
          options:
            label: image
            mediaType: image
            isMultiple: true
            maximumFileSize: =20 * 1024 * 1024

actions:
  - children:
        # Action to upload the images.
      - type: action.execute-entities 
        options:
          title: Upload images
          provider: DATA_PROVIDER_REST
          entity: customer-images
          # Create the image record in the local SQLite table. 
          method: create 
          # Create the image record in the REST service.
          function: rest-upload-customer-images 
           # Data configuration points to the collection of images 
           # with their metadata.
           # in the media-picker ensuring that the call to POST. 
           # & create is executed multiple times for each image.
            =@ctx.components.image.state.value.
            {
              "custId": @ctx.jig.inputs.customer.id,
              "createdBy": @ctx.user.email,
              "description": @ctx.jig.components.description.state.value,
              "createdDate": $now(),
              "image": $ 
            }
          onSuccess: 
              type: action.go-back  
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
# Define the data to use in the jig, the data has been synced by the global
# action to the local data provider from the REST Service.
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

customer-composite.jigx

```yaml
title: Customer Details
type: jig.composite
# Add an onFocus to return the. images for the specific customer 
# using the id. This is on demand syncing to limit the images returned.
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: customer-images
        function: rest-get-customer-images
        parameters:
          custId: =@ctx.jig.inputs.customer.id

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.location
      options:
        viewPoint:
          centerPosition: middle
          address: =@ctx.jig.inputs.customer.address & ' ' & @ctx.jig.inputs.customer.city & ', ' & @ctx.jig.inputs.customer.state & ', ' & @ctx.jig.inputs.customer.zip

children:
  - jigId: view-customer-details
    inputs:
      customer: =@ctx.jig.inputs.customer
  - jigId: list-customer-images
    inputs:
      customer: =@ctx.jig.inputs.customer
      
actions:
  - children:
      - type: action.go-to
        options:
          title: Add images
          linkTo: add-customer-images
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
# Define the data to use in the jig, the data has been synced
# by the global action to the local data provider from the REST Service.
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
        - onPress: 
            type: action.go-to
            options:
              inputs:
               customer: =@ctx.current.item  
              # Link to the composite to see the customer details and images.                 
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
                  # Specifiy the function parameters required by the
                  # function to delete the customer, in this example custId                 
                  parameters:
                    # id of customer record to be deleted in REST service.
                    custId: =$number(@ctx.current.item.id)                  
                  data:  
                    # id of customer to be deleted from local data provider
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
:::

## &#x20;Index

For performance and offline support the data is synced from the REST service as soon as the app is opened or receives focus. This is achieved by calling the global action in the `OnFocus` and `onLoad` events.

:::CodeblockTabs
index.jigx

```yaml
name: hello-rest-example
title: Hello REST Solution
category: sales
# onFocus is triggered whenever the jig is displayed. 
# The sync-entities action in the global action calls the Jigx REST function
# and populates the local SQLite tables on the device with the data 
# returned from REST service.
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

