---
title: Map function
slug: -6Vy-ma
createdAt: Thu Jun 13 2024 08:00:48 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 10 2024 08:58:09 GMT+0000 (Coordinated Universal Time)
---

Use the JSONata map function to sync multiple entities dynamically. When building a solution, the number of entities to sync and the parameters for each are not always known; for example, when syncing the attachments, files, or documents for a message, there can be zero, one, or more. It is necessary to dynamically specify a list of the entities, functions, and function parameters to return from the database using an expression.&#x20;

- The **basic expression **structure is `=$.map(array, function)`.
  - Specify the array you will consult, i.e., a datasource `@ctx.datasources.{datasourceName}`.
  - For the function, specify `($item)`.
  - Example of the basic structure `=$map(@ctx.datasources.{datasourceName}, function($item))`.
- After defining the basic structure, **map out** relevant properties from the array to the relevant `entity`/`function`/`parameters` and specify the dynamic entry using the `$.item` property, e.g., `"calenderId": $.item.id`. This will run through all the records in the datasource and perform a sync-entities action for each record in the table.

```yaml
# Example of dynamic sync-entities expression
actions:
  - children:
      - type: action.sync-entities
        options:
          title: Show events
          provider: DATA_PROVIDER_REST
          entities: | 
            =$map(@ctx.datasources.list-calendars-rest, function($item) {
              $.{
                "entity": "events-from-calendar"
                "function": "get-calendar-event-list"
                "functionParameters": {
                  "accessToken": "jigx.graph.oauth",
                  "calendarId": $item.id
                }
              }
            })[]
```

