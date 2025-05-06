---
title: Get To-do lists & tasks
slug: yQLe-get-t
createdAt: Thu May 02 2024 16:42:09 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 18:00:17 GMT+0000 (Coordinated Universal Time)
---

## Scenario

Get a list of To-do tasks for a user in Microsoft Graph using a GET REST function and display the tasks in a list jig.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
**Resource links:**&#x20;

- <a href="https://learn.microsoft.com/en-us/graph/api/todotasklist-list-tasks?view=graph-rest-1.0&tabs=http" target="_blank">List tasks</a> - MS Graph documentation&#x20;
- <a href="https://developer.microsoft.com/en-us/graph/graph-explorer" target="_blank">Graph Explorer</a>
- [Configuring OAuth for MS Graph]()&#x20;

**Required OAuth scope **(least to most privilege):

Tasks.Read
Tasks.ReadWrite
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UXO3cJBGL2oEzsbc3jTlu_graph-tasks.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UXO3cJBGL2oEzsbc3jTlu_graph-tasks.png" size="70" width="1240" height="2500" position="center" caption="Task list" alt="Task list"}
:::
::::

## Examples and code snippets

:::hint{type="success"}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator" target="_blank">GitHub</a>.
:::

## General

:::CodeblockTabs
index.jigx

```yaml
name: ms-graph-demonstrator
title: MS Graph Demonstrator
description: A sample solution that uses the Microsoft Graph API. You can deploy and use this solution without any additional configuration.
category: business
widgets:
  - size: 2x2 # choose size of the widget on the home hub
    jigId: view-user-jigx
  - size: "2x2"
    jigId: calendar-summary
  - size: "4x2"
    jigId: next-meeting
    when: |
      =@ctx.datasources.next-meeting=null? false:true 
  - size: "2x2"
    jigId: list-email-messages
  - size: "2x2"
    jigId: list-task-lists
  - size: "4x2"
    jigId: items-trending

onFocus: 
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: user-profile
              function: get-user-profile
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: profile-picture
              function: get-profile-picture
              functionParameters:
                accessToken: microsoft.OAuth 
                userId: =@ctx.user.email
            - entity: user-emails
              function: get-user-emails-addresses
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: items-trending
              function: get-items-trending
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: next-week-calendar-events
              function: get-calendar-events-next-week
              functionParameters:
                accessToken: microsoft.OAuth
                startdatetime: =$fromMillis($millis())
                enddatetime: =$fromMillis($millis()+604800000)
            - entity: calendars
              function: get-calendar-list
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: todo-task-lists
              function: get-task-lists
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: email-messages
              function: get-email-messages
              functionParameters:
                accessToken: microsoft.OAuth
                $filter: ="receivedDateTime ge " & $fromMillis($millis()-432000000)
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: todo-tasks
              function: get-all-todo-tasks
              functionParameters:
                accessToken: microsoft.OAuth
                taskListIds: |
                  ={
                    "requests": $map(@ctx.datasources.task-lists.id, function($v, $i, $a) {
                      {
                        "id": $string($i + 1),
                        "method": "GET",
                        "url": "me/todo/lists/" & $v & "/tasks?$top100",
                        "dependsOn": $i>0? [$string($i)]
                      }
                    })
                  }

onRefresh: 
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: todo-task-lists
              function: get-task-lists
              functionParameters:
                accessToken: microsoft.OAuth
            
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: todo-tasks
              function: get-all-todo-tasks
              functionParameters:
                accessToken: microsoft.OAuth
                taskListIds: |
                  ={
                    "requests": $map(@ctx.datasources.task-lists.id, function($v, $i, $a) {
                      {
                        "id": $string($i + 1),
                        "method": "GET",
                        "url": "me/todo/lists/" & $v & "/tasks?$top100",
                        "dependsOn": $i>0? [$string($i)]
                      }
                    })
                  }
          
```
:::

## Functions

MS Graph list To-do tasks function in <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator/functions/tasks" target="_blank">GitHub</a>.

:::CodeblockTabs
get-all-todo-tasks.jigx

```yaml
provider: DATA_PROVIDER_REST
method: POST
url: https://graph.microsoft.com/v1.0/$batch
inputTransform: taskListIds
outputTransform: |
  $.responses.$map($, function($v, $i, $a) {
      $v[$i].body.value.$merge([$,{ "toDoListId": $decodeUrlComponent($v.body."@odata.context".$substringAfter("lists('").$substringBefore("')/tasks")) }])
  })
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth  #Use manage.jigx.com to define credentials for your solution
  Content-Type: 
    type: string
    location: header
    required: false
    value: "application/json"
  taskListIds:
    type: string
    location: body
    required: true
errorTransform: |
  {
    "error": "No lists"
  }
```

get-task-lists.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me/todo/lists
outputTransform: $
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth #Use manage.jigx.com to define credentials for your solution
  $top:
    type: string
    location: query
    required: false
    value: 100
records: =$.value
continuation:
  when: =$."@odata.nextLink"
  url: =$."@odata.nextLink"
  parameters:
    accessToken:
      location: header
      required: true
      type: string
      value: microsoft.OAuth 
errorTransform: |
  {
    "error": "No lists"
  }
```
:::

## Jigs

MS Graph list To-do tasks jig in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/tasks/list-task-lists.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
list-task-lists.jigx

```yaml
title: Task Lists
type: jig.list
icon: contact

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.windowslatest.com/wp-content/uploads/2018/12/Office-apps-new-icons.jpg

onRefresh:
  type: action.action-list
  options:
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: todo-task-lists
              function: get-task-lists
              functionParameters:
                accessToken: microsoft.OAuth

datasources:
  mydata: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: todo-task-lists
        - entity: todo-tasks
      query: SELECT json_extract(tlists.Data, '$.id') as tlId, json_extract(tlists.Data, '$.displayName') as tlDisplayName,
        json_extract(tlists.Data, '$.isOwner') as isOwner, count(json_extract(tasks.Data, '$.id')) AS task_count
        FROM [todo-task-lists] tlists
        LEFT JOIN [todo-tasks] tasks ON json_extract(tlists.Data, '$.id') = json_extract(tasks.Data, '$.toDoListId')
        Group by json_extract(tlists.Data, '$.id'),json_extract(tlists.Data, '$.displayName')
        order by task_count desc

data: =@ctx.datasources.mydata
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.tlDisplayName
    leftElement: 
      element: icon
      icon: task-list
    divider: solid
    rightElement: 
      element: icon
      icon: arrow-right
    subtitle: |
      =@ctx.current.item.isOwner? "Owner of the list: Yes":"Owner of the list: No"
    label:
      title: |
        =@ctx.current.item.task_count
    
widgets:
  toDo: 
    type: widget.list
    options:
      data: =@ctx.datasources.mydata
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.tlDisplayName
          leftElement: 
            element: icon
            icon: task-list
          divider: solid
          subtitle: |
            ="Number of Tasks: " & @ctx.current.item.task_count
          
```
:::

##

