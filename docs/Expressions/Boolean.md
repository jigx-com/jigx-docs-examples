# Boolean

Within JSONata there are two types of Boolean expressions used to find out whether the result is true or false, namely:

1. [Boolean operators](https://docs.jsonata.org/boolean-operators) that include `and`, `or`
   [Boolean functions](https://docs.jsonata.org/boolean-functions) that include:
   - [$boolean()](https://docs.jsonata.org/boolean-functions#boolean)
   - [$not()](https://docs.jsonata.org/boolean-functions#not)
   - [$exists()](https://docs.jsonata.org/boolean-functions#exists)

## Configuration

| **Result**                                                               | **Expression**                                                                          |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| (And)&#xA;Does the array of data contain both a name and an image?       | `=$boolean(@ctx.datasources.employees.name and @ctx.datasources.employees.img)`         |
| (Or)&#xA;Does the array of data contain a phone number or email?         | `=$boolean(@ctx.datasources.employees.phoneNumber or @ctx.datasources.employees.email)` |
| (If value =)&#xA;If the name of the employee is "Mary Gomez", set true   | `=@ctx.datasources.employee.name = "Mary Gomez" ? true :false`                          |
| (If value \<)&#xA;If the age of an employee is smaller than 20 set true. | `=@ctx.datasources.employee.age < 20 ? true :false`                                     |
| (If array >)&#xA;Does the array of data contain more than two objects?   | `=$count(@ctx.datasources.employees) > 2 ? true :false `                                |

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets

### Evaluating fields

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Boolean expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IB2sIUMi98vlAC-8zpawb_booleaniphone13blueportrait.png "Boolean expression")
:::

:::VerticalSplitItem
This example evaluates static data in a `component.enity` to show the results in the entity field as a `boolean`.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/boolean.jigx).
:::
::::

:::CodeblockTabs
boolean.jigx

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Does the array of data contain both a name and an image? (And)
            value: =$boolean(@ctx.datasources.employees.name and @ctx.datasources.employees.img)
        - type: component.entity-field
          options:
            label: Does the array of data contain a phone number or email? (Or)
            value: =$boolean(@ctx.datasources.employees.phoneNumber or @ctx.datasources.employees.email)
        - type: component.entity-field
          options:
            label: If name of employee is "Mary Gomez", set true. (If value =)
            value: =@ctx.datasources.employee.name = "Mary Gomez" ? true :false
        - type: component.entity-field
          options:
            label: If age of employee is smaller than 20 set true. (If value <)
            value: =@ctx.datasources.employee.age < 20 ? true :false
        - type: component.entity-field
          options:
            label: Does the array of data contain more than two objects? (If array >)
            value: =$count(@ctx.datasources.employees) > 2 ? true :false 
```
:::

### Placeholder

:::::VerticalSplit{layout="right"}
::::VerticalSplitItem
Example of writing a condition for a placeholder. If the number of objects in the array is greater than zero, the placeholder is not displayed. If it isn't and the field is empty, a placeholder will appear with the icon and the specified text.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/placeholder.jigx).

See [tips and tricks when using placeholders](https://community.jigx.com/t/tips-tricks-use-placeholders/78) for additional information.

:::CodeblockTabs
placeholder.jigx

```yaml
placeholders:
  - when: =$count(@ctx.datasources.employees-dynamic) > 0 ? false :true 
    title: There is no data
    icon: missing-data
    
```
:::
::::

:::VerticalSplitItem
![Placeholder](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XMqGfRfgof-WsZJq6qYtE_placeholderiphone13blueportrait.png "Placeholder")
:::
:::::

