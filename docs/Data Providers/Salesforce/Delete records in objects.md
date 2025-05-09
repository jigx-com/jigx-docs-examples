---
title: Delete records in objects
slug: 1UtO-delete
description: Learn how to delete records in a Salesforce object using Salesforce provider's Delete method. Understand the importance of being cautious as deletions are irreversible. Follow our example code snippet to delete a Salesforce Account record, including using
createdAt: Wed Jul 19 2023 12:39:59 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 12:04:01 GMT+0000 (Coordinated Universal Time)
---

Using the Salesforce provider's Delete method, you can delete records in a Salesforce object. This is helpful when a data cleanup is needed due to outdated, incorrect, or irrelevant data. It is essential to exercise caution when deleting records, as the action is irreversible. In Jigx Builder use an `action.confirm` with a `modal` to provide a message before deleting the record permanently. Ensure you have sufficient rights in Salesforce to delete a record in an object.

## Examples and code snippets

:::hint{type="warning"}
Examples are based on test data in a Jigx demo Salesforce environment. Copying the sample code must be adjusted to represent your own Salesforce environment.
:::

### Delete a Salesforce Account record

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/K-RyjjKQLQvbYp16EUENW_salesforcedelete.PNG" size="70" position="center" caption="Deleting records " alt="Deleting records "}
:::

:::VerticalSplitItem
This example uses a list jig type with a `component.list-item` with a `rightElement: button` to execute the Salesforce provider's `method: delete`.
:::
::::

:::CodeblockTabs
salesforce-delete-account.jigx

```yaml
title: Delete Account
description: Delete a Salesforce account
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1600881217197-068e1d79ffb8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2232&q=80

onFocus:
  type: action.action-list
  options:
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_SALESFORCE
          entities:
            - Account

datasources:
  salesforce-accounts: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: Account
      query: SELECT id, '$.Name', '$.Type', '$.BillingCountry' FROM [Account] 
       
    
data: =@ctx.datasources.salesforce-accounts
item:
  type: component.list-item
  instanceId: =@ctx.current.item.id
  options:
    title: =@ctx.current.item.Name
    rightElement: 
      element: button
      title: Delete

      onPress: 
        type: action.action-list
        options:
          isSequential: true
          actions:
            - type: action.confirm
              options:
                isConfirmedAutomatically: false
                onConfirmed: 
                  type: action.execute-entity
                  options:
                    provider: DATA_PROVIDER_SALESFORCE
                    entity: Account
                    method: delete
                    data:
                      id: =@ctx.current.item.id
                    onSuccess: 
                      title: Account deleted
                  
                modal:
                  title: Are you sure you want to delete the Account?
            - type: action.go-back            
```
:::

