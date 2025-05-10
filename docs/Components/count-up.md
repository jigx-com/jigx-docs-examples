---
title: count-up
slug: MiC0-c
createdAt: Tue Mar 18 2025 19:13:12 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 07 2025 07:09:19 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The count-up component is a display-only component that continuously updates in real-time to show the elapsed time since a given start timestamp.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-nW6zJJxYorLEl2_vVUe8H-20250319-072422.png" size="60" position="center" caption="Count-up" alt="Count-up"}


:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure**|                                                                                                                                           |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `startTimestamp`   | Add a start date, date/time or time , either using:&#xA;- datasource, e.g. `=@ctx.datasources.events[1].date`&#xA;- expression, e.g. `=$fromMillis($toMillis($now()) + 50000)`&#xA;- string, e.g. `"2023-09-20 18:00"`, or `"2023-07-25T17:30:00+02:00"`<br />If `startTimestamp` is omitted or set to null, the component remains static and does not count up. |

| **Other options** |                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `labels`          | The count-up label displays time in the format Days: Hours: Minutes: Seconds. The Days section appears only when the timer exceeds 24 hours.&#xA;Configuration options are:&#xA;- `isVisible` (default: `true`)- Controls visibility of the count-up labels. Setting it to `false` hides the labels.&#xA;- `position` - Determines whether the count-up labels (Days: Hours: Minutes: Seconds) appear at the top or bottom of the count-up display. |
| `size`            | Choose between `extra-large` and `medium` sizes, with `extra-large` as the default if the property is not specified in the YAML.                |

## Examples and code snippets 

:::::ExpandableHeading
### Count-up basic

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows how to set up a basic `count-up` component that starts counting from the current moment.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-nW6zJJxYorLEl2_vVUe8H-20250319-072422.png" size="60" position="center" caption="Count-up" alt="Count-up"}
:::
::::

:::CodeblockTabs
count-up-basic.jigx

```yaml
title: Basic count-up
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2024/10/02/18/24/ai-generated-9091889_640.jpg

children:
 - type: component.count-up
    options:
      # Set labels showing hours, minutes and seconds to visible.
      labels:
        isVisible: true
        # Position the labels under the count-up component.
        position: bottom
      # Set the required size of the component.  
      size: extra-large
      # Provide the start time.
      startTimestamp: =$now()
```
:::
:::::

:::::ExpandableHeading
### Count-up sizes and lables

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-FzoIGzYYYvnodUOpxXzJF-20250319-110311.png" size="60" position="center" caption="Count-up in varying sizes" alt="Count-up in varying sizes"}
:::

:::VerticalSplitItem
This example displays two `count-up` components of different sizes. The first is `extra-large`, with `labels` `positioned` above it, while the second is `medium`-sized with `labels` below.
:::
::::

:::CodeblockTabs
count-up-sizes.jigx

```yaml
title: Count-up sizes and labels
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2018/09/24/08/16/stopwatch-3699317_640.jpg

children:
  - type: component.section
    options:
      title: Count-up - EXTRA LARGE WITH TOP LABELS 
      children:
      - type: component.count-up
        options:
          labels:
            isVisible: true
            # Position the labels (Hours : Minutes: Seconds) above the component. 
            position: top
          # Set the component's size as extra-large.  
          size: extra-large
          # Start time defined in ISO format converted to milliseconds.
          startTimestamp: =$toMillis('2025-03-19T10:43:04.377Z')
            
  - type: component.section
    options:
      title: Count-up - MEDIUM WITH BOTTOM LABELS 
      children:
      - type: component.count-up
        options:
          labels:
            isVisible: true
            # Position labels (Days: Hours : Minutes: Seconds) below the component. 
            position: bottom
           # Set the component's size as medium.   
          size: medium
          # Start time defined in ISO format converted to milliseconds.
          startTimestamp: =$toMillis('2025-03-06T23:00:00Z')
              
```
:::
:::::

:::::ExpandableHeading
### Count-up using a datasource

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example showcases two `count-up` components using a datasource with timestamp records in ISO format and milliseconds. The first component uses the millisecond timestamp, while the second uses the ISO format timestamp.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ZNs61T_KydUti3vw3y1gc-20250319-110401.png" size="60" position="center" caption="Start time defined in a datasource" alt="Start time defined in a datasource"}
:::
::::

:::CodeblockTabs
count-up-datasource.jigx

```yaml
title: Count-up using datasource
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2018/03/07/13/28/stopwatch-3205980_640.jpg

datasources:
  time:
    type: datasource.static
    options:
      data:
        - id: 1
          timeStamp: 1742380984000
          type: millis
        - id: 2
          timeStamp: 2025-03-06T23:00:00Z
          type: ISO

children:
  - type: component.section
    options:
      title: Count-up - datasource start time in millis 
      children:
      - type: component.count-up
        options:
          # Start time defined in milliseconds in a datasource.
          startTimestamp: =@ctx.datasources.time[0].timeStamp
  - type: component.section
    options:
      title: Count-up - datasource start time in ISO format 
      children:
      - type: component.count-up
        options:
          # Start time defined in ISO format in a datasource converted to milliseconds.
          startTimestamp: =$toMillis(@ctx.datasources.time[1].timeStamp)

```
:::
:::::

:::::ExpandableHeading
### Count-up using state in a when condition

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![count-up condition](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-gTZBlyV4cONAWWhje5ule-20250319-124254.png "Count-up condition")
:::

:::VerticalSplitItem
This example demonstrates how to use the jig `state` in a `when` property to initially hide the `count-up` component and reveal it when a start `button` is pressed within a `list-item`.
:::
::::

:::CodeblockTabs
count-up-expression.jigx

```yaml
title: Count Up 
type: jig.default

# Reset the jig state to the initial values when the jig is refreshed.
onRefresh: 
  type: action.reset-jig-state
  options:
    changes: 
      - startTime
# Reset the jig state to the initial values when the jig comes into focus.
onFocus: 
  type: action.reset-jig-state
  options:
    changes: 
      - startTime
# Set initial states in the jig.      
state:
  startTime: 
    initialValue: Start
    
header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2019/01/15/09/36/stopwatch-3933687_640.jpg

children:
  - type: component.list-item
    instanceId: repair1
    options:
      title: Repair brickwork
      subtitle: Job starts when you select the appointment from the list
      leftElement: 
        element: icon
        color: color4
        isContained: true
        icon: hammer
      # Configure a button with the onPress event to,
      # start the job by setting the state to 'In Progress'.  
      rightElement: 
        element: button
        title: =@ctx.jig.state.start
        onPress: 
         type: action.set-jig-state
         options:
            changes:
              startTime: In progress
  - type: component.list-item
    instanceId: install
    options:
      title: Install new HVAC
      subtitle: Job starts when you select the appointment from the list
      leftElement: 
        element: icon
        color: color9
        isContained: true
        icon: fan
      tags:
        - text: Complete
          color: color2
                        
  - type: component.count-up
    instanceId: workTime
    # Set the when condition to determine when the count-up is visible.
    # The count-up starts using the timestamp provided once it is visible.
    when:  =@ctx.jig.state.start = "In progress"
    options:
      startTimestamp: =$millis() - 10000
```
:::
:::::

