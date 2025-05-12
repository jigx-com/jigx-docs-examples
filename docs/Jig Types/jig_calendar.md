# jig.calendar

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The calendar jig displays an agenda calendar view. `jig.calendar` contains data with an <a href="https://docs.jigx.com/docs/jc-event" target="_blank">event</a> component, which adds functionality to the calendar and provides a convenient overview of your scheduled events.
:::

:::VerticalSplitItem
::Image[]{alt="Jig Calendar Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/soEBniAbtE5Ia__YoZDrw_calendarmain.png" size="80" caption="Jig Calendar Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/soEBniAbtE5Ia__YoZDrw_calendarmain.png"}
:::
::::

## Configuration options

Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `from`             | Configure the starting time. You can change the property format by setting the value to the `Text With Format` property, *cntrl+space*, and choosing `Date`. In the `format` property, select the required date format.&#xA;The default format saved in the database is **yyyy/mm/ddThour\:minute\:second** (i.e., 2022-07-27T08:15:00). &#xA;Expressions for modifying the date and time format can be found in the [Expressions - cheatsheet](#). |
| `title`            | Provide the name of the event. If you do not want to show a title in a jig use `title: ' '` or add an expression.                                                                                                                                                                                                                                                                                                                                   |
| `to`               | Configure the ending time. You can change the property format by setting the value to the `Text With Format` property, *cntrl+space*, and choosing `Date`. In the `format` property, select the required date format.&#xA;The default format saved in the database is **yyyy/mm/ddThour\:minute\:second** (i.e., 2022-07-27T08:15:00). &#xA;Expressions for modifying the date and time format can be found in the [Expressions - cheatsheet](#).   |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `description`     | The general description of the event.                                                                                                                                                                                                                                                                                                             |
| `icon`            | The icon will be displayed on the [widget](#) of this jig. Start typing the name of the icon to invoke the available list in IntelliSene. See [Jigx icons](#) for information on worknig with icons.                                                                                                                                              |
| `people`          | The list of invitees/attendees for the event. Use an expression to configure the property, for example, &#xA;`people: =@ctx.current.item.attendees.emailAddress`.                                                                                                                                                                                 |
| `location`        | The event's location, for example, a meeting room or conference center.                                                                                                                                                                                                                                                                           |
| `tags`            | Displays a list of `tags` for the event, such as meeting, interview, or social. The `tags` array can contain the *color* and *title* for each tag. &#xA;`"=[{'title': @ctx.current.item.type, 'color': @ctx.current.item.color}]"`&#xA;or define the tag in a datasource whihc is referenced in the property.&#xA;`tags: =@ctx.current.item.tags` |

Certain actions can be executed on the event; for example, when pressing on the event opens the URL of the advertised event.

| **Actions**     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `onButtonPress` | You can set any action in this property just like in the `onPress` property. The difference is that if only `onButtonPress` is configured, after pressing on the event, a modal window with the event's details opens. The modal contains a button for the action configured in the `onButtonPress` property. When `isHidden` is used with `when:false` , the `isHidden` property is automatically overwritten on the mobile device and set to `isHidden:true` and the button automatically hides. |
| `onPress`       | When pressing on the event an action executes. Use IntelliSense to select an action or refer to the list of available [Actions](./../Actions.md). When the `onPress` is configured, the `onButtonPress` configuration is ignored.                                                                                                                                                                                                                                                                  |

## Examples and code snippets

:::hint{type="success"}
The code below is an extract from the full *jigx-samples* solution. The code snippets describe the component discussed in this section. For the solution to function in the Jigx app download the full *jigx-samples* project from <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples" target="_blank">GitHub,</a> and follow the instructions in [Setting up your solution](docId:1gfew7GRPvkfxon-TsymP).
:::

### Calendar jig

In this example, we show the daily agenda, by tapping we can get the details about the actual event and the overview for a month is also available. You can easily recognize the days we have an event planned thanks to the markings.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{alt="Calendar jig events" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/leFvY-3-iDe8str7O0H6d_calendarmain.png" size="86" caption="Calendar jig events" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/leFvY-3-iDe8str7O0H6d_calendarmain.png"}
:::

:::VerticalSplitItem
::Image[]{alt=" Event details" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SplwcoBsb4CiF3nXDBm9r_calendareventdetail.png" size="86" caption=" Event details" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SplwcoBsb4CiF3nXDBm9r_calendareventdetail.png"}
:::
::::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{alt="Meeting details & link" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IqXVVr7I3J7naESvgjZWZ_calendareventdetail2.png" size="86" caption="Meeting details & link" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IqXVVr7I3J7naESvgjZWZ_calendareventdetail2.png"}
:::

:::VerticalSplitItem
::Image[]{alt="Month with event markers" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/g4RQkjSGj73R4dM3uJ5i8_calendarfull.PNG" size="86" caption="Month with event markers" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/g4RQkjSGj73R4dM3uJ5i8_calendarfull.PNG"}
:::
::::

**Examples:**
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-calendar/static-data/calendar-example/calendar-example.jigx).
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data-dynamic.jigx).
**Datasources:**
See the full code sample for datasources for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data.jigx).
See the full code sample for datasources for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data-dynamic.jigx).

:::hint{type="success"}
Using the code below requires data in the database, the jigx.:Comment[sample]{resolved="true" docCommentId="8ysxgrBnh1CFlCx6O3e74"} solution has the data provided for calendar-sample. You can use the calendar-sample.csv file in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/csv/calendar-sample.csv) and upload it via the [Data](#) configuration in Jigx Management.
:::

:::CodeblockTabs
calendar-example-dynamic.jigx

```yaml
title: Calendar
type: jig.calendar
icon: calendar

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://cdnsm5-ss13.sharpschool.com/UserFiles/Servers/Server_181580/Image/calendar.jpg

data: =@ctx.datasources.calendar-data-dynamic
item:
  type: component.event
  options:
    from: =@ctx.current.item.startDT
    to: =@ctx.current.item.endDT
    title: =@ctx.current.item.subject
    location:  =@ctx.current.item.location
    people: =@ctx.current.item.attendees.emailAddress
    description: =@ctx.current.item.bodyPreview
    tags: =@ctx.current.item.tags
    onButtonPress: 
      when: =@ctx.current.item.isOnline="true"
      type: action.open-url
      options:
        title: Join Meeting
        url: =@ctx.current.item.onlineUrl
        isTrackingTransparencyRequired: false
        isHidden: =@ctx.current.item.isOnline="true"?false:true
```

datasources

```yaml
datasources:
  calendar-data-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
    
      entities:
        - default/calendar
    
      jsonProperties: 
      # column names of the result set specified under jsonProperties will retain their json object format
        - attendees
        - tags
        - start
    
    # PLEASE NOTE: the query below contains 2 complex statements to calculate the start and end date of the meeting. this is only for demo purposes
    # to ensure that entries in the calendar always starts tomorrow when you view the sample code.
    # Under normal circumstances the start and end dates are ISO-8601 format (YYYY-MM-DDTHH:MM).
      query: | 
        SELECT
          id,
          '$.subject',
          '$.location',
          '$.body',
          '$.bodyPreview',    
          date('now', json_extract(json_extract(data, '$.start'), '$.dayOffset'),'localtime') || 'T' || json_extract(json_extract(data, '$.start'), '$.time') as startDT,
          strftime('%Y-%m-%dT%H:%M:%S', datetime(date('now', json_extract(json_extract(data, '$.start'), '$.dayOffset'),'localtime') || 'T' || json_extract(json_extract(data, '$.start'), '$.time'), '+1 hours')) as endDT,
          '$.isAllDay',
          '$.attendees',
          '$.tags',
          '$.isOnline',
          '$.onlineUrl'
        FROM [default/calendar]
```

default.jigx

```yaml
databaseId: default
tables:
  calendar: null
```

index.jigx

```yaml
name: jigx-calendar-sample
title: jigx-calendar-sample
category: business
tabs:
  home:
    jigId: calendar
    icon: calendar 
```
:::

### Considerations

- The sample above is for illustrative purposes only, and shows how to use a SQL statement to always return dates with events from the next day onwards.
- A dynamic data table defines the event data, and a JSON view of one of the records can be seen in Dynamic Data.
- The calendar uses a data source that selects the list of events. The start and end dates are dynamically calculated using the SQLite `date()` and `strftime()` functions. The JSON in the Dynamic Data is a string when entered through Jigx Management with the result of what seems like a double json\_extract, but is not.
- The SQL select statement that returns the `startDT` and `endDT` takes today’s date, adds the day offset as specified in the start field in Dynamic Data, and appends the time in the start field.  The complete start dates and times are built up by concatenating the two values. Similiarly for the end date except add an hour to the SQL statement.
- When using applications such as Microsoft Exchange and Microsoft Graph as a datasource, replace the date part of the datetime with the same formula while using the time part of the graph calendar item.

:::::ExpandableHeading
### Calendar with preview

This example displays a preview after long-pressing the event in the Calendar jig (on the event)

:::hint{type="info"}
Only [Entity](./../Preview/Entity.md) and [Web-view](./../Preview/Web-view.md) are available as child components for preview.
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/INfH1Ok873_PEOLp8N4zz_cal-prew.png)
:::

:::VerticalSplitItem
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/I_AMevUwmBQnVwpdv2_GI_3uap-p2or6r5o9qqiec8eimg7960iphone13blueportrait.png)
:::
::::

**Examples:**
See the full example of [calendar-jig](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-calendar/static-data/calendar-preview/calendar-jig.jigx) and [calendar-detail-entity](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-calendar/static-data/calendar-preview/calendar-detail-entity.jigx) in GitHub.

:::CodeblockTabs
calendar-jig

```yaml
title: Entity preview - Calendar
type: jig.calendar
icon: career

header: 
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        title: Upcoming meetings
        source:
          uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8bWVldGluZ3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=900&q=60
datasources:
  calendar_data: 
    type: datasource.static
    options:
      data:
        - description: New features to be added
          id: 1
          title: Documentation Discussion
          type: meeting
          color: color2
          people: https://images.unsplash.com/photo-1548449112-96a38a643324?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - description: Project manager position
          id: 2
          title: Second interview - Maria Booyens
          type: interview
          color: color3
          people: https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        
    
data: =@ctx.datasources.calendar_data  
item:
  type: component.event
  options:
    from:
      text: =$fromMillis($toMillis($now()) + ($number(@ctx.current.item.id)- 1) * 3600000)
      format:
        dateFormat: "l"
    to: =$fromMillis($toMillis($now()) + $number(@ctx.current.item.id) *
      3600000)
    title: =@ctx.current.item.title
    description: =@ctx.current.item.description
    tags: "=[{'title': @ctx.current.item.type, 'color': @ctx.current.item.color}]"
    people: "=[{'avatarUrl': @ctx.current.item.people}]"
    onPress: 
      type: action.go-to
      options:
        linkTo: entity-calendar-detail
        parameters:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          type: =@ctx.current.item.type
    onButtonPress: 
      type: action.go-to
      options:
        title: Go to detail
        linkTo: entity-calendar-detail
        parameters:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          type: =@ctx.current.item.type
    buttonTitle: Go to detail
```

calendar-detail-entity

```yaml
title: Meeting detail
type: jig.default

header: 
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        title: Meeting detail
        source:
          uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8bWVldGluZ3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=900&q=60

children:
    - type: component.entity
      options:
        isCompact: true
        children:
          - type: component.section
            options:
              title: Meeting - Compact entity
              children:
                - type: component.entity-field
                  options:
                    label: Title
                    value: =@ctx.jig.inputs.title   
                - type: component.entity-field
                  options:
                    label: Type
                    value: =@ctx.jig.inputs.type
                    rightIcon: conversation-chat-2
                - type: component.entity-field
                  options:
                    label: Description
                    value: =@ctx.jig.inputs.description   

              
preview:
  isCompact: true
  actions:
   - children:
        - type: action.go-to
          options:
            title: Join the meeting
            linkTo: placeholder
        - type: action.go-to
          options:
            title: Cancel the meeting
            linkTo: placeholder
            style:
              isDanger: true
        - type: action.go-to
          options:
            title: Change the location
            linkTo: placeholder
            style:
              isDisabled: true


  children:
    - type: component.entity
      options:
        isCompact: true
        children:
          - type: component.section
            options:
              title: Meeting - Compact entity
              children:
                - type: component.entity-field
                  options:
                    label: Title
                    value: =@ctx.jig.inputs.title  
                - type: component.entity-field
                  options:
                    label: Description
                    value: =@ctx.jig.inputs.description 
                - type: component.entity-field
                  options:
                    label: Type
                    value: =@ctx.jig.inputs.type
                    
          
  header: 
    type: component.jig-header
    options:
      height: medium
      children: 
        type: component.image
        options:
          title: Meeting detail
          source:
            uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8bWVldGluZ3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=900&q=60
```
:::
:::::

## See also

- [Jigs (screens)](#)
- [Related examples (Github)](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-calendar)

