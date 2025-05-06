---
title: jig.composite
slug: MPHU-jigcomposite
description: This document provides detailed information on configuring and using a composite jig, which is a combination of multiple jigs. It includes examples and code snippets for setting up a composite jig without any input and demonstrates the use of a YAML code 
createdAt: Wed Jun 08 2022 06:31:09 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 10:38:35 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The composite jig is a jig made up of several parts or elements. In this case, a jig is made up of several jigs. This jig allows you to display multiple jigs on one list where you would otherwise be unable to combine the functionality in the same way.&#x20;
:::

:::VerticalSplitItem
::Image[]{alt="Jig Composite Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7guWK3dQZ_xkWBnn-yCDc_composite.png" size="90" width="1570" height="1954" caption="Jig Composite Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7guWK3dQZ_xkWBnn-yCDc_composite.png"}
:::
::::

## ****Configuration options

Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

| **Core Structure** |                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| `jigId`            | The core structure includes: `jigId` 2x or more (depends on how many jigs you are connecting). |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | The icon will be displayed on the [widget]() of this jig. Start typing the name of the icon to invoke the available list in IntelliSene. See [Jigx icons]() for information on worknig with icons.                                                                                                                                                                                                 |
| `inputs`          | If you are setting up a `jig.composite` where jigs rely on input to display or otherwise interact with very specific data, you'll need to use `inputs`. Here you set the data you would like to transfer to the composite jig. There are 2 options to make data available for input:<br />1) Set them in `output` inside the jig .
2) Set them as a `global` variable by using `set-state action`. |
| `isTitleHidden`   | The boolean value allows you to hide the title of your jig in the composite jig. Even if the jig's title is set to `true` , because the title is a mandatory property.                                                                                                                                                                                                                             |
| `when`            | The ability to include or exclude a jig for display on a composite jig. If set to `true` the jig is included, if set to `false` the jig will not appear on the composite jig. Dynamically set this property by using expressions.                                                                                                                                                                  |

## Considerations

- When calling a jig in a composite jig for example, `jigId: personal-details`, you can add an `instanceId` on the composite jig. This allows you to interact with the referenced jig, such as saving or calling a control on the referenced jig.   If no `instanceId` exists, IntelliSense cannot show it in the composite jig configuration.&#x20;

:::CodeblockTabs
composite.jigx

```yaml
children:
  - jigId: personal-details
    instanceId: personalDetails
    inputs:
      inputName: My details
  - jigId: work-details
    instanceId: workDetails
  - jigId: employee-details
    instanceId: hrInfo
    
actions:
  - children:
      # you can choose an action to save the data as an object
      - type: action.execute-entity
        options: 
          title: Create my details
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/personal
          method: create
          data: =@ctx.jigs.personalDetails.components.my-details.state.data

     # or

      # you can choose an action to save individual fields    
      - type: action.execute-entity
        options: 
          title: Create my work details
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/work
          method: create
          data: 
            employee-position: =@ctx.jigs.workDetails.components.work-position.state.value
            employee-startWork: =@ctx.jigs.workDetails.components.work-startWork.state.value
                  
      # or

      # you can choose an action to save individual fields from Multiple jigs  
      - type: action.execute-entity
        options: 
          title: Create Employee details
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/employees
          method: create
          data: 
            id: =@ctx.jigs.hrInfo.components.employee-id.state.value
            employee-first-name: =@ctx.jigs.personalDetails.components.my-first-name.state.value   
            employee-surname: =@ctx.jigs.personalDetails.components.my-surname.state.value
            employee-position: =@ctx.jigs.workDetails.components.work-position.state.value
            employee-contract: =@ctx.jigs.hrInfo.components.employee-contract.state.value  
```
:::

## Examples and code snippets 

:::hint{type="success"}
The code below is an extract from the full *jigx-samples* solution. The code snippets describe the component discussed in this section. For the solution to function in the Jigx app download the full *jigx-samples* project from <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples" target="_blank">GitHub,</a> and follow the instructions in [Setting up your solution](docId:1gfew7GRPvkfxon-TsymP).
:::

:::::ExpandableHeading
### Composite Jig without any form of input

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Composite jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CdvFnDVAGN7W5UQc00w_N_brj8ppzfa99c5cmqx-wsucomposite-withoutiphone13blueportrait.png "Composite jig")
:::

:::VerticalSplitItem
This example shows the simplest way in which a `Composite Jig` can be set up - referencing two separate jigs and displaying them on one without having to filter the content.&#x20;

**Examples:**

See the compsite jig code example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-composite/jig-composite.jigx" target="_blank">GitHub</a>.
See the <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/location/static-data/location-with-address.jigx" target="_blank">location</a> code and <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/static-data/country-list-sd.jigx" target="_blank">country list </a>code examples in GitHub.
See the static country datasource code example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/country-data-static.jigx" target="_blank">GitHub</a>.
See the index.jigx code below to add the jig to the Home Hub.


:::
::::

:::CodeblockTabs
composite-jig.jigx

```yaml
#This file is added under the jig folder
title: Composite Jig
description: Composite Jig without input
type: jig.composite

children:
  - jigId: location-with-address
  - jigId: country-list-sd
```

location-with-address.jigx

```yaml
title: Location with address
type: jig.default

isCollapsible: true

datasources:
  address: 
    type: datasource.static
    options:
      data:
        - street: 768 5th Ave
          city: New York
          country: US

children:
  - type: component.location
    options:
      address: =@ctx.datasources.address.street & ',' & @ctx.datasources.address.city & ',' & @ctx.datasources.address.country
      zoomLevel: 9
```

country-list-sd.jigx

```yaml
title: Country List
description: List of countries and their flags
type: jig.list
icon: world

data: =@ctx.datasources.country-data-static
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.title
    subtitle: =@ctx.current.item.value
    leftElement: 
      element: icon
      name: =@ctx.current.item.icon
```

datasources

```yaml
datasources:
  country-data-static:
    type: datasource.static
    options:
      data:
      - title: Afghanistan
        value: AF
        icon: af
        iconType: flag
      - title: Albania
        value: AL
        icon: al
        iconType: flag
      - title: Algeria
        value: DZ
        icon: dz
        iconType: flag
      - title: American Samoa
        value: AS
        icon: as
        iconType: flag
      - title: Andorra
        value: AD
        icon: ad
        iconType: flag
      - title: Angola
        value: AO
        icon: ao
        iconType: flag
      - title: Anguilla
        value: AI
        icon: ai
        iconType: flag
      - title: Antigua And Barbuda
        value: AG
        icon: ag
        iconType: flag
      - title: Argentina
        value: AR
        icon: ar
        iconType: flag
      - title: Armenia
        value: AM
        icon: am
        iconType: flag
      - title: Aruba
        value: AW
        icon: aw
        iconType: flag
      - title: Australia
        value: AU
        icon: au
        iconType: flag
      - title: Austria
        value: AT
        icon: at
        iconType: flag
      - title: Azerbaijan
        value: AZ
        icon: az
        iconType: flag
      - title: Bahamas
        value: BS
        icon: ar
        iconType: flag
      - title: Bahrain
        value: BH
        icon: bh
        iconType: flag
      - title: Bangladesh
        value: BD
        icon: bd
        iconType: flag
      - title: Barbados
        value: BB
        icon: bb
        iconType: flag
      - title: Belarus
        value: BY
        icon: by
        iconType: flag
      - title: Belgium
        value: BE
        icon: be
        iconType: flag
```

index.jigx

```yaml
name: location
title: location with country list
category: personal
tabs:
  home:
    jigId: composite-jig
    icon: home-apps-logo
```
:::
:::::

:::::ExpandableHeading
### Composite Jig with input

This example shows how a Composite jig can be used to only display certain data based on the input received.

::::VerticalSplit{layout}
:::VerticalSplitItem
![Composite jig with input](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/11o2jArG-3bPKeQT7w0pi_comiphone13blueportrait.png "Composite jig with input")
:::

:::VerticalSplitItem
![Composite jig with input](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8ycT7LBXUDhtkDoz8pdUc_compiphone13blueportrait.png "Composite jig with input")
:::
::::

**Examples:**
See the full composite jig input code example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-composite/inputs/service-details-comp.jigx" target="_blank">GitHub</a>.
See the folder with supporting files in <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-composite/inputs/supporting-files" target="_blank">GitHub</a>.
See the datasource code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx" target="_blank">GitHub</a>.&#x20;

See the default.jigx code snippet with the database table defined below.

:::hint{type="success"}
Using the code below requires data in the database, the jigx.sample solution has the data provided for cleaning -services. You can use the cleaning-services.csv file in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/csv/cleaning-services.csv" target="_blank">GitHub</a> and upload it via the [Data]() configuration in Jigx Management.
:::

:::CodeblockTabs
service-details-comp.jigx

```yaml
type: jig.composite
title: Cleaning Services

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1512314889357-e157c22f938d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8aW5mb3JtYXRpb258ZW58MHx8MHx8&auto=format&fit=crop&w=900&q=60

children:
  - jigId: cleaning-serv-horizon-list-dd
    instanceId: cleaning
# Instance Id is required for a composite jig exposing outputs
# To be accessed by another jig 
    
  - jigId: service-details
    instanceId: service_deets
# Add inputs to receive the outputs-keys, reference the instanceId
# Which renders the selected data    
    inputs:
      id: =@ctx.jigs.cleaning.outputs.output-key
```

cleaning-serv-horizon-list-dd.jigx

```yaml
title: List of available services

type: jig.list
icon: contact 
isHorizontal: true
isCollapsible: false
isInitiallyCollapsed: true
hasActiveItem: true
isSelectable: true

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1628177142898-93e36e4e3a50?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80

outputs:
  output-key: =@ctx.solution.state.servicesId
  
data: =@ctx.datasources.cleaning-services-dynamic
item:
  
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.description
    horizontalItemSize: large
    
    progress: =@ctx.current.item.id = @ctx.solution.state.servicesId ? 1 :0
    color:
      - when: =@ctx.current.item.id = @ctx.solution.state.servicesId ? true :false
        color: color2
    leftElement: 
      element: image
      text: ''
      uri: =@ctx.current.item.image
    label:
      title: =@ctx.current.item.time & ' minutes'
    rightElement:
      element: value
      text: =(@ctx.current.item.hourlyrate) != 'NA' ? '$ ' & $number(@ctx.current.item.hourlyrate) & ' p/hr':'$ ' & $number(@ctx.current.item.onceoffrate) & ' once off'
    onPress: 
      type: action.action-list
      options:
        actions:
 # set the solution state and the value as id of the current selected item       
          - type: action.set-state
            options:
              state: =@ctx.solution.state.servicesId
              value: =@ctx.current.item.id
```

service-details.jigx

```yaml
title: =@ctx.datasources.cleaningServices.service != null ? "Service details":" "
type: jig.default
placeholders:
  - title: Please choose a service
    when: =@ctx.datasources.cleaningServices.service != null ? false:true
    icon: loading-data
      
datasources:
  cleaningServices:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - entity: default/cleaning-services
      queryParameters:
        servId: =@ctx.solution.state.servicesId
  
      query: | 
        SELECT 
          id,
          '$.area', 
          '$.description',
          '$.hourlyrate',
          '$.illustratuion',
          '$.image',
          '$.indoor',
          '$.onceoffrate',
          '$.service',
          '$.time' 
        FROM [default/cleaning-services] WHERE id = @servId

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: =@ctx.datasources.cleaningServices.image

children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaningServices.service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaningServices.area
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaningServices.time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaningServices.indoor
                  contentType: checkbox
        - type: component.entity-field
          options:
            label: Description
            value: =@ctx.datasources.cleaningServices.description
            isMultiline: true
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =(@ctx.datasources.cleaningServices.hourlyrate) != 'NA' ? '$ ' & $number(@ctx.datasources.cleaningServices.hourlyrate):'NA'
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: ='$ ' & $number(@ctx.datasources.cleaningServices.onceoffrate)
                  isHidden: =(@ctx.datasources.cleaningServices.onceoffrate) = null ? true:false
```

datasources

```yaml
datasources:
  cleaning-services-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services
      query: |
        SELECT 
          id, 
          '$.id' as sqlid, 
          '$.area', 
          '$.description', 
          '$.hourlyrate', 
          '$.illustration', 
          '$.image', 
          '$.indoor', 
          '$.onceoffrate', 
          '$.service', 
          '$.pressed', 
          '$.time',
          '$.quantity'
        FROM [default/cleaning-services] WHERE '$.hourlyrate' IS NOT NULL ORDER BY id DESC
```

default.jigx

```yaml
databaseId: default
tables:
  cleaning-services: null  
```

index.jigx

```yaml
name: cleaning-service
title: cleaning service
category: personal
tabs:
  home:
    jigId: service-details-comp
    icon: home-apps-logo
```
:::
:::::

## See also** **

- [Jigs (screens)]()
- <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-composite" target="_blank">Related examples (Github)</a>

