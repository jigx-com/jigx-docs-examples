# submit-form

The action can be used on a form to save data into any of the [data](https://docs.jigx.com/aI2F-data) types (check out [Forms](#) to learn more about forms). `submit-form` has to be used on a <a href="https://docs.jigx.com/examples/jigdefault" target="_blank">default jig</a> with the [form](./../Components/form.md) component. A typical use case of submit-form is saving or updating the records in a table.

The `submit-form` action can be set up as a primary action on default jig with a form component

1. Your jig type has to be jig.default
2. Action must be submit-form with the title of the button, and you need to specify: the id of the form that you want to save, provider, entity, method and if you are using SQL, REST, SALESFORCE, SOAP you need to specify the function that you are calling.
3. On the default jig you need to create a component. form, the instance Id, which will be the id of the form.
4. You can use the form's components in the form, and the instanceId of each component will be the name of the column of the data row that will be saved.

## Offline remote data handling

Dealing with offline remote data is fundamental to ensuring data synchronization and consistency between the mobile app and the remote data source, allowing users to continue using the app and performing actions without interruption. [Offline remote data handling](#) explains how to configure solutions to deal with data when the device is offline using the `queueOperations` property available in execute-entities and provides examples and code samples.

## Examples and code snippets&#x20;

::::ExpandableHeading
### submit-form example

Example of submit-form to save a new employee into the dynamic-data table. The first name, last name, and phone number will be saved in the employees' data table.

**Example:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/submit-form/dynamic-data/submit-form.jigx)

:::CodeblockTabs
submit-form.jigx

```yaml
actions:
  - children:
      - type: action.submit-form
        options:
          formId: simple-form
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/employees
          method: save
          title: Save person

children:
  - type: component.form
    instanceId: simple-form
    options:
      children:
        - type: component.text-field
          instanceId: firstname
          options:
            label: First name
        - type: component.text-field
          instanceId: lastname
          options:
            label: Last name
        - type: component.text-field
          instanceId: phone
          options:
            label: Phone number
            keyboardType: decimal-pad
```
:::
::::

