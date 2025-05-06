---
title: Save & update records in objects
slug: 7Wlr-save-or-update-an
description: Learn how to easily update records in Salesforce from your mobile device using the *Save* or *Update* methods. This comprehensive guide includes examples and code snippets on editing the amount field and utilizing the Salesforce Provider's *save* method t
createdAt: Wed Jul 19 2023 12:41:59 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 15:04:19 GMT+0000 (Coordinated Universal Time)
---

There is always a need to ensure records are kept up to date and have the latest contact details, sales figures, or case details. The Salesforce *Save* or *Update* methods allow you to update records in Salesforce directly from your mobile device.&#x20;

## Examples and code snippets

:::hint{type="warning"}
Examples are based on test data in a Jigx demo Salesforce environment. Copying the sample code must be adjusted to represent your own Salesforce environment.&#x20;
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hgBabHVNXORk0caznrtB5_sf-oppsave.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hgBabHVNXORk0caznrtB5_sf-oppsave.PNG" size="70" width="1240" height="2500" position="center" caption="Update opportunity amount" alt="Update opportunity amount"}
:::

:::VerticalSplitItem
This example shows how to update a Salesforce Opportunity record. From the list of opportunities using the `onPress` action the jig opens a form showing the opportunity name and amount. Edit the amount field. Using the Salesforce Providers `save` method the opportunity is updated.&#x20;


:::
::::

:::CodeblockTabs
Salesforce-opp-update.jigx

```yaml
title: Opportunity Update
description: Update the opportunity Amount
type: jig.default

header:
  type: component.jig-header
  options:
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1509228627152-72ae9ae6848d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80   
    height: medium
  
datasources:
  opp-amount:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: Opportunity
      query: SELECT id, '$.Name', '$.Amount' FROM [Opportunity] WHERE id = @id
      queryParameters:
        id: =@ctx.jig.inputs.id
    
children:
  - type: component.form
    instanceId: opp-form
    options:
      children:              
        - type: component.text-field
          instanceId: id
          options:
            initialValue: =@ctx.jig.inputs.id
            isHidden: true
            label: id   
        - type: component.text-field
          instanceId: Name
          options:
            label: Opportunity Name
            initialValue: =@ctx.datasources.opp-amount.Name
        - type: component.number-field
          instanceId: Amount
          options:
            label: Amount 
            initialValue: =@ctx.datasources.opp-amount.Amount
       
actions:
  - children:
      - type: action.submit-form
        options:
          title: Update Amount
          provider: DATA_PROVIDER_SALESFORCE
          entity: Opportunity
          formId: opp-form
          method: save
          data:
            id: =@ctx.components.id.state.value
            Amount: =@ctx.components.Amount.state.value
          onSuccess: 
            type: action.go-back  
```

salesforce-opp-list.jigx

```yaml
title: List Salesforce opportunities
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80

onFocus:
  type: action.action-list
  options:
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_SALESFORCE
          entities:
            - entity: Opportunity

datasources:
  salesforce-opp-list: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: Opportunity
      query: SELECT id, '$.Name', '$.Amount' FROM [Opportunity]
                 
children:
  - type: component.list
    instanceId: account-list
    options:
      data: =@ctx.datasources.salesforce-opp-list
      
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.Name
          leftElement:
            element: avatar
            text: SF
          rightElement: 
            element: value
            text:
              format:
                currency: USD
                numberStyle: currency
              text: =@ctx.current.item.Amount
          onPress: 
            type: action.go-to
            options:
              linkTo: salesforce-opp-update
              inputs:
                id: =@ctx.current.item.id
                entity: Opportunity
```
:::

