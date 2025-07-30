# Delete customer (DELETE)

## Scenario

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Add the ability to delete a customer from the list of customers by swiping left on the customer in the list-item and tapping the *Delete* button.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/uJnmJlrFeH9sjVlhUrpc1_rest-delete.PNG" size="70" position="center" caption="Delete customer" alt="Delete customer" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/uJnmJlrFeH9sjVlhUrpc1_rest-delete.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
:::
::::

### How does this work

A delete function is configured to call the REST APIs DELETE operation and identify the record to delete using the customer Id (CustID). The function is referenced in the `execute-entity` action which will delete the customer from the list and from the datasource via the REST API when the Delete button is pressed.

:::hint{type="info"}
This code sample builds upon the previous [List customers (GET)](<./List customers _GET_.md>) step, to develop a complete and functional solution.
:::

## REST API

| **REST**         | **Detail**                                                 |
| ---------------- | ---------------------------------------------------------- |
| URL              | https\://\[your\_rest\_service]/api/customers?id=\{custId} |
| Operation/Method | DELETE                                                     |

## Function

Specify the REST API url and operation (method), parameters to include authentication in the header and the customer id (custId) to use as the identification of the record to delete.

:::CodeblockTabs
rest-delete-customer.jigx

```yaml
provider: DATA_PROVIDER_REST
# Deletes data from the REST Service.
method: DELETE 
# Use your REST service URL. 
url: https://[your_rest_service]/api/customers?id={custId}
# Direct the function call to use local execution between the device
# and the REST service. 
useLocalCall: true 
format: text

parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution.
    value: service.oauth 
  custId:
    type: int
    location: query
    required: true
```
:::

## Action (global)

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or is in focus on the device.

:::CodeblockTabs
load-data.jigx

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
        function: rest-get-customers
```
:::

## Jig (screen)

- Use a list jig type to configure a list of customers.
- Since the data is already synced to the local Sqlite data provider, the jigs datasource is configured using the local provider with a query to provide the data for use in the list.
- Expressions are used to reference the exact data property required in each component.
- A `swipeable: left` event is configured for the delete with an `execute-entity` action that calls the delete function and uses the custId to identify the record to delete.

:::CodeblockTabs
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
    # Add the swipeable event to the customer - list to include 
    # the delete button.         
    swipeable:
      left:
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
                  # Delete the record from the REST service.
                  function: rest-delete-customer 
                  # Specifiy the function parameters required by the 
                  # function to delete the customer, in this example custId.                 
                  parameters:
                    # id of customer record to be deleted in REST service.  
                    custId: =$number(@ctx.current.item.id)                 
                  data:
                   # id of customer to be deleted from local data provider.  
                    id: =@ctx.current.item.id 
              modal:
                title: Are you sure?
                description: =('Press Confirm to permanently delete ' & @ctx.current.item.companyName)
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
# onFocus is triggered whenever the jig is displayed. The sync-entities 
# action in the global action calls the Jigx REST function and populates
# the local SQLite tables on the device with the data returned from REST 
# service.
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
:::

