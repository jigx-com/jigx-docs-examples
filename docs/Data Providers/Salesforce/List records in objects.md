---
title: List records in objects
slug: Cg0q-list
createdAt: Wed Jul 19 2023 12:39:56 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 15:03:54 GMT+0000 (Coordinated Universal Time)
---

# List records in objects

Reading data from Salesforce using the Salesforce provider is easy. The provider is intuitive, and once you have synced the data from the Salesforce provider to the local data provider, you can design lists, charts, and widgets to show your organization's Salesforce metrics, accounts, opportunities, and more.

### Examples and code snippets

{% hint style="warning" %}
Examples are based on test data in a Jigx demo Salesforce environment. Copying the sample code must be adjusted to represent your own Salesforce environment.
{% endhint %}

#### List of accounts

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A8Tn9KF-RKvhmVl9o\_CxX\_salesforce-list.PNG" size="70" position="center" caption="Search and filtering a list" alt="Search and filtering a list"}
{% endcolumn %}

{% column %}
The code below shows a simple example of a list of accounts in Salesforce. Adding `search` and `filter` properties allows you to easily find the accounts you looking for.
{% endcolumn %}
{% endcolumns %}

:::CodeblockTabs&#x20;

```yaml
title: List Salesforce accounts
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1605152276897-4f618f831968?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2670&q=80


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
      query: SELECT id, '$.Name', '$.Type', '$.BillingCountry' FROM [Account] WHERE ('$.Type' LIKE @filter OR @filter IS NULL) AND ('$.Name' LIKE '%'||@search||'%' OR @search IS NULL)
      queryParameters:
       filter: =@ctx.components.account-list.state.filter
       search: =@ctx.components.account-list.state.searchText
       
children:
  - type: component.list
    instanceId: account-list
    options:
      data: =@ctx.datasources.salesforce-accounts
      isSearchable: true
      maximumItemsToRender: 50
      filter: 
        - title: All
          value: ""
        - title: Prospect
          value: Prospect
        - title: Customer - Direct
          value: Customer - Direct
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.Name
          subtitle: =@ctx.current.item.BillingCountry
          label:
            title: =@ctx.current.item.Type
          leftElement:
            element: avatar
            text: SF
        
```

#### List of Opportunities

{% columns %}
{% column %}
The code below shows a basic example of a list of opportunites in Salesforce with an `onPress` action that will allow you to update the opportunity amount.
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/i3TJ4x\_PLLgmihe9nnqgS\_sf-opplist.PNG" size="70" position="center" caption="Basic List" alt="Basic List"}
{% endcolumn %}
{% endcolumns %}

{% code title="list.jigx" %}
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
            - Opportunity

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
{% endcode %}

#### Create a Stage detail jig

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FGcAzSsO51PuV3Di4atbl\_stagedetail.PNG" size="70" position="center"}
{% endcolumn %}

{% column %}
Below is an example of reading data from the _Account_, _Opportunity_, and _OpportunityStage_ objects in Salesforce. Combining the data, using a `jig.list` with `component.list-item` and `component.summary` to create the Stage Detail jig.
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="stage-detail.jigx" %}
```yaml
title: Stage detail
type: jig.list
icon: house

header:
  type: component.jig-header
  options:
    children:
      options:
        source:
          uri: https://images.unsplash.com/photo-1555421689-491a97ff2040?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80
      type: component.image
    height: medium
    
onFocus:
  type: action.action-list
  options:
    actions:
      -  type: action.sync-entities
         options:
          provider: DATA_PROVIDER_SALESFORCE
          entities:
            - Account
            - Opportunity
            - OpportunityStage
                   
datasources:
   account-data:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: Account
      query: |
        SELECT Acc.id as accid
          ,json_extract(Acc.data, '$.Name') as Name
          ,json_extract(Opp.data, '$.AccountId') as AccountId
          ,sum(json_extract(Opp.data, '$.Amount')) as OppValue
          FROM [Account] Acc 
          LEFT JOIN [Opportunity] Opp
          on AccountId = accid
                 
   stage-data:
      type: datasource.sqlite
      options:
        provider: DATA_PROVIDER_LOCAL
        entities:
          - Opportunity
          - OpportunityStage
        query: SELECT opp.id as oppid ,json_extract(opp.data, '$.StageName') as x
          ,sum(json_extract(opp.data, '$.Amount')) as y ,json_extract(opp.data,
          '$.CloseDate') as CloseDate ,json_extract(opp.data, '$.AccountId') as
          oppaccid ,json_extract(OppStg.data, '$.ApiName') as ApiName
          ,json_extract(OppStg.data, '$.SortOrder') as SortOrder FROM
          [Opportunity] opp LEFT JOIN [OpportunityStage] OppStg on x = ApiName
          where CloseDate between '2020-01-01' and '2020-03-31' group by x order
          by SortOrder

data: =@ctx.datasources.stage-data
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.x
    rightElement:
      element: value
      text:
        format:
          currency: USD
          numberStyle: currency
        text: =@ctx.current.item.y
      
summary:
  children:
    type: component.summary
    options:
      title: >
        ='Total: $' & $formatNumber(@ctx.datasources.total-sales.totalsales ,
        '#,###.00')
      subtitle: Quarter sales to date
      layout: default
      leftIcon:
        element: icon
        name: currency-dollar-circle
```
{% endtab %}

{% tab title="total-sales.jigx" %}
```yaml
# datasources>total-sales.jigx
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_LOCAL

  entities:
    - entity: Opportunity
  query: >
    select id , sum(json_extract(data , '$.Amount')) as totalsales from Opportunity

    where 

    json_extract(data, '$.StageName') = 'Closed Won'

    and json_extract(data, '$.CloseDate') between '2020-01-01' and '2020-03-31'
```
{% endtab %}
{% endtabs %}
