---
title: Get Event List
slug: eq2E-get-event-list
createdAt: Sat Nov 26 2022 20:48:07 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 17:58:07 GMT+0000 (Coordinated Universal Time)
---

# Get Event List

{% columns %}
{% column %}
### Scenario

Get a list of the next week's events on a user's calendar from Microsoft Graph using GET REST functions and show the events in a calendar jig.

**Resource links:**

* [List events](https://learn.microsoft.com/en-us/graph/api/user-list-events?view=graph-rest-1.0\&tabs=http) - MS Graph documentation
* [List calendarView](https://learn.microsoft.com/en-us/graph/api/user-list-calendarview?view=graph-rest-1.0\&tabs=http) - MS Graph documentation
* [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
* [Configuring OAuth for MS Graph](https://docs.jigx.com/configuring-oauth-for-ms-graph)

**Required OAuth scope** (least to most privilege):

Calendars.Read Calendars.ReadWrite

**Related Sample**

This example uses [Get Calendar List](<Get Calendar List.md>) to provide the calendar input to the view-calendar-events jig and navigates to [Get Event Item](<Get Event Item.md>) when the event item is pressed.&#x20;
{% endcolumn %}

{% column %}
&#x20;![Calendar events](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YBoFi0sX8sWnJ1Kp77gs9_graph-listevents.png)


{% endcolumn %}
{% endcolumns %}

### Examples and code snippets

{% hint style="success" %}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator).
{% endhint %}

### General

{% code title="index.jigx" %}
```yaml
name: ms-graph-demonstrator
title: MS Graph Demonstrator
description: A sample solution that uses the Microsoft Graph API. You can deploy and use this solution without any additional configuration.
category: business
home:
    jigId: calendar-summary
    icon: home-apps-logo
    jigId: next-meeting
    when: |
      =@ctx.datasources.next-meeting=null? false:true
    icon: meeting-remote

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
              parameters:
                accessToken: microsoft.OAuth
                startdatetime: =$fromMillis($millis())
                enddatetime: =$fromMillis($millis()+604800000)
            - entity: calendars
              function: get-calendar-list
              parameters:
                accessToken: microsoft.OAuth

```
{% endcode %}

### Functions

MS Graph Event List function in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/functions/calendar/get-calendar-event-list.jigx).

{% tabs %}
{% tab title="get-calendar-event-list.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me/calendars/{calendarId}/events
outputTransform: $
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth #Use manage.jigx.com to define credentials for your solution
  calendarId:
    type: string
    location: path
    required: true
  $top:
    type: string
    location: query
    required: false
    value: 100
  $filter:
    type: string
    location: query
    required: false
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
```
{% endtab %}

{% tab title="get-calendar-events-next-week.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me/calendarview
outputTransform: $
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth #Use manage.jigx.com to define credentials for your solution
  startdatetime:
    type: string
    location: query
    required: true
  enddatetime:
    type: string
    location: query
    required: true
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
```
{% endtab %}
{% endtabs %}

### Jigs

MS Graph Calendar Events List jig in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/calendar/view-calendar-events.jigx).

{% code title="view-calendar-events.jigx" %}
```yaml
title: Calendar
type: jig.calendar

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://support.content.office.net/en-us/media/f1c4b693-4670-4e7a-8102-bbf1749e83fe.jpg

# sync the events for the selected calendar by calendarId
onFocus:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: calendarEvents
        function: get-calendar-event-list
        parameters:
          accessToken: microsoft.OAuth
          calendarId: =@ctx.jig.inputs.calId
          $filter: ="start/dateTime ge '" & $fromMillis($millis()-86400000) & "' and end/dateTime le '" & $fromMillis($millis()+5184000000) & "'"

onRefresh:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: calendarEvents
        function: get-calendar-event-list
        parameters:
          accessToken: microsoft.OAuth
          calendarId: =@ctx.jig.inputs.calId
          $filter: ="start/dateTime ge '" & $fromMillis($millis()-86400000) & "' and end/dateTime le '" & $fromMillis($millis()+5184000000) & "'"

datasources:
  calendarEvents:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: calendarEvents
      jsonProperties:
        - attendees
      query: |
        SELECT id,
        '$.id' as eventId,
        '$.createdDateTime',
        '$.lastModifiedDateTime',
        '$.originalStartTimeZone',
        '$.originalEndTimeZone',
        '$.reminderMinutesBeforeStart',
        '$.isReminderOn',
        '$.hasAttachments',
        '$.subject',
        '$.bodyPreview',
        '$.importance',
        '$.sensitivity',
        '$.isCancelled',
        '$.isOrganizer',
        '$.showAs',
        '$.webLink',
        json_extract(Data, '$.onlineMeetingUrl.joinUrl') as onlineMeetingUrl,
        '$.isOnlineMeeting',
        '$.onlineMeetingProvider',
        '$.onlineMeeting',
        json_extract(Data, '$.body.contentType') as bodyContentType,
        json_extract(Data, '$.body.content') as bodyContent,
        json_extract(Data, '$.start.dateTime') || 'Z' as startTime,
        json_extract(Data, '$.end.dateTime') || 'Z' as endTime,
        '$.location',
        '$.attendees',
        '$.organizer'
        FROM [calendarEvents]

data: =@ctx.datasources.calendarEvents
item:
  type: component.event
  options:
    from: =@ctx.current.item.startTime
    to: =@ctx.current.item.endTime
    title: =@ctx.current.item.subject
    location: "='Importance: ' & @ctx.current.item.importance"
    description: =@ctx.current.item.bodyPreview
    people: "=@ctx.current.item.attendees.{'fullName': emailAddress.address, 'email': emailAddress.address}"
    buttonTitle: View Event Details
    onPress:
      type: action.go-to
      options:
        linkTo: view-calendar-event-details-w
        parameters:
          eventId: =@ctx.current.item.eventId
          evtFrom: =@ctx.current.item.startTime
          evtTo: =@ctx.current.item.endTime
          bodyContent: =@ctx.current.item.bodyContent
          summary: =@ctx.current.item.bodyPreview
          subject: =@ctx.current.item.subject
          onlineMeetingUrl: =@ctx.current.item.onlineMeetingUrl
          isOnlineMeeting: =@ctx.current.item.isOnlineMeeting
          bodyPreview: =@ctx.current.item.bodyPreview
          attendees: =@ctx.current.item.attendees
          onlineMeetingProvider: =@ctx.current.item.onlineMeetingProvider

actions:
  - children:
      - type: action.go-to
        options:
          title: Create New Event
          linkTo: create-calendar-event
```
{% endcode %}

### See Also

* [Get Calendar List](<Get Calendar List.md>)
* [Get Event Item](<Get Event Item.md>)
* [Create Event Item](<Create Event Item.md>)
