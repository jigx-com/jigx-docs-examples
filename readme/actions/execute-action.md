# execute-action

Using the `execute-action` action provides greater control and enables reuse when the same logic needs to be performed in multiple places. For example, `action.sync-entities` might be called during app initialization, again when data changes, or when only a specific subset of data needs to be synced. By using `execute-action`, you can easily reuse the granular actions that handle the actual work, reducing duplication and improving maintainability.  For more information, see [Global Actions](https://docs.jigx.com/building-apps-with-jigx/ui/actions#global-actions).

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
Configure the action property by selecting the global action file from the list of available global action files. The `when:` property can be used to determine when the global action must execute in a jig.
{% endstep %}
{% endstepper %}

{% include "../../.gitbook/includes/common-action-properties.md" %}

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
