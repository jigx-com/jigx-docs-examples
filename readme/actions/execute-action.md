# execute-action

Using `execute-action` gives you a reusable way to run global actions from jigs, events, and other actions. Use it when the same logic must run in multiple places, or when you need to call an action from another installed solution. For more information, see [Global Actions](https://docs.jigx.com/building-apps-with-jigx/ui/actions#global-actions).

***

## **How to configure execute-action**

{% stepper %}
{% step %}
Create a jigx file under the `actions` folder.
{% endstep %}

{% step %}
Auto-completion pops up with the list of available actions. Select the required action and configure the properties' values.
{% endstep %}

{% step %}
Use expressions to configure global options such as actions, expressions, and datasources.
{% endstep %}

{% step %}
Call the global action in a jig or index.jigx. Open the jig where you want to call the global action.
{% endstep %}

{% step %}
Use IntelliSense to list the available actions and select the **Execute Action** option `action.execute-action`.
{% endstep %}

{% step %}
Configure the `action` property by selecting the global action file from the list of available global action files. The `when:` property can be used to determine when the global action must execute in a jig. Add `package` to call a global action from another installed solution. Both `action` and `package` accept fixed values or expressions.
{% endstep %}
{% endstepper %}

{% include "../../.gitbook/includes/common-action-properties.md" %}

## Cross-solution action access

Use the `package` property to run a global action from another installed solution. This follows the same cross-solution pattern used for datasources. See [Cross solution datasource access](../datasource/cross-solution-datasource-access.md).

Both `action` and `package` accept expressions. This lets you resolve the target solution and global action at runtime.

## Examples and code snippets

{% tabs %}
{% tab title="global-sync.jigx" %}
```yaml
action:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: customers
        function: new-rest-get-customers
```
{% endtab %}

{% tab title="index.jigx" %}
```yaml
onLoad:
  type: action.execute-action
  options:
    action: load-data
```
{% endtab %}

{% tab title="cross-solution-action.jigx" %}
```yaml
actions:
  - children:
      - type: action.execute-action
        options:
          title: Assign employee
          # Provide the name of the other solution where the action is located. 
          package: human-resources
          action: assign
          parameters:
            employee_id: =@ctx.components.employee-select.state.selected.id
            project_name: =@ctx.components.project-select.state.selected.project_name
```
{% endtab %}

{% tab title="function-error.jigx" %}
```yaml
error:
  - when: =@ctx.response.status = 403
    notification: true
    alert:
      title: Error syncing customer list
      description:
        Error syncing customers, our system is temporarily unavailable.
        Please try again.
      presentAs: modal
      icon: synchronize-arrows-1
      style:
        isWarning: true
      # Configure an action to retry the GET or cancel and go back to the list or form.
      actions:
        - type: action.execute-action
          options:
            title: Load Customers
            action: load-data
        - type: action.go-to
          options:
            title: Cancel
            linkTo: new-customer-hr1
```
{% endtab %}

{% tab title="list-customers.jigx" %}
```yaml
onRefresh:
  type: action.execute-action
  options:
    action: load-data
```
{% endtab %}
{% endtabs %}
