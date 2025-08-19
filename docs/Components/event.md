# event

The component can only be used in the [jig.calendar](<../Jig Types/jig_calendar.md>) to display events related to data records. All events have a start and end date. Additional elements can be added, such as people attending the event or where the event will take place.

### Configuration options

Some properties are common to all components, see [Common component properties](event.md) for a list and their configuration options.

<table><thead><tr><th width="159.73046875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>from</code></td><td>Configure the starting time. You can change the property format by setting the value to the <code>Text With Format</code> property, <em>cntrl+space</em>, and choosing <code>Date</code>. In the <code>format</code> property, select the required date format. The default format saved in the database is <strong>yyyy/mm/ddThour:minute:second</strong> (i.e., 2022-07-27T08:15:00). For more information about the setting of the date format/ time zones, refer to .</td></tr><tr><td><code>to</code></td><td>Configure the ending time. You can change the property format by setting the value to the <code>Text With Format</code> property, <em>cntrl+space</em>, and choosing <code>Date</code>. In the <code>format</code> property, select the required date format. The default format saved in the database is <strong>yyyy/mm/ddThour:minute:second</strong> (i.e., 2022-07-27T08:15:00). For more information about the setting of the date format/ time zones, refer to.</td></tr><tr><td><code>title</code></td><td>Provide the name of the event.</td></tr></tbody></table>

<table><thead><tr><th width="166.3125">Other options</th><th></th></tr></thead><tbody><tr><td><code>description</code></td><td>The general description of the event.</td></tr><tr><td><code>location</code></td><td>The event's location, for example, a meeting room or conference center.</td></tr><tr><td><code>people</code></td><td>The list of invitees/attendees for the event. Use an expression to configure the property, for example, <code>people: =@ctx.current.item.attendees.emailAddress</code>.</td></tr><tr><td><code>tags</code></td><td>Displays a list of <code>tags</code> for the event, such as meeting, interview, or social. The <code>tags</code> array can contain the <em>color</em> and <em>title</em> for each tag. <code>"=[{'title': @ctx.current.item.type, 'color': @ctx.current.item.color}]"</code> or define the tag in a datasource which is referenced in the property. <code>tags: =@ctx.current.item.tags</code></td></tr></tbody></table>

Certain actions can be executed on the event; for example, when pressing on the event opens the URL of the advertised event.

<table><thead><tr><th width="172.33203125">Actions</th><th></th></tr></thead><tbody><tr><td><code>onButtonPress</code></td><td>You can set any action in this property just like in the <code>onPress</code> property. The difference is that if only <code>onButtonPress</code> is configured, after pressing on the event, a modal window with the event's details opens. The modal contains a button for the action configured in the <code>onButtonPress</code> property. When <code>isHidden</code> is used with <code>when:false</code> , the <code>isHidden</code> property is automatically overwritten on the mobile device and set to <code>isHidden:true</code> and the button automatically hides.</td></tr><tr><td><code>onPress</code></td><td>When pressing on the event an action executes. Use IntelliSense to select an action or refer to the list of available . When the <code>onPress</code> is configured, the <code>onButtonPress</code> configuration is ignored.</td></tr></tbody></table>

### Examples and code snippets

#### Event of meeting

{% columns %}
{% column %}
&#x20;![Meeting event](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qH20EHiZsEqMm-1fydZau_tii6byi98kqitscdlxevent-meetingeventiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
The jig displays the event on the calendar. We immediately see what time the meeting will take place, where it will take place and which people will attend.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/static-data/event-of-meeting/event-of-meeting.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/dynamic-data/event-of-meeting/event-of-meeting-dynamic.jigx).

**Datasources**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/event-training.jigx) See the full datasource for dynamic data in [GitHub](event.md)&#x20;
{% endcolumn %}
{% endcolumns %}

:::CodeblockTabs&#x20;

{% tabs %}
{% tab title="event-of-meeting" %}
```yaml
# add file under jigs folder 
type: jig.calendar
title: =$now('[D1o] [MNn] [Y]')

data: =@ctx.datasources.event-meeting
item: 
  type: component.event
  options:
    title: =@ctx.current.item.name
    description: =@ctx.current.item.description
    from: 
      text: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)
      format:
        dateFormat: lll
    to: 
      text: =$fromMillis($toMillis($now()) + @ctx.current.item.eventEnd * 3600000)
      format:
        dateFormat: lll
    people: =@ctx.current.item.people
    tags: =@ctx.current.item.tags
    location: =@ctx.current.item.location
```
{% endtab %}

{% tab title="event-of-meeting-dynamic" %}
```yaml
# add file under jigs folder 
type: jig.calendar
title: =$now('[D1o] [MNn] [Y]')

data: =@ctx.datasources.event-meeting-dynamic
item: 
  type: component.event
  options:
    title: =@ctx.current.item.title
    description: =@ctx.current.item.description
    from: 
      text: =$fromMillis($toMillis($now()) + $number(@ctx.current.item.eventStart) * 3600000)
      format:
        dateFormat: lll
    to: 
      text: =$fromMillis($toMillis($now()) + $number(@ctx.current.item.eventEnd) * 3600000)
      format:
        dateFormat: lll
    people: =@ctx.datasources.event-people-dynamic
    location:  =@ctx.current.item.location
    tags: "=[{'title': @ctx.current.item.tags, 'color': @ctx.current.item.color}]"
```
{% endtab %}

{% tab title="event-meeting" %}
```yaml
type: datasource.static
options:
  data:
    - name: "Meeting with the mayor"
      description: "Discussion of subsidies"
      eventStart: 1
      eventEnd: 2
      tags:
        - color: color2
          title: Important
      location: "4 Great Jones Alley, NY"
      people: 
        - avatarUrl: https://images.unsplash.com/photo-1548449112-96a38a643324?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          fullName: John Doe
        - avatarUrl: https://images.unsplash.com/photo-1624224971170-2f84fed5eb5e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1598&q=80
          fullName: Andrew Williams
        - avatarUrl: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          fullName: July Nelson
        - avatarUrl: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
          fullName: Karl Fisher
```
{% endtab %}

{% tab title="event-meeting-dynamic" %}
```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - entity: default/calendar
  query: |
    SELECT
      '$.title',
      '$.description',
      '$.eventStart',
      '$.eventEnd',
      '$.location',
      '$.tags',
      '$.color',
      '$.category'
    FROM [default/calendar] WHERE category = "meeting"
```
{% endtab %}
{% endtabs %}

#### Event of training

{% columns %}
{% column %}
&#x20;![Training event](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZqCjnEYr20cKgcuryWYA_event-training.PNG)&#x20;


{% endcolumn %}

{% column %}
&#x20;The jig displays a multi-day event on the calendar.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/static-data/multi-day-event/multi-day-event.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/dynamic-data/multi-day-event/multi-day-event-dynamic.jigx).

**Datasources**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/event-vacation.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/event-vacation-dynamic.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="multi-day-event-day-event" %}
```yaml
# add file under jigs folder 
title: =$now('[D1o] [MNn] [Y]') 
type: jig.calendar
data: =@ctx.datasources.event-training
item:
  type: component.event
  options:
    title: =@ctx.current.item.name
    from: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)  
    location: =@ctx.current.item.location
    to: =$fromMillis($toMillis($now()) + 2 * 60 * 60000 + @ctx.current.item.eventEnd * 3600000)
```
{% endtab %}

{% tab title="multi-day-event-dynamic" %}
```yaml
# add file under jigs folder 
title: =$now('[D1o] [MNn] [Y]')
type: jig.calendar
data: =@ctx.datasources.event-training-dynamic
item:
  type: component.event
  options:
    title: =@ctx.current.item.title
    from: =$fromMillis($toMillis($now()) + $number(@ctx.current.item.eventStart) *
        3600000)  
    location: =@ctx.current.item.location
    to: =$fromMillis($toMillis($now()) + 5 * 60 * 60000 + @ctx.current.item.eventEnd * 3600000)
```
{% endtab %}

{% tab title="event-training" %}
```yaml
# Add file under datasources folder
type: datasource.static
options:
  data:
    - eventEnd: 168 
      eventStart: 0
      location: Blue room
      name: Onboarding/Induction Training
```
{% endtab %}

{% tab title="event-training-dynamic" %}
```yaml
# Add file under datasources folder
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - entity: default/calendar
  query: |
    SELECT
      '$.title',
      '$.location',
      '$.eventStart',
      '$.eventEnd',
      '$.category' 
    FROM [default/calendar] WHERE '$.category' = 'meeting-event'
```
{% endtab %}
{% endtabs %}

#### Event with action

{% columns %}
{% column %}
&#x20;![Event with action](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VRUxBeE5caQr5pntG0EYD_img8568iphone13blueportrait.png)&#x20;


{% endcolumn %}

{% column %}
&#x20;![Event with action](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YeceMRw6Rbi1bKY6Yfxpe_img8569iphone13blueportrait.png)&#x20;


{% endcolumn %}
{% endcolumns %}

The jig displays an event on the calendar with actions on the main screen or in the detail of the event.

**Examples**: \
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/dynamic-data/event-with-action/event-with-action.jigx). \
See also the supporting files [create event](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/dynamic-data/event-with-action/create-event.jigx) and [add event users](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/event/dynamic-data/event-with-action/add-event-user.jigx) in GitHub.

**Datasource**: \
See the full datasource using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data-dynamic.jigx).

:::CodeblockTabs&#x20;

{% tabs %}
{% tab title="event-with-action.jigx" %}
```yaml
# add file under jigs folder 
title: Calendar with action
type: jig.calendar

datasources:
  event-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/calendar
      query: | 
        SELECT
          id,
          '$.title',
          '$.location',
          '$.time',
          '$.date-from',
          '$.date-to',
          '$.eventStart',
          '$.eventEnd',
          '$.fullname',
          '$.avatar',
          '$.color',
          '$.tags',
          '$.category',
          '$.email'
        FROM [default/calendar] WHERE '$.category' = "people"
        UNION 
        SELECT
          id,
          '$.title',
          '$.location',
          '$.time',
          '$.date-from',
          '$.date-to',
          '$.eventStart',
          '$.eventEnd',
          '$.fullname',
          '$.avatar',
          '$.color',
          '$.tags',
          '$.category',
          '$.email'
        FROM [default/calendar] 
        WHERE '$.email' = @email and '$.category' = "update"
      queryParameters:
        email: =@ctx.user.email

actions:
  - children:
      - type: action.go-to
        options:
          title: Create new Event
          linkTo: create-event

data: =@ctx.datasources.event-dynamic
item:
  type: component.event
  options:
    from: =@ctx.current.item.eventStart != null ? $fromMillis($toMillis($now()) + $number(@ctx.current.item.eventStart) * 3600000) :$fromMillis($toMillis(@ctx.current.item.date-from))
    to: =@ctx.current.item.eventEnd != null ? $fromMillis($toMillis($now()) + $number(@ctx.current.item.eventEnd) * 3600000) :$fromMillis($toMillis(@ctx.current.item.date-to))  
    title: =@ctx.current.item.title
    location:  =@ctx.current.item.location
    tags: "=[{'title': @ctx.current.item.tags, 'color': @ctx.current.item.color}]"
    people: =@ctx.current.item.avatar != null ? [{'fullName':@ctx.current.item.fullname, 'avatarUrl':@ctx.current.item.avatar}]
    onButtonPress: 
      type: action.action-list
      options:
        title: Register for the meeting
        actions:
          - type: action.go-to
            options:
              linkTo: add-event-user
              parameters:
                id: =@ctx.current.item.id
                title: =@ctx.current.item.title
```
{% endtab %}

{% tab title="create-event.jigx" %}
```yaml
# add file under jigs folder 
title: Create event
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/calendar
          method: create
          data:
            id: =@ctx.components.id.state.value
            category: =@ctx.components.category.state.value
            title: =@ctx.components.title.state.value
            location: =@ctx.components.location.state.value
            date-from: =@ctx.components.date-from.state.value
            date-to: =@ctx.components.date-to.state.value
            tags: =@ctx.components.tags.state.value
            email: =@ctx.components.email.state.value
            color: =@ctx.components.color.state.value     
          onSuccess: 
            type: action.go-back

children:
  - type: component.form
    instanceId: newEvent
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: id
          options:
            label: id
            isHidden: true
        - type: component.text-field
          instanceId: category
          options:
            label: category
            value: update
            isHidden: true
        - type: component.text-field
          instanceId: title
          options: 
            label: Event name
        - type: component.text-field
          instanceId: location
          options:
            label: Event location
        - type: component.field-row
          options:
            children:
              - type: component.date-picker
                instanceId: date-from
                options:
                  label: Event start
                  mode: datetime
              - type: component.date-picker
                instanceId: date-to
                options:
                  label: Event end
                  mode: datetime
        - type: component.text-field
          instanceId: tags
          options:
            label: Tag
        - type: component.text-field
          instanceId: email
          options:
            label: Email
            value: =@ctx.user.email
            isHidden: true
        - type: component.text-field
          instanceId: color
          options:
            label: color
            value: color6
            isHidden: true
```
{% endtab %}

{% tab title="add-event-user.jigx" %}
```yaml
title: Registration
type: jig.default
description: =@ctx.jig.inputs.title
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/calendar
          method: create
          data:
            id: =@ctx.components.id.state.value
            userName: =@ctx.components.userName.state.value
            userEmail: =@ctx.components.userEmail.state.value
            PhoneNumber: =@ctx.components.PhoneNumber.state.value
            avatar: =@ctx.components.avatar.state.value
          onSuccess: 
            type: action.go-back
                 
children:
  - type: component.form
    instanceId: bookForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
      - instanceId: id
        options:
          isHidden: true
          label: id
          value: =@ctx.jig.inputs.id
        type: component.text-field
      - options:
          children:
            - instanceId: userName
              options:
                label: Name
                value: =@ctx.user.displayName
              type: component.text-field
            - instanceId: userEmail
              options:
                label: Email
                value: =@ctx.user.email
              type: component.email-field
        type: component.field-row
      # - instanceId: userPhone
      #   options:
      #     label: Phone
      #   type: component.number-field
      - type: component.text-field
        instanceId: PhoneNumber
        options:
          label: Phone Number
          value: =@ctx.datasources.employee-detail-dynamic.phone
          keyboardType: phone-pad
          # Set the type of text for this field. This will enforce a regex for this field of the type it is set to.
          textContentType: telephoneNumber 
      - instanceId: avatar
        options:
          label: Photo
        type: component.avatar-field
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            contentType: phone
            label: Phone
            value: =@ctx.datasources.employee-detail-dynamic.phone
```
{% endtab %}
{% endtabs %}
