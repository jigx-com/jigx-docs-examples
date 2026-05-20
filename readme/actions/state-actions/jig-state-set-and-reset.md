# jig-state (set & reset)

Use actions to set or reset various jig states. These operations affect screen-specific data, enabling dynamic UI updates and logic control. Proper state management ensures consistent behavior and data updates across the screen.

The `set-jig-state` action updates a jig’s state value, acting as a variable accessible within the current jig instance.\
The `reset-jig-state` action restores one or more jig states to their initial values.

Refer to [state](https://docs.jigx.com/building-apps-with-jigx/logic/state) for more information on the various state options and their respective functionality.

## Configuration options

A `set-jig-state`  or `reset-jig-state` actions can be set up in various ways, either by using an event or an action button to trigger the change:

* `onFocus` — executes the action when the screen gains focus.
* `onRefresh` — executes the action when the screen is refreshed.
* As the main action on the jig, and when you press the action, the `set-jig-state`  or `reset-jig-state` action will be executed. The `onPress` and `onChange` events will be executed when you trigger these events.

{% include "../../../.gitbook/includes/common-action-properties.md" %}

<table><thead><tr><th width="170.67578125">Core structure</th><th></th></tr></thead><tbody><tr><td><code>changes</code></td><td>Specify the jig-state's <code>State Key</code> and provide the new state value using an expression, text or datasource.</td></tr><tr><td><code>title</code></td><td>Provide the action button with a title, for example, Submitted.</td></tr></tbody></table>

<table><thead><tr><th width="171.62890625">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Select an <a href="https://docs.jigx.com/jigx-icons">icon</a> to display when the action is configured as the secondary button or in a header action.</td></tr><tr><td><code>isHidden</code></td><td><code>false</code> hides the action button, <code>true</code> shows the action button. Default setting is <code>true</code>.</td></tr><tr><td><code>style</code></td><td><code>isDanger</code> - Styles the action button in red or your brand's designated danger color. <code>isDisabled</code> - Displays the action button as greyed out. <code>isPrimary</code> - Styles the action button in blue or your brand's designated primary color. <code>isSecondary</code> - Sets the action as a secondary button, accessible via the ellipsis. The <code>icon</code> property can be used when the action button is displayed as a secondary button.</td></tr></tbody></table>

## How to configure a jig state

{% stepper %}
{% step %}
At the top of the jig file, configure the  `states`  property by defining the state's variable key name and  initial values of the jig screen.
{% endstep %}

{% step %}
Within the jig configure the `set-jig-state` action either in an event, such as `onPress`, or in the `action` property.
{% endstep %}

{% step %}
Use the `reset-jig-state`  action to reset the jig states to its `initialValue`.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="state" %}
```yaml
title: Dashboard
type: jig.default

state:
  status:
    initialValue: inactive
```
{% endtab %}

{% tab title="set-jig-state" %}
```yaml
actions:
  - numberOfVisibleActions: 2
    children:
      - type: action.set-jig-state
        options:
          changes:
            status: active
          title: Update status
```
{% endtab %}

{% tab title="reset-jig-state" %}
```yaml
onRefresh:
  # Set the state back to the initialValue of inactive
  type: action.reset-jig-state
  options:
    changes:
      - status
```
{% endtab %}
{% endtabs %}

## Examples and code snippets

{% columns %}
{% column %}
This example demonstrates an inspection checklist that uses the jig's state to track when the checklist is complete. Two key state variables are used:

* `checksStarted`: Tracks if the inspection has started (starts as `false`)
* `checksCompleted`: Tracks if all checks are finished (starts as `false`)

Tapping on the choice-fields sets the jig's `checksStarted` state to `true` .

Tapping the _Inspection Complete_ button sets the jig's `checksCompleted` state to `true`. This single state change triggers three things automatically:

* All checkboxes become disabled (you can't change them anymore)
* A success banner appears at the top
* The complete button is hidden

To reset the jig states to their initial values, reset actions run when you:

* Navigate back to the jig (`onFocus`)
* Pull down to refresh (`onRefresh`)

Both actions reset the state variables, so you can start fresh each time.
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/actions-set-reset-jig-state (2).gif" alt="Set and reset jig state"><figcaption><p>Set and reset jig state</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="inspection-checklist.jigx" %}
```yaml
title: Inspection tasks
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri:
              https://cdn.pixabay.com/photo/2025/04/25/09/49/ai-generated-9558304_640.jpg
# State management for the jig, define the initial values of the jig state          
state:
  checksStarted:
    initialValue: false
  checksCompleted:
    initialValue: false
# Actions to perform when the jig comes into focus.
onFocus:
  type: action.action-list
  options:
    isSequential: true
    actions:
     # Reset the jig state variables to their initial values.
      - type: action.reset-jig-state
        options:
          changes:
            - checksStarted
            - checksCompleted
      # Reset the checklist form data (uncheck all checkboxes).      
      - type: action.reset-state
        options:
          state: =@ctx.components.checklist.state.data
# Actions to perform when user pulls to refresh.
onRefresh:
  type: action.action-list
  options:
    isSequential: true
    actions:
      # Reset the jig state variables to their initial values.
      - type: action.reset-jig-state
        options:
          changes:
            - checksStarted
            - checksCompleted
      # Reset the checklist form data (uncheck all checkboxes).    
      - type: action.reset-state
        options:
          state: =@ctx.components.checklist.state.data

children:
  # Banner shows only when inspection is completed
  - type: component.banner
    # Success banner that appears when all checks are completed, 
    # determined by evaluating the jig state variable - checksCompleted.
    when: =@ctx.jig.state.checksCompleted = true
    options:
      title: "Checks completed"
      subtitle: "Remember to record time and materials used."
      style:
        isPositive: true
      leftElement:
        element: icon
        icon: check-2
        type: duotone
  # Form component containing the checklist.
  - type: component.form
    # Unique identifier for referencing this form.
    instanceId: checklist
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.choice-field
          instanceId: choice
          options:
            label: Checklist
            data: =@ctx.datasources.checklist-items
            item:
              type: component.choice-field-item
              options:
                title: =@ctx.current.item.title
                value: =@ctx.current.item.id
            # Setting jig state to indicate checks have started when checkbox is checked    
            onChange:
              type: action.set-jig-state
              options:
                changes:
                  checksStarted: true
            isRequired: true
            isMultiple: true
            # Disable choice boxes when the state is checksCompleted
            style:
              isDisabled: =@ctx.jig.state.checksCompleted = true
actions:
  - numberOfVisibleActions: 1
    # Set the jig state when all 3 checklist items are selected
    when: =$count(@ctx.components.choice.state.selected.id) = 3
    children:
      - type: action.set-jig-state
        options:
          title: Inspection Complete
          # Show the action button only when all 3 items are checked
          isHidden: =$count(@ctx.components.choice.state.selected.id) !=3
          # Set checksCompleted to true when button is pressed.
          changes:
            checksCompleted: true
```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  checklist-items:
    type: datasource.static
    options:
      data:
        - id: 1
          title: "Inspect equipment"
        - id: 2
          title: "Gather materials"
        - id: 3
          title: "Complete task report"
```
{% endtab %}
{% endtabs %}
