# set-active-tab

Programmatically set the next active tab to display in the [jig.tabs](<./../Jig Types/jig_tabs.md>). The action determines which tab will open next. For example, if you are on the third tab, the action button can be set to open the first tab.

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure**  |                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `Action Identifier` | Give the action a unique name that will be used to reference the action in another jig's action. See the example below. |
| `id`                | Provide the `jigId` for the jig that will be opened next.                                                               |

| **State configuration** | **Key**         | **Notes**                                                             |
| ----------------------- | --------------- | --------------------------------------------------------------------- |
| `=@ctx.jig.state.`      | `initialTabId`  | A state variable used to reference the tab designated as the default. |
| `=@ctx.jig.state.`      | `activeTabId`   | A state variable that references the currently active tab.            |

## Considerations

- The `action.set-active-tab` can only be used in [jig.tabs](<./../Jig Types/jig_tabs.md>).
- The `action.set-active-tab` needs to be referenced as a callback action which is used in conjunction with the `action.execute-action`.

## How to configure the action

1. The action is configured under the `jigId` in the `jig.tabs` file. Give the action a unique name (`action identifier`) that will be used to reference the action in the tab's corresponding jig.
2. In the corresponding jig configure the `action.execute-action` and specify the unique name (`action identifier`)  in the action property's value.

## Examples and code snippets

### Basic set active tab

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-v9n12mYoxQdQcvO9V0ehS-20250212-115144.gif" size="70" position="center" caption="Set next active tab" alt="Set next active tab" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-v9n12mYoxQdQcvO9V0ehS-20250212-115144.gif"}
:::

:::VerticalSplitItem
In this example, when you are on the third tab (timelogs), a `Next Appointment` button at the bottom of the screen will open the first tab (appointments).
**Note:** The `action.set-active-tab` works in conjunction with `action.execute-action` using an `action identifier`.
:::
::::

:::CodeblockTabs
jig.tabs.jigx

```yaml
type: jig.tabs
title: Global INC
areTabsScrollable: false

children:
  - jigId: appointments
    title: Today
    icon: calendar-3
  - jigId: inventory
    title: Stock
    icon: supply-chain-shipping-fee-included-truck
  - jigId: timelogs
    title: Logs
    icon: time-clock-circle-1-alternate    
    actions:
      # Give the action a unique identifier. 
      # In the main jig use this identifier in the action.execute-action.
      # This creates the action button on the main jig 
      # to trigger the action.
      next-appointment: 
        type: action.set-active-tab
        options:
          # Set the next tab that will open programatically,
          # when the action button is tapped in the timelogs jig.
          # The id is the jigId of the tab you want to open next.   
          id: appointments
  - jigId: manuals
    title: Help   
    icon: book-book-pages
```

timelogs.jigx

```yaml
title: Time logging
description: Log the time taken to complete the job
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1456574808786-d2ba7a6aa654?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8dGltZSUyMGxvZ3xlbnwwfHwwfHx8Mg%3D%3D

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
      # To trigger the action.set-active-tab in the jig.tabs.jigx,
      # configure an action button to execute the action.
      # This button displays on the bottom of the jig,
      # when tapped it will open the next appointment tab. 
      - type: action.execute-action
        options:
          title: Next appointment
          # Reference the action identifier configured in the jig.tabs.
          action: next-appointment            


:::
