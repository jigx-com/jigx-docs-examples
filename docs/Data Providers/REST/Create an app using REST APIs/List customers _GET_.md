---
title: List customers (GET)
slug: 1O2k-get
createdAt: Tue Apr 30 2024 08:30:58 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 12:54:55 GMT+0000 (Coordinated Universal Time)
---

## Scenario

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Create a list of customers showing the company name, contact person's first and last name, status, and an avatar on the left displaying the US state.&#x20;
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/DS3wYOeRqIAtsmqCP6op5_rest-list.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/DS3wYOeRqIAtsmqCP6op5_rest-list.PNG" size="80" width="1240" height="2500" position="center" caption="Customer list" alt="Customer list"}
:::
::::

### How does this work

The REST APIs GET operator is used in a Jigx function with an `outputTransform` to specify the exact data to be returned. In the `outputTransform,` the properties we want to return and use are specified. A global action is configured to sync the data in the app with the REST data provider calling the function. In turn, the global action is called in the index.jigx file to load the data when the app is opened. In the list jig the local data provider is used to configure the list-item component.

## REST API

| **REST**         | **Detail**                                    |
| ---------------- | --------------------------------------------- |
| URL              | https\://\[your\_rest\_service]/api/customers |
| Operation/Method | GET                                           |

## Function

Specify the REST API url and operation (method), parameters to include authentication in the header and in the `outputTransform` define the data properties to be returned. The customer logo is stored in the REST service in base64, Jigx requires the logo in local-uri format for display. A `conversion` is configured in the function to change the base64 to local-uri.  &#x20;

:::CodeblockTabs
rest-get-customer.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET #Fetches data from the REST Service
url: https://[your_rest_service]/api/customers #Use your REST service URL 
#Return data for rows with matching ids
forRowsWithMatchingIds: true
#Direct the function call to use local execution between the mobile device and the REST service
useLocalCall: true

parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: service.oauth #Use manage.jigx.com to define credentials for your solution
#Define the customer fields that must be fetched from the REST Service
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
#Convert the images returned from the REST service to local-uri which the jig expects to be able to display the image      
conversions:
  - property: logo
    from: base64
    to: local-uri
```
:::

## Action (global)

Create a load-data.jigx file under the actions folder. This file is configured with an action that syncs the data from the REST service, by calling the function, to the local Sqlite table. The action file is referenced in the index.jigx file to load the data when the app is opened or  is in focus on the device.

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
```
:::

## Jig (screen)

- Use a list jig type to configure a list of customers.&#x20;
- Since the data is already synced to the local Sqlite data provider, the jigs datasource is configured with a query to provide the data for use in the list.&#x20;
- Expressions are used to reference the exact data property required in each component.

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
    
tabs:
  home:
    jigId: list-customers
    icon: home-apps-logo
 
```
:::

