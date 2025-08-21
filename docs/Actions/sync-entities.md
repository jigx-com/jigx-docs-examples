# sync-entities

This action can be used to sync your local database with your live database on the server. There are multiple ways to set up a `sync-entities` action within a jig:

1. Under action button
2. In action list
3. In onPress/onChange events (if the component has these options)
4. In onRefresh/onFocus
5. Dynamically sync multiple entities

{% hint style="warning" %}
`sync-entities` can't be used if you using [Static Data](https://docs.jigx.com/examples/static).&#x20;
{% endhint %}

## Examples and code snippets

### sync-entities in action

{% columns %}
{% column %}
In this example, when tapping the Sync entities button the `action.sync-entities` is used to show a list of employees.

**Example:** The full example of sync-entities in action you can find in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/sync-entities/sync-entities-action.jigx)
{% endcolumn %}

{% column %}
::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0loGd9Ahy\_Ed5LO5RY\_5j\_action-sync-entities.PNG" size="80" position="center" caption="Sync-entities action" alt="Sync-entities action" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0loGd9Ahy\_Ed5LO5RY\_5j\_action-sync-entities.PNG" width="800" height="791" darkWidth="800" darkHeight="791"}
{% endcolumn %}
{% endcolumns %}

{% code title="sync-entities-action.jigx" %}
```yaml
actions:
  - children:
    - type: action.sync-entities
      options:
        title: Sync entities
        provider: DATA_PROVIDER_DYNAMIC
        entities:
          - default/employees    
```
{% endcode %}

### sync-entities in the action list

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mvmPcSbReereFrlWFAo8t\_syncent-actionlist.PNG" size="80" position="center" caption="Sync-entities action" alt="sync-entities action" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mvmPcSbReereFrlWFAo8t\_syncent-actionlist.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}&#x20;
{% endcolumn %}

{% column %}
In this example the `action.sync-entities` is used to linkt to the a different jig.

**Example:** The full example of sync-entities in an action list you can find in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/sync-entities/sync-entities-actionlist.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="sync-entities-actionlist.jigx" %}
```yaml
actions:
  - children:
    - type: action.action-list
      options:
        title: Sync entities
        actions:
          - type: action.sync-entities
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entities:
                - default/employees
          - type: action.go-to
            options:
              linkTo: default-employee-detail
```
{% endcode %}

### sync-entities in onPress/onChange event

{% columns %}
{% column %}
Here is the example of [sync-entities](https://docs.jigx.com/examples/sync-entities) in onPress/onChange event in [list-item](https://docs.jigx.com/examples/list-item)

**Example:**

The full example of sync-entities in onChange you can find in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/sync-entities/sync-entities-onChange.jigx). The full example of sync-entities in onPress you can find in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/sync-entities/sync-entities-onPress.jigx).&#x20;
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fSEBZHTaBdKmnRfeiOWlH\_syncent-onpress.PNG" size="80" position="center" caption="Sync-entities action with onPress" alt="sync-entities action with onPress" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fSEBZHTaBdKmnRfeiOWlH\_syncent-onpress.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="sync-entities-onPress.jigx" %}
```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
    subtitle: =@ctx.current.item.time = null ? '' :'The last onPress action:' & ' ' & @ctx.current.item.time
    leftElement: 
      element: avatar
      text: '' 
      uri: =@ctx.current.item.photo
    onPress: 
      type: action.action-list
      options:
        isSequential: true
        actions:
          - type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              method: update
              entity: default/employees
              data:
                id: =@ctx.current.item.id
                time: =$fromMillis($toMillis($now()), '[h#1]:[m01][P]')
          - type: action.sync-entities
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entities:
                - default/employees
```
{% endtab %}

{% tab title="sync-entities-onChange.jigx" %}
```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
    subtitle: =@ctx.current.item.time = null ? '' :'The last onChange action:' & ' ' & @ctx.current.item.time
    leftElement: 
      element: avatar
      text: '' 
      uri: =@ctx.current.item.photo
    rightElement:
      element: switch
      onChange: 

        type: action.action-list
        options:
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                method: update
                goBack: stay
                entity: default/employees
                data:
                  id: =@ctx.current.item.id
                  time: =$fromMillis($toMillis($now()), '[h#1]:[m01][P]')
            - type: action.sync-entities
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entities:
                  - default/employees
```
{% endtab %}
{% endtabs %}

### sync-entities in onRefresh/onFocus

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/v-diCoJjp-AGG2UGwZn9n\_syncent-inchange.PNG" size="80" position="center" caption="sync-entities action with onRefresh" alt="sync-entities action with onRefresh" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/v-diCoJjp-AGG2UGwZn9n\_syncent-inchange.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}

{% column %}
**Example:**

See the full example of sync-entities on onRefresh action in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/sync-entities/sync-entities-onRefresh.jigx).&#x20;

{% hint style="info" %}
&#x20;If you want to use onLoad or onFocus just change the `onRefresh` to `onLoad` or `onFocus`
{% endhint %}
{% endcolumn %}
{% endcolumns %}

:::CodeblockTabs&#x20;

{% tabs %}
{% tab title="sync-entities-onRefresh.jigx" %}
```yaml
onRefresh: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/employees
```
{% endtab %}

{% tab title="sync-entities-onFocus" %}
```yaml
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/employees
```
{% endtab %}
{% endtabs %}

## Dynamically sync multiple entities

When building a solution, the number of entities to sync and the parameters for each are not always known; for example, when syncing the attachments, files, or documents for a message, there can be zero, one, or more. It is necessary to dynamically specify a list of the entities, functions, and function parameters to return from the database using an expression.

### Considerations

* The expression is specified in the `action.sync-entities` action either as a local action in the jig or as a global action.
* Dynamic sync-entities apply to the REST, OneDrive, and Salesforce data providers.
* Any of the following can be synced dynamically: entity, functions, and function parameters.

### Expression structure

* The **basic expression** structure is `=$.map(array, function)`.
  * Specify the array you will consult, i.e., a datasource `@ctx.datasources.{datasourceName}`.
  * For the function, specify `($item)`.
  * Example of the basic structure `=$map(@ctx.datasources.{datasourceName}, function($item))`.
* After defining the basic structure, **map out** relevant properties from the array to the relevant `entity`/`function`/`parameters` and specify the dynamic entry using the `$.item` property, e.g., `"calenderId": $.item.id`. This will run through all the records in the datasource and perform a sync-entities action for each record in the table.

{% code title="sync-entities-action" %}
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
                "parameters": {
                  "accessToken": "jigx.graph.oauth",
                  "calendarId": $item.id
                }
              }
            })[]
```
{% endcode %}

### Example sync-entities dynamically for calendars (full input source)

To return all records from the input source use `$item.id`. In this example, a jig has two lists; the first list shows all the user's calendars, and the second list uses the `ids` from the first list to return all the events for all the calendars. A summary component shows a count of the number of events.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GmLSc1g6aMLAAgchgPdQK\_jb-dyn-sync-cals.png" size="70" position="center" caption="Sync calendars and events" alt="Sync calendars and events" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GmLSc1g6aMLAAgchgPdQK\_jb-dyn-sync-cals.png" width="800" height="796" darkWidth="800" darkHeight="796"}

{% tabs %}
{% tab title="full-calendar-list" %}
```yaml
# Jig for to show the calendars and events
title: Calendars
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1435527173128-983b87201f4d?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y2FsZW5kYXJ8ZW58MHx8MHx8fDA%3D

onRefresh: 
  type: action.execute-action
  options:
    action: sync-dynamic-ds-rest
    parameters:
      datasource: =@ctx.datasources.list-calendars-rest

actions:
  - children:  
    # dynamically list all calendars using REST using the sync-dynamic-ds-rest
    # global action with and the full datasource.
      - type: action.execute-action
        options:
          title: Sync all calendar events
          action: sync-dynamic-ds-rest
          parameters:
            datasource: =@ctx.datasources.list-calendars-rest
            
children:
  - type: component.section
    options:
      title: My calendars
      children:
        - type: component.list
          options:
          # use the list-calendars-rest to return the list of calendars.
            data: =@ctx.datasources.list-calendars-rest
            maximumItemsToRender: 8
            item: 
              type: component.list-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.id
  - type: component.section
    options:
      title: All Calendar Events
      children:
        - type: component.list
          options:
          # use the list-calendars-rest to return the list events by calendar.
            data: =@ctx.datasources.list-events-by-calendar
            maximumItemsToRender: 8
            item: 
              type: component.list-item
              options:
                title: =@ctx.current.item.subject
               
summary:
  children:
    type: component.summary
    options: 
      layout: counter
 # Expression to count the number of events across all calendars.     
      value: =$count(@ctx.datasources.list-events-by-calendar)
      title: Total events 
```
{% endtab %}

{% tab title="sync-dynamic-ds-rest" %}
```yaml
# Global action using the full datasource to return the calender events
action:  
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
# Add the expression for the dynamic sync-entities in the specified format. 
# The array uses the full datasource.    
    entities: |
      =$map(@ctx.action.parameters.datasource, function($item) {
        $.{
          "entity": "events-from-calendar",
          "function": "get-calendar-event-list",
          "parameters": {
            "accessToken": "jigx.graph.oauth",
            "calendarId": $item.id
          }
        }
      })[]
parameters:
  datasource: 
    type: object
    required: true
```
{% endtab %}

{% tab title="get-calendar-event-list" %}
```yaml
# Rest function to get the calendars events 
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me/calendars/{calendarId}/events
parameters:
  $filter:
    location: query
    required: false
    type: string
  $top:
    location: query
    required: false
    type: string
    value: 100
  accessToken:
    location: header
    required: true
    type: string
    value: jigx.graph.oauth
  calendarId:
    location: path
    required: true
    type: string  
outputTransform: $
continuation:
  parameters:
    accessToken:
      location: header
      required: true
      type: string
      value: jigx.graph.oauth
  url: =$."@odata.nextLink"
  when: =$."@odata.nextLink" 
records: =$.value
useLocalCall: true
```
{% endtab %}
{% endtabs %}

### Example sync-entities dynamically for a selected calendar

To return all records for a selected calendar use `=$map(@ctx.action.parameters.selected, function($item)` in the global action. In this example, a jig has a dropdown to select the calendar and a _Show events_ button syncs the entries in the selected calendar. A summary component shows a count of the number of events in the selected calendar.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-9e6Q31g\_zJYZw9ARJCXw\_jb-dyn-sync-cal2.png" size="78" position="center" caption="Sync events for the birthday calendar" alt="Sync events for the birthday calendar" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-9e6Q31g\_zJYZw9ARJCXw\_jb-dyn-sync-cal2.png" width="800" height="803" darkWidth="800" darkHeight="803"}

{% tabs %}
{% tab title="my-events.jigx" %}
```yaml
# jig to selected the calendar and sync the events for that calendar
title: My events
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1633526543814-9718c8922b7a?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

onRefresh: 
  type: action.execute-action
  options:
    action: sync-dynamic-ds-rest
    parameters:
      datasource: =@ctx.datasources.list-calendars-rest

actions:
  - children: 
  # return events for a selected calendar by passing the selected array in the 
  # parameters.
      - type: action.execute-action
        options:
          title: Show events
          action: sync-dynamic-selected-rest
          parameters:
            selected: =@ctx.components.selectCalendar.state.selected
  # If you wanted a single value returned replace {selected} with {value}.
      
children:
  - type: component.form
    instanceId: selectCalendarForm
    options:
      children:
        - type: component.dropdown
          instanceId: selectCalendar
          options:
            label: Select Calendar
            data: =@ctx.datasources.list-calendars-rest
            isMultiple: true
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.id
  
  - type: component.list
    options:
      data: =@ctx.datasources.list-events-by-calendar
      maximumItemsToRender: 8
      item: 
        type: component.list-item
        options:
         leftElement: 
           element: icon
           icon: event
         title: =@ctx.current.item.subject
         subtitle: =@ctx.current.item.importance

summary:
  children:
    type: component.summary
    options: 
      layout: counter
      value: =$count(@ctx.datasources.list-events-by-calendar)
      title: Number of events
```
{% endtab %}

{% tab title=" message = "hello world" puts message sync-dynamic-selected-rest" %}
```yaml
# Add the global action under actions folder and use selected in the array
# mapping. 
action: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities: |
      =$map(@ctx.action.parameters.selected, function($item) {
        $.{
          "entity": "events-from-calendar",
          "function": "get-calendar-event-list",
          "parameters": {
            "accessToken": "jigx.graph.oauth",
            "calendarId": $item.id
          }
        }
      })[]
# If using a single value as your input source your mapping would be 
# "calendarId": $item
parameters:
  selected: 
    type: object 
    required: true
```
{% endtab %}

{% tab title="get-calendar-event-list" %}
```yaml
# Rest function to get the calendars events 
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me/calendars/{calendarId}/events
parameters:
  $filter:
    location: query
    required: false
    type: string
  $top:
    location: query
    required: false
    type: string
    value: 100
  accessToken:
    location: header
    required: true
    type: string
    value: jigx.graph.oauth
  calendarId:
    location: path
    required: true
    type: string  
outputTransform: $
continuation:
  parameters:
    accessToken:
      location: header
      required: true
      type: string
      value: jigx.graph.oauth
  url: =$."@odata.nextLink"
  when: =$."@odata.nextLink" 
records: =$.value
useLocalCall: true
```
{% endtab %}
{% endtabs %}
