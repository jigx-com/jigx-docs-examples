---
title: execute-entity
slug: jGWl-execute-entity
description: Learn how to use the "execute-entity" action to save, update, or delete data from your database. This document provides code snippets and examples for using execute-entity in various scenarios such as action buttons, lists, and events. Discover the syntax
createdAt: Thu Jun 09 2022 18:22:55 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Nov 04 2024 15:41:43 GMT+0000 (Coordinated Universal Time)
---

Execute-entity can save, update, or delete data in a **single row** from a database, depending on the chosen method. Each datasource type (Dynamic / SQL / REST) will have a different syntax for updating, saving, and deleting data.

For the Dynamic datasource, values will be saved under the _data_ option.
For SQL/REST datasource, values will be saved under the _functionParameters_ option.

:::hint{type="warning"}
This action can't be used if you are using [Static Data](https://docs.jigx.com/examples/static).
:::

## Configuration options

An `execute-entity` action can be used in multiple areas:

1. Under the action button
2. In action list
3. In onPress/onChange events (if the component you are setting up has these options)
4. In onRefresh/onFocus

:::hint{type="warning"}
The execute-entity has a `go-back` option, which is set to on by default. That means when you run execute-entity, it will automatically return you to the previous jig.
:::

## Offline remote data handling

Dealing with offline remote data is fundamental to ensuring data synchronization and consistency between the mobile app and the remote data source, allowing users to continue using the app and performing actions without interruption. [Offline remote data handling](https://docs.jigx.com/offline-remote-data-handling) explains how to configure solutions to deal with data when the device is offline using the `queueOperations` property available in execute-entities and provides examples and code samples.

## Examples and code snippets

:::::ExpandableHeading

### Execute-entity in action

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FNJS6iz-l7FhJtP82_Kae_ex-actioniphone13blueportrait.png" size="80" position="center" caption="Execute enitity" alt="Execute entity"}
:::

:::VerticalSplitItem
In this example, execute entity is used in _action_ with the _create_ method. This example results in creating a new record with the First name, Last name, Email, and Phone number information. Execute entity is called by the press of the _Save details_ button on the bottom.

**Example:**
See the full example of execute-entity in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-action.jigx).
:::
::::

:::CodeblockTabs
execute-entity-action

```yaml
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Save details
          provider: DATA_PROVIDER_DYNAMIC
          method: create
          entity: default/form
          data:
            firstname: =@ctx.datasources.employee-detail-dynamic.firstname
            lastname: =@ctx.datasources.employee-detail-dynamic.lastname
            email: =@ctx.datasources.employee-detail-dynamic.email
            phone: =@ctx.datasources.employee-detail-dynamic.phone
          onSuccess:
            type: action.go-back
```

:::
:::::

:::::ExpandableHeading

### Execute-entity in action list

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZEf_uXB3562SxaHxxh_ae_ex-a-listiphone13blueportrait.png" size="82" position="center" caption="Execute entity in action-list" alt="Execute entity in action-list"}
:::

:::VerticalSplitItem
By pressing the _Save details_ button the execute-entity action will be followed by the go-to action.

**Examples:**
See the full example of execute-entity in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-actionlist.jigx).
:::
::::

:::CodeblockTabs
execute-entity-action-list

```yaml
actions:
  - children:
      - type: action.action-list
        options:
          isSequential: true
          title: Save details
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                method: create
                entity: default/form
                data:
                  firstname: =@ctx.datasources.employee-detail-dynamic.firstname
                  lastname: =@ctx.datasources.employee-detail-dynamic.lastname
                  email: =@ctx.datasources.employee-detail-dynamic.email
                  phone: =@ctx.datasources.employee-detail-dynamic.phone
            - type: action.info-modal
              options:
                modal:
                  title: Details successfully saved
                  buttonText: View list
                  element:
                    type: icon
                    icon: cog-approved
                    color: primary
                onConfirmed:
                  type: action.go-to
                  options:
                    linkTo: ja-execute-entity-onPress
```

:::
:::::

:::::ExpandableHeading

### Execute-entity in onPress/onChange event

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fHcCpIywUK-qDL8nRfoO3_tjvfgtwpkgot3fa73lrbex-onchangeiphone13blueportrait.png" size="80" position="center" caption="Execute-entity in onPress" }
:::

:::VerticalSplitItem
Here is the example of execute-entity in onPress/onChange event in list-item.

**Examples:**
See the full example using onChange in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-onChange.jigx).
See the full example using onPress you in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-onPress.jigx).
:::
::::

:::CodeblockTabs
onPress

```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstname
    subtitle: =@ctx.current.item.lastname
    description: =(@ctx.current.item.modify = 0 ? 0 :@ctx.current.item.modify) & ' time/s changed.'
    leftElement:
      element: avatar
      text: ""
      uri: =@ctx.current.item.photo
    onPress:
      type: action.execute-entity
      options:
        provider: DATA_PROVIDER_LOCAL
        method: update
        entity: default/employees
        data:
          id: =@ctx.current.item.id
          modify: =($number(@ctx.current.item.modify) + 1)
```

onChange

```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstname
    subtitle: =@ctx.current.item.lastname
    description: =(@ctx.current.item.modify = 0 ? 0 :@ctx.current.item.modify) & ' time/s changed.'
    leftElement:
      element: avatar
      text: ""
      uri: =@ctx.current.item.photo
    rightElement:
      element: checkbox
      value: true
      onChange:
        type: action.execute-entity
        options:
          provider: DATA_PROVIDER_LOCAL
          method: update
          entity: default/employees
          data:
            id: =@ctx.current.item.id
            modify: =$number(@ctx.current.item.modify) + 1
```

:::
:::::

::::ExpandableHeading

### Execute-entity in onRefresh/onFocus

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ODgGFijGrBYtf6_qv57VK_actioneentityrefresh.PNG" size="80" position="center" caption="Execute entity" alt="Execute entity"}

Here is the example of execute-entity in onRefresh/onFocus.

See the full example using onRefresh in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-onRefresh.jigx).
See the full example using onFocus in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/ja-execute-entity/ja-execute-entity-onFocus.jigx)

:::CodeblockTabs
execute-entity-onRefresh

```yaml
onRefresh:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    method: update
    entity: default/employees
    data:
      id: =@ctx.datasources.employee-detail-dynamic.id
      modify: =@ctx.datasources.employee-detail-dynamic.modify >= 10 ? 1 :($number(@ctx.datasources.employee-detail-dynamic.modify) + 1)
```

execute-entity-onFocus

```yaml
onFocus:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    method: update
    entity: default/employees
    data:
      id: =@ctx.datasources.employee-detail-dynamic.id
      modify: =@ctx.datasources.employee-detail-dynamic.modify >= 10 ? 1 :($number(@ctx.datasources.employee-detail-dynamic.modify) + 1)
```

:::
::::

::::ExpandableHeading

### Deleting data using execute-entity

Here is an example of deleting different data using execute-entity. There are always 2 options for how you can delete a record:

1. Using SQL Select
2. Using JSONata function

In the first two examples, you can see the same situation where you are deleting all the records where the name equals Jane.

The third example shows how to delete the first 3 records from your datasource.

:::CodeblockTabs
delete-by-first-name

```yaml
datasource:
  people:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: people
      query: |
        SELECT
          id,
          '$.name',
          '$.surname',
          '$.address'
        FROM [people] WHERE '$.name' LIKE 'Jane'

actions:
  - type: "action.execute-entity"
    options:
      entity: people
      method: delete
      provider: DATA_PROVIDER_DYNAMIC
      data:
        id: =@ctx.datasource.people.id
```

delete-by-fist-name-jsonata-function

```yaml
type: "action.execute-entity"
options:
  goBack: stay
  entity: form
  provider: DATA_PROVIDER_LOCAL
  method: delete
  data: "=@ctx.datasources.people[name = 'Jane']{'id':id}[]"
```

delete-first-3-records

```yaml
datasource:
  people:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/people
      query: |
        SELECT
          id,
          '$.name',
          '$.surname',
          '$.address'
        FROM [default/people] LIMIT 3

actions:
  - type: "action.execute-entity"
    options:
      goBack: stay
      entity: deafult/people
      method: delete
      provider: DATA_PROVIDER_DYNAMIC
      data:
        id: =@ctx.datasource.people.id
```

:::
::::
