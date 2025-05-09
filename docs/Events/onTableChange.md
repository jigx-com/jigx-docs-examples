---
title: onTableChange
slug: 3Ufn-on
createdAt: Wed Mar 12 2025 09:33:33 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 23 2025 07:03:44 GMT+0000 (Coordinated Universal Time)
---

## What it does

This event enables a remote system like Acumatica to call into Jigx and trigger changes on a mobile device by monitoring data updates. It detects changes in specific data tables (entities) and executes the configured actions accordingly. A common use case is ensuring data consistency between the remote system and the app and keeping information updated across the system.

## How it works

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-kY-lpInKQ8HXoX07BLTSA-20250320-085318.png)

**External system data changes**

1. The remote system pushes data changes to the Jigx endpoint.
2. The Jigx endpoint stores and continuously syncs the data to a Dynamic Data table.
3. The `onTableChange` event monitors the Dynamic Data table for updates.
4. When a change is detected, the event triggers an action that updates the mobile app.

**Internal local data changes**

1. When data is saved to a local table on the device, the `onTableChange` event monitors the table for changes.
2. Upon detecting a change, the event triggers the configured action to sync the data with a Dynamic Data or remote table.

## Where and how to configure it

1. Configure [Acumatica Push Notifications](<./onTableChange/Acumatica Push Notifications.md>) to use the [Jigx API endpoint](<./onTableChange/Acumatica Push Notifications.md>).
2. In the Jigx API endpoint configuration, specify a name for the remote system's data table. This is the name given to the Dynamic Data table.
3. In default.jigx, add the Dynamic Data table name.
4. In index.jigx, add the `onTableChange` event property at the root level.
5. Specify the data table the event should monitor for changes—this should match the table defined in the Jigx endpoint and default.jigx.
6. Configure an action (e.g., `action.sync-entities`) to execute when a change is detected.
7. Use IntelliSense to select from the list of available actions.

## Considerations

Key factors to keep in mind when using this event.

- Multiple `onTableChange` events can be configured in the index.jigx file.
- The event continuously listens for data changes on the specified table.
- It can be used with any data provider, including local, REST, SQL, and Dynamic Data.
- The event can listen for changes in one table and respond by updating another table using the `actions` property.
- In the SQL data provider, when using the `functionCall` method, the `onTableChange` event does not execute because the data changes occur directly on the backend and do not affect local data.
- When the app is in the background, and changes occur in backend remote data tables, the `onTableChange` event executes once when the app opens to apply the data changes. This ensures optimal app performance and prevents multiple redundant executions.
- When the app is open and data changes are made, the event executes individually for each detected change.
- Avoid creating a loop in `onTableChange` by checking a table for changes and then modifying the same table.

## Examples and code snippets 

### Single data table

This example demonstrates how to use the `onTableChange` event to monitor data changes in a single table from a remote data system. When a data change occurs on the remote system, the event executes and resets the solutions state.

:::CodeblockTabs
index.jigx

```yaml
title: Global
name: global-inc
category: health

# Add the onTableChange event to listen for changes on a single table.
onTableChanged:
  # Specify the remote table to monitor.
  - table: employees
    action: 
      # Configure the action to execute when a change is detected.
      type: action.reset-solution-state
      options:
        changes:
          - dataStatus                
```

default.jigx

```yaml
databaseId: default
tables:
  employees: null
```
:::

### Multiple data tables

This example demonstrates how to use the `onTableChange` event to monitor data changes across multiple tables and different data providers within the solution. When a data change occurs, the event executes the defined actions for each configured data provider.

In the second table, multiple actions are configured, including `action.sync-entities`, which is dynamically updated by specifying a list of entities, functions, and function parameters using an expression. This is particularly useful when the number of entities to sync and their corresponding parameters are not always known.

:::CodeblockTabs
index.jigx

```yaml
title: Global
name: global-inc
category: health

# Add the onTableChange event to listen for changes in multiple tables.
onTableChanged:
   # Configure the first table to be monitored.
  - table: calendar
    action: 
      # Configure the action to execute when a change is detected.
      type: action.reset-solution-state
      options:
        changes:
          - Status   
  # Configure the second table to be monitored.        
  - table: calendarEvents
    action: 
      # Configure the actions to execute when a change is detected. 
      # Multiple actions can be executed when data changes in the table.
      type: action.action-list
      options:
        isSequential: true
        # First action to sync data dynamically to the REST endpoint.
        actions:  
          - type: action.sync-entities
            options:
              provider: DATA_PROVIDER_REST
              # Add the expression for the dynamic sync-entities in the specified format. 
              # The array uses the full datasource.    
              entities: |
                =$map(@ctx.action.parameters.datasource, function($item) {
                  $.{
                    "entity": "events-from-calendar",
                    "function": "get-calendar-event-list",
                    "functionParameters": {
                      "accessToken": "jigx.graph.oauth",
                      "calendarId": $item.id
                    }
                  }
                })[]
          # Second action to navigate to a specific jig.      
          - type: action.go-to
            options:
              linkTo: event-of-meeting-dynamic
```

default.jigx

```yaml
databaseId: default
tables:
  calendar: null
  calendarEvents: null
```
:::

### Action data changes from one table to another table

In the example below, the `send-notifications` table is monitored for changes. Once notifications are sent, the event executes and updates the `customer` table with the relevant data.

:::CodeblockTabs
index.jigx

```yaml
title: Global
name: global-inc
category: health

# Add the onTableChange event to listen for changes on a single table.
onTableChanged:
  # Specify the table to monitor for changes.
  - table: send-notification
    action: 
      # Configure the action to execute when a change is detected. 
      type: action.execute-entity
      options:
        provider: DATA_PROVIDER_DYNAMIC
        # Specify the table to update, note this is a different table to the table monitored. 
        entity: default/customer
        method: create
        # specify the data that must be updated in the table.
        data:
          notified: 'Yes'
          date: =$now()
```

default.jigx

```yaml
databaseId: default
tables:
  send-notification: null
  customer: null
```
:::

