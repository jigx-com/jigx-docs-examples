---
title: jig.tabs
slug: JU-M-jig
createdAt: Thu Jan 09 2025 07:54:55 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu May 01 2025 11:25:00 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Tabs allow you to navigate between different jigs with ease, enhancing the user experience by providing an organized layout. These tabs are placed at the top of the screen to ensure a sleek and intuitive interface.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-OMOVs8U637zq2E_iRppiL-20250206-182545.gif" size="66" position="center" caption="Tabs " alt="Tabs "}
:::
::::

## Configuration options

Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

The `jig.tabs` can be configured in the following way in Jigx Builder.

| **Core structure** |                        |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Give the jig a title that is displayed at the top of the screen.                                                               |
| `type`             | Select `jig.tabs`.        |
| `jigId`            | Provide the `jigId` for the jig that will be displayed when the tab is active.                                                |
| `instanceId`       | Give the tab a unique identifier, that can be used in expressions.                                                            |
| `tab`              | - `title` - The text that displays as the tab name.
- `icon` - Add an icon to display in the tab. A list of available icons can be found in  [Jigx icons](). The `title` appears below the `icon` in the tab.&#x20;
- `badge` - Add a badge to display on the tab to highlight critical information. The badge can be configured at the root level of the jig file. The badge can be configured with an `icon`, `color`, and a `value`. |

| **Other options**   |                                                            |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `areTabsScrollable` | When there are many tabs that exceed the width of the screen, set the property to `true` to scroll and view the additional obscured tabs by swiping left. Setting the property to `false` will only display the tabs that fit on the width of the screen, additional tabs will be hidden. The property is accessible using IntelliSense at the root level in the YAML. By default tabs are scrollable.&#xA;Tip: Using areTabsScrollable: false will align the tabs in the center. |
| `inputs`            | Used to pass data between the jigs in the tabs to provide context and data. See [Passing data using inputs]() for more information.                                   |
| `instanceId`        | Give the tab a unique identifier allowing you to reference the tab in expressions in jigs.                                                                           |
| `initialTabId`      | Specify the tab to display when the jig opens. The tab's `jigId` is used as the value. This property is accessible via IntelliSense at the root level in the YAML. If not specified, the first tab is displayed by default.                                                |
| `isDisabled`        | If `true` you won't be able to toggle the tabs. The default value is `false`.                                                                                          |
| `isSwipeable`       | Set to `true` allows you to navigate between tabs by swiping left and right anywhere on the jig. By default tabs are not swipeable and require you to press on the tab title for navigation.                                                                             |
| `when`              | This property is used to show/hide any tab based on conditions, such as true, false, or conditions set using an expression.                                           |

| **Actions**|                  |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actions`   | The `actions` property is a local action applicable to the specific tab. Once the tab is tapped the action will execute.<br />* `Action Identifier` - Provide a unique name that is used to identify the action.* `Action Identifier` - Provide a unique name that is used to identify the action.* `type` - Select the [action](./../Actions.md)  that is triggered in the specific tab. Use IntelliSense to see the available list of actions.<br />See the [Tabs with actions]() code example below.  |

| **State Configuration** | **Key**     | **Notes**                                              |
| ----------------------- | ----------- | ------------------------------------------------------- |
| `=@ctx.jig.state.`      | activeTabId | Applies to the active tab in the `jig.tab` type.        |
| `=@ctx.solution.state.` | tab         | Global variable for the tab used throughout a solution. |

## Considerations

- Specifying a background color for tabs is currently not supported.
- `jig.headers` do not display in the children tabs.
- Using `areTabsScrollable: false` aligns the tabs in the center, aligns the tabs at the center, enhancing visual consistency.

## Examples and code snippets 

:::::ExpandableHeading
### Basic tabs

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-gXY6EX-Uq2C9RtFI5kPcb-20250206-181546.gif" size="66" position="center" caption="Basic tab jig" alt="Basic tab jig"}
:::

:::VerticalSplitItem
This example demonstrates the simplest use of the `jig.tabs`. Four tabs are configured, each opens the corresponding jig.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-basic.jigx).
Supporting jig samples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/supporting-jigs).
:::
::::

:::CodeblockTabs
jig-tabs-basic.jigx

```yaml
# Select the jig type tabs.
type: jig.tabs
title: Global INC
# Aligns the tabs at the center, enhancing visual consistency.
areTabsScrollable: false

children:
  # Specify the jig that will open when the tab is pressed.
  # Tab 1
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
        # Give the tabs a name,you can use an expression, datasource or text. 
        title: Today  
  # Tab 2        
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Stock
  # Tab 3      
  - jigId: timelogs
    tab:
      type: component.tab-button
      options: 
        title: Logs
  # Tab 4  
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: Help   
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-basic
    icon: home-apps-logo
```

appointments.jigx

```yaml
# Supporting jig - First tab corresponding jig
title: Today
description: My appointments for today
type: jig.default

datasources:
  appointments: 
    type: datasource.static
    options:
      data:
        - id: 1
          time: 8:00am
          customer: Jay Motors
          address: 13 Sunnydale Road
        - id: 2
          time: 11:30am
          customer: Elementary School
          address: 1 Harold Street
        - id: 3
          time: 8:00am
          customer: Becker Consulting
          address: Suite A, Tower building, Main street  
children:
  - type: component.form
    instanceId: schedule-appt
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.choice-field
          instanceId: appointment
          options:
            label: Today
            data: =@ctx.datasources.appointments
            item:
              type: component.choice-field-item
              options:
                title: =@ctx.current.item.customer
                value: =@ctx.current.item.address
```

inventory.jigx

```yaml
# Supporting jig - Second tab's corresponding jig
title: Inventory
description: Select the parts required for the job
type: jig.list

datasources:
  inventory: 
    type: datasource.static
    options:
      data:
        - id: 1
          item: Compressor 
        - id: 2
          item: Condenser Coil 
        - id: 3
          item: Refrigerant 
        - id: 4 
          item: Expansion Valve 
        - id: 5
          item: Fan Motor                        

data: =@ctx.datasources.inventory
item:
  type: component.list-item
  options:
    leftElement: 
      element: icon
      icon: tool-organizer-1
      isDuotone: true
    title: =@ctx.current.item.item
    
```

timelogs

```yaml
# Supporting jig - Third tab's corresponding jig
title: Time logging
description: Log the time taken to complete the job
type: jig.default

onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.components.shift-form.state.data
    
children:
  - type: component.form
    instanceId: shift-form
    options:
      children:
        - type: component.number-field
          instanceId: employee-number
          options:
            label: Employee number
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: Name
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last Name   
        - type: component.email-field  
          instanceId: email
          options:
            label: Email  
        - type: component.text-field
          instanceId: contact
          options:
            textContentType: telephoneNumber
            label: Contact number
        - type: component.field-row
          options:
            children:
              
              - type: component.date-picker
                instanceId: shift-date
                options:
                  label: Select shift date 
              - type: component.duration-picker
                instanceId: shift-duration
                options:
                  label: Log your shift duration
                  initialValue: 14400
                  helperText: Standard shift is 4 hours 
                  errorText: =@ctx.component.state.value > 14400 ? 'Shift time needs approval':'' 
                  hours:
                    step: 4
                  minutes:
                    step: 2  
                    
actions:
  - children:
      - type: action.execute-entity 
        options:
          title: Log job time
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/work
          method: create
          data:
            employee-number: =@ctx.components.employee-number.state.value
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            contact:  =@ctx.components.contact.state.value
            shift-date: =@ctx.components.shift-date.state.value
            shift-duration: =@ctx.components.shift-duration.state.value  
```

manuals.jigx

```yaml
# Supporting jig - Fourth tab's corresponding jig
title: HVAC manual
type: jig.document

source:
  documentType: PDF
  uri: https://s28.q4cdn.com/392171258/files/doc_downloads/test.pdf
```
:::
:::::

:::::ExpandableHeading
### Scrollable tabs

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-lBrVY3woIBnimDwWulEHH-20250110-093815.gif" size="66" position="center" caption="Scrollable tabs" alt="Scrollable tabs"}
:::

:::VerticalSplitItem
This example shows the `jig.tabs` with ten tabs. Tab8, Tab9, and Tab10 are not visible. Setting the  the `areTabsScrollable: true` property enables scrolling on the tab bar.  Each tab opens the corresponding jig when pressed.  For demonstration purposes placeholder jigs are used.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-scrollable.jigx).
Supporting jig samples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/supporting-jigs).
:::
::::

:::CodeblockTabs
jig-tabs-scrollable.jigx

```yaml
# Select the jig type tabs.
type: jig.tabs
title: Global INC
# For multiple tabs that run over the screen, the property enables the tabs to be scrolled.
areTabsScrollable: true

children:
  # Specify the jigs that will open when the tabs are pressed.
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
       title: Tab 1
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Tab 2
  - jigId: timelogs
    tab:
      type: component.tab-button
      options:
        title: Tab 3
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: tab 4          
  - jigId: tab-placeholder
    tab:
      type: component.tab-button
      options:
        title: Tab 5  
  - jigId: tab-placeholder1
    tab:
      type: component.tab-button
      options:
        title: Tab 6  
  - jigId: tab-placeholder2
    tab:
      type: component.tab-button
      options:
        title: Tab 7  
  - jigId: tab-placeholder3
    tab:
      type: component.tab-button
      options:
        title: Tab 8  
  - jigId: tab-placeholder4
    tab:
      type: component.tab-button
      options:
        title: Tab 9  
  - jigId: tab-placeholder5
    tab:
      type: component.tab-button
      options:
        title: Tab 10   
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-scrollable
    icon: home-apps-logo
```

tab-placeholder.jigx

```yaml
# This jig is create the base for the placeholder jigs in this example. 
# Duplicate the jig to create the required placeholder jigs. 
title: Placeholder 
description: This screen is a placeholder for demo purposes
type: jig.default

placeholders:
  - title: No data to display
    icon: missing-data
    
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: ' '
            value: ' '
```
:::
:::::

:::::ExpandableHeading
### Swipeable tabs

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-UdPtwouumvXFSZS6_4cU5-20250206-181844.gif" size="66" position="center" caption="Swipeable tabs" alt="Swipeable tabs tabs"}
:::

:::VerticalSplitItem
This example shows the `jig.tabs` with four tabs. Setting the `isSwipeable: true` property allows you to swipe left and right anywhere on the screen to navigate between the tabs instead of pressing on each tab title to display the jigs.  Each tab opens the corresponding jig.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-swipeable.jigx).


:::
::::

:::CodeblockTabs
jig-tabs-swipeable.jigx

```yaml
# Select the jig type tabs.
type: jig.tabs
title: Global INC
# Aligns the tabs at the center, enhancing visual consistency.
areTabsScrollable: false
# Enable swiping. Swipe left and right on the screen to navigate between tabs.
isSwipeable: true
# Specify the jigs that will open in each tab.

children:
  # Specify the jigs that will open when the tabs are pressed. 
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
        title: Today
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Stock
  - jigId: timelogs
    tab:
      type: component.tab-button
      options:
        title: Logs
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: Help               
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-swipeable
    icon: home-apps-logo
```
:::
:::::

:::::ExpandableHeading
### Tabs with initialTabId

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-fMURvK7rblWigmQqdUPWv-20250206-182207.png" size="66" position="center" caption="Initial tab specified" alt="Initial tab specified"}
:::

:::VerticalSplitItem
This example demonstrates the `jig.tabs` with the third tab (logs) set as the default (initial) tab displayed when the jig opens. The `initialTabId: timelogs` property specifies which tab will be in focus upon opening the jig. To specify the default jig use the `jigId` as the `initialTabId`'s value.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-intialtabid.jigx).


:::
::::

:::CodeblockTabs
jig-tabs-initialtabid.jigx

```yaml
# Select the jig type tabs.
type: jig.tabs
title: Global INC
# Aligns the tabs at the center, enhancing visual consistency.
areTabsScrollable: false
# Specify the jigId for the tab that must be displayed when the jig opens. 
initialTabId: timelogs

children:
  # Specify the jigs that will open in each tab. 
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
        title: Today
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Stock
  - jigId: timelogs
    tab:
      type: component.tab-button
      options:
        title: Logs
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: Help    
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-initialtabid
    icon: home-apps-logo
```
:::
:::::

:::::ExpandableHeading
### Tabs with icons

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-OMOVs8U637zq2E_iRppiL-20250206-182545.gif" size="66" position="center" caption="Tabs with icons" alt="Tabs with icons"}
:::

:::VerticalSplitItem
This example demonstrates the `jig.tabs` with the `icons`. The active tab's `icon` displays in the primary color.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-icons.jigx).

:::
::::

:::CodeblockTabs
jig-tabs-icons.jigx

```yaml
# Select the jig type tabs.
type: jig.tabs
title: Global INC
# Aligns the tabs at the center, enhancing visual consistency.
areTabsScrollable: false

# Specify the jigs that will open in each tab.
children:
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
       title: Today
       # Add an icon to the tab. The title is diplayed below the icon.
       # When active the icon uses the primary color.   
       icon: calendar-3
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Stock
        # Add an icon to the tab. The title is diplayed below the icon. 
        icon: supply-chain-shipping-fee-included-truck
  - jigId: timelogs
    tab:
      type: component.tab-button
      options:
        title: Logs
        # Add an icon to the tab. The title is diplayed below the icon.
        icon: time-clock-circle-1-alternate
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: Help
        # Add an icon to the tab. The title is diplayed below the icon.    
        icon: book-book-pages
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-icons
    icon: home-apps-logo
```
:::
:::::

:::::ExpandableHeading
### Tabs with inputs

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-MsVwU6nEEHgimuiowkBQ7-20250206-183000.gif" size="66" position="center" caption="Tabs with inputs" alt="Tabs with inputs"}
:::

:::VerticalSplitItem
This example demonstrates `jig.tabs` where the *Logs* tab is configured to use a jig with inputs. The input values are set within `jig.tabs` under the `jigId` of the corresponding jig.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-inputs.jigx).
Supporting jig samples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/supporting-jigs).

:::
::::

:::CodeblockTabs
jigx-tabs-inputs.jigx

```yaml
type: jig.tabs
title: Global INC
# Aligns the tabs at the center, enhancing visual consistency.
areTabsScrollable: false

# Specify the jigs that will open in each tab.
children:
  - jigId: appointments
    tab:
      type: component.tab-button
      options:
        title: Today
  - jigId: inventory
    tab:
      type: component.tab-button
      options:
        title: Stock
  - jigId: timelogs-inputs
    tab:
      type: component.tab-button
      options:
        title: Logs
    # The jig that displays in the tab has inputs defined. 
    # Provide the values for the inputs to the jig.      
    inputs:
      Name: =@ctx.user.displayName
      email: =@ctx.user.email
      contact: 1345632
  - jigId: manuals
    tab:
      type: component.tab-button
      options:
        title: Help 
```

timelogs-inputs.jigx

```yaml
title: Time logging
description: Log the time taken to complete the job
type: jig.default

onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.components.shift-form.state.data
# Specify the inputs that are needed in the jig.
inputs:  
  Name: 
    type: string
    required: true
  email: 
    type: string
    required: true
  contact: 
    type: number
    required: true
        
children:
  - type: component.form
    instanceId: shift-form
    options:  
      children:
        - type: component.text-field
          instanceId: Name
          options:
# Use the input provided in the jig.tab to display the initial value.          
            initialValue: =@ctx.jig.inputs.Name
            label: Name  
        - type: component.email-field  
          instanceId: email
          options:
# Use the input provided in the jig.tab to display the initial value.              
            initialValue: =@ctx.jig.inputs.email
            label: Email  
        - type: component.text-field
          instanceId: contact
          options:
# Use the input provided in the jig.tab to display the initial value.              
            initialValue: =@ctx.jig.inputs.contact
            textContentType: telephoneNumber
            label: Contact number
        - type: component.field-row
          options:
            children:
              - type: component.date-picker
                instanceId: shift-date
                options:
                  label: Select shift date 
              - type: component.duration-picker
                instanceId: shift-duration
                options:
                  label: Log your shift duration
                  initialValue: 14400
                  helperText: Standard shift is 4 hours 
                  errorText: =@ctx.component.state.value > 14400 ? 'Shift time needs approval':'' 
                  hours:
                    step: 4
                  minutes:
                    step: 2  
```

index.jigx

```yaml
name: work
title: work
category: business      
# Configure the jig containing the tabs to open on the home hub.
tabs:
  home:
    label: home
# Specify the jig to open when the home icon in the navigation bar is pressed.    
    jigId: jig-tabs-inputs
    icon: home-apps-logo
```
:::
:::::

:::::ExpandableHeading
### Set tab's content from a single jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-y_xWPxX2BR2mdsyMN72Ar-20250227-155626.gif" size="66" position="center" caption="Tabs using single tab" alt="Tabs using single tab"}
:::

:::VerticalSplitItem
This example demonstrates how to use a single jig to set the content for each tab by using the jig `inputs`.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/jig-tabs-content.jigx)
Supporting jig samples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-tabs/supporting-jigs).

:::
::::

:::CodeblockTabs
jig-tab-content

```yaml
type: jig.tabs
title: Time-tracking
isSwipeable: true
areTabsScrollable: false
initialTabId: week1
# Specify the single jig that will open in each tab.
# Use inputs to change the content in the tab.
Children:
  # Tab 1 
  # Note all the tabs use the same jigId. 
  - jigId: timecard
    instanceId: week1
    tab:
      type: component.tab-button
      options:
        title: Week 1 
        icon: number-one-circle
    # Provide the values for the inputs to the jig to display on the jig.     
    inputs:
      Team: HVAC Team
      shift: Day
      hours: 8
  # Tab 2 
  # Note all the tabs use the same jigId.  
  - jigId: timecard
    instanceId: week2
    tab:
      type: component.tab-button
      options:
        title: Week 2
        icon: number-two-circle
    # Provide the values for the inputs to the jig to display on the jig.      
    inputs:
      Team: Electrical Team
      shift: Night
      hours: 12
      color: color2
  # Tab 3 
  # Note all the tabs use the same jigId.     
  - jigId: timecard
    instanceId: week3
    tab:
      type: component.tab-button
      options:
        title: Week 3
        icon: number-three-circle  
    # Provide the values for the inputs to the jig to display on the jig.      
    inputs:
      Team: Plumbing Team
      shift: Split
      hours: 6
      color: color4
```

timecard.jigx

```yaml
title: Time-tracking
type: jig.default
# Define the inputs required in the jig, the content is set per tab.
inputs:
  Team: 
    type: string
    required: true
  shift: 
    type: string
    required: true
  hours:
    type: number
    required: true
    
children:
  - type: component.list-item
    instanceId: rotation
    options:  
      # Use the input provided in the jig.tab to display the title.   
      title: =@ctx.jig.inputs.Team
      # Use the input provided in the jig.tab to display the icon color.
      color: =@ctx.jig.inputs.color
      leftElement: 
        element: icon
        icon: multiple-man-woman-2-geometric-close-up
        isContained: true
  - type: component.list-item
    instanceId: work-day
    options:  
      # Use the input provided in the jig.tab to display the shift value.    
      title: =@ctx.jig.inputs.shift
      color: =@ctx.jig.inputs.color
      leftElement: 
        element: icon
        icon: calendar
        isContained: true
  - type: component.list-item
    instanceId: time
    options:  
      # Use the input provided in the jig.tab to display the hours worked.
      title: =@ctx.jig.inputs.hours 
      color: =@ctx.jig.inputs.color
      leftElement: 
        element: icon
        icon: time-clock-circle-1-alternate
        isDuotone: true
```
:::
:::::

