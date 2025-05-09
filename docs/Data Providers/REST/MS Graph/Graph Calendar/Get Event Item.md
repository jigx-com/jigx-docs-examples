---
title: Get Event Item
slug: e9aK-get-event-item
description: Learn how to retrieve the details of an event item from a user's calendar using Microsoft Graph with this comprehensive document. Explore code examples, configuration details, and REST calls with OAuth authentication. Additionally, discover how to create 
createdAt: Sat Nov 26 2022 20:48:33 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed May 08 2024 14:27:40 GMT+0000 (Coordinated Universal Time)
---

## Scenario

Get the details of an event item in a user's calendar from Microsoft Graph using a GET REST function and showing it in a default jig using an expander, entity-field, and list component.

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
**Resource links:**

- [List Event](https://learn.microsoft.com/en-us/graph/api/user-list-events?view=graph-rest-1.0&tabs=http) - MS Graph documentation
- [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
- [Configuring OAuth for MS Graph]()

**Required OAuth scope** (least to most privilege):

Calendars.Read
Calendars.ReadWrite

**Related Sample**

This example uses [Get Calendar List](<./Get Calendar List.md>) and [Get Event List](<./Get Event List.md>) to provide the calendar id and event id input to the view-calendar-event-details jig.
:::

:::VerticalSplitItem
![Calendar event](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hFXLIgg5zAk0sS-e1-HhJ_graph-eventitem.png "Calendar event")
:::
::::

## Examples and code snippets

:::hint{type="success"}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator).
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

```
:::

## Functions

:::hint{type="info"}
We will use `forRowsWithValues` in the get-calendar-event-details function to update only one record in the calendarEvents table when called from `onRefresh` on the view-calendar-event-details jig. If you dont specify `forRowsWithValues` the entire table is wiped by the REST call and only the result is inserted. See [REST Overview]() for more information on using `forRowsWithValues` with REST calls.
:::

MS Graph Event Item function in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/functions/calendar/get-calendar-event-details.jigx).

:::CodeblockTabs
get-calendar-events-details.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/users/{userId}/calendars/{calendarId}/events/{calendarEventId}
outputTransform: $
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth # Use manage.jigx.com to define credentials for your solution
  userId:
    type: string
    location: path
    required: true
  calendarId:
    type: string
    location: path
    required: true
  calendarEventId:
    type: string
    location: path
    required: true
forRowsWithValues:
  id: calendarEventId
  
```
:::

## Jigs

MS Graph Calendar Events jig in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/calendar/view-calendar-events.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
view-calendar-event-details

```yaml
title: =@ctx.jig.inputs.subject
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://support.content.office.net/en-us/media/f1c4b693-4670-4e7a-8102-bbf1749e83fe.jpg

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Location
            value: =@ctx.jig.inputs.locationDisplayName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Day
                  value: =$fromMillis($toMillis(@ctx.jig.inputs.evtFrom), '[MNn] [D], [Y]', @ctx.system.timezone.offset)
              - type: component.entity-field
                options:
                  label: Time
                  value: |
                    = $fromMillis($toMillis(@ctx.jig.inputs.evtFrom), '[h]:[m01] [PN]', @ctx.system.timezone.offset)
                    & " to " & 
                    $fromMillis($toMillis(@ctx.jig.inputs.evtTo), '[h]:[m01] [PN]', @ctx.system.timezone.offset)
        - type: component.entity-field
          options:
            label: Online Meeting
            value: =@ctx.jig.inputs.onlineMeetingProvider
            contentType: link
            href: =@ctx.jig.inputs.onlineMeetingUrl
            isTrackingTransparencyRequired: false
            isHidden: =@ctx.jig.inputs.isOnlineMeeting? false:true
        - type: component.entity-field
          options:
            label: Summary
            value: =@ctx.jig.inputs.bodyPreview
            isMultiline: true
  - type: component.expander
    options:
      isInitiallyCollapsed: true
      header:
        centerElement: 
          type: component.titles
          options: 
            title: Task Message (Expand to Read)  
      children:
        - type: component.web-view
          options:
            isTrackingTransparencyRequired: false
            height: 400
            content: |
              =("
              <html>
                <head>
                  <meta name=" & "'" & "viewport" & "'" & " content=" & "'" & "width=device-width, " & "initial-scale=1" & "'" & "/>
                </head>
                <body>" 
                  & @ctx.jig.inputs.bodyContent
              & "</body>
              </html>")
  - type: component.list
    options:
      data: =@ctx.jig.inputs.attendees
      maximumItemsToRender: 8
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.emailAddress.name
          divider: solid
          subtitle: "='Status: ' & @ctx.current.item.status.response"
          label:
            title: =@ctx.current.item.type
            color:
              - when: =@ctx.current.item.type = 'required'
                color: color2
              - when: =@ctx.current.item.type != 'required'
                color: color7
          leftElement: 
            element: avatar
            text: =$uppercase(@ctx.current.item.emailAddress.name)

actions:
  - children:
      - type: action.open-url
        options:
          title: Join Meeting
          url: =@ctx.jig.inputs.onlineMeetingUrl
          isHidden: |
            =@ctx.jig.inputs.isOnlineMeeting? false: true
            
preview:
  header: 
    type: component.jig-header
    options:
      height: small
      children: 
        type: component.image
        options:
          source:
            uri: https://support.content.office.net/en-us/media/f1c4b693-4670-4e7a-8102-bbf1749e83fe.jpg
  isCompact: false
  children:
    - type: component.entity
      options:
        children: 
        - type: component.entity-field
          options:
            label: Subject
            value: =@ctx.jig.inputs.subject
            contentType: default
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Day
                  value: =$fromMillis($toMillis(@ctx.jig.inputs.evtFrom), '[MNn] [D], [Y]', @ctx.system.timezone.offset)
              - type: component.entity-field
                options:
                  label: Time
                  value: |
                    = $fromMillis($toMillis(@ctx.jig.inputs.evtFrom), '[h]:[m01] [PN]', @ctx.system.timezone.offset)
                    & " to " & 
                    $fromMillis($toMillis(@ctx.jig.inputs.evtTo), '[h]:[m01] [PN]', @ctx.system.timezone.offset)
        - type: component.entity-field
          options:
            label: Summary
            value: =@ctx.jig.inputs.bodyPreview
            isMultiline: true
    - type: component.web-view
      options:
        isTrackingTransparencyRequired: false
        height: 400
        content: |
          =("
          <html>
            <head>
              <meta name=" & "'" & "viewport" & "'" & " content=" & "'" & "width=device-width, " & "initial-scale=1" & "'" & "/>
            </head>
            <body>" 
              & @ctx.jig.inputs.bodyContent
          & "</body>
          </html>")
  actions:
    # - when: =@ctx.jig.inputs.isOnlineMeeting = 1
    - children:
      - type: action.open-url
        options:
          title: Join Meeting
          url: =@ctx.jig.inputs.onlineMeetingUrl
          isHidden: |
            =@ctx.jig.inputs.isOnlineMeeting? false: true
         
```
:::

## See Also

- [Get Event List](<./Get Event List.md>)
- [Get Calendar List](<./Get Calendar List.md>)
- [Create Event Item](<./Create Event Item.md>)

