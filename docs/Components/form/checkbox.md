---
title: checkbox
slug: NI_e-checkbox
description: Learn how to effectively use the versatile checkbox component in your forms with this comprehensive document. Discover how to enable users to make binary choices and select single or multiple options. Explore options for configuring initial checked or unc
createdAt: Thu Jun 09 2022 19:27:06 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Oct 21 2024 12:43:07 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Checkboxes on mobile app forms offer a straightforward way to make selections, especially for multiple options, enhancing usability and interaction.

The component is used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component and supports single- and multiple-selection options. The checkbox's initial checkbox status and required checkbox status can be set.
:::

:::VerticalSplitItem
::Image[]{alt="Checkbox preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/C108AXi_xo5aRgmBnjo_9_checkboxes.png" size="90" caption="Checkbox preview" position="center" }
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

|**Core structure** |                                                                                                    |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| `instanceId`       | The unique identifier for the checkbox component.                                                        |
| `label`            | Provide a label/name for the checkbox. 'Label' is displayed as a placeholder when no value is specified. |

| **Other options**       |   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`                 | Sets the color of the checkbox based on conditions by using the when property. First evaluated to true will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette]().  |
| `errorText`             | Add text, string, or expressions to show text under the checkbox indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling. |
| `helperText`            | Add text, string, or expressions to guide users by showing text under the checkbox. Helper text is displayed only when there is no errorText.   |
| `icon`                  | Add an icon to the title. A list of icons is available. See [Jigx icons]() for more information.     |
| `initialValue`          | The `initialValue` is the value that the checkbox will load with when the form is initially loaded. You can use this property to preset the checkbox value so that the user doesn't have to manually select it. Set to `true` loads the checkbox as selected, `false` loads the checkbox as unselected. Using the `reset-state` action with `initialValues` does not clear the checkbox, it resets the field back to it's `initialValue`.                     |
| `isAutoFocused`         | If `true` it will get focus immediately after the jig is displayed.     |
| `isHidden`              | If `true` the checkbox will be hidden on the form. If set to `false` the field will be shown.     |
| `isIgnored`             | When `true`, the field will be ignored when submitting the form and the content will not be stored.      |
| `isOptionalLabelHidden` | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.      |
| `isRequired`            | Set to `true` when the field is required. Useful when you use it in form submission. Set to `false` the checkbox is optional and will have an (optional) in the label.  |
| `nextProperty`          | Name of the property you want to focus next in the form when you use return/next on a keyboard.    |
| `style`                 | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isDanger` - when the checkbox is selected the component displays in red.&#xA;- `isDisabled` - makes the checkbox  field un-selectable.&#xA;- `isPositive` when the checkbox is selected the component displays in green.&#xA;- `isWarning` - displays the component in red.&#xA;More than one can be true. It will be evaluated based on priority. |
| `value`                 | The value to show for the checkbox. Setting up a checkbox with a `value` property of `true` will display the checkbox as selected when the form loads, setting the property to `false` will display the checkbox as unselected when the form loads.   |

| **Actions** |   |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the `checkbox` is changed. Use IntelliSense (ctrl+space) to see the list of available actions.  |
| `onPress`   | `OnPress` action overwrites the main check / uncheck functionality.  |

| **State Configuration**  | **Key**              | **Notes**                                                         |
| ------------------------ | -------------------- | ----------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | - State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | * Global state variable that can be used throughout the solution. |

:::hint{type="info"}
There's also the option to configure checkboxes as part of [entity-field](./../entity/entity-field.md) or [list-item](./../list/list-item.md).
:::

## Examples and code snippets

:::::ExpandableHeading
### Checkbox on Form - Single Selection (Yes/No Question)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Checkbox on a form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IJK_lSaGyt3T1vku2VDAY_mdjjmgfkxmndvtxfd8ru5checkbox-yes-no.png "Checkbox on a form")
:::

:::VerticalSplitItem
The component displays a yes/no question about the agreement to the Terms and Conditions. The option is preselected as the agreement is in our case required.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/yes-no-question/checkbox-yes-no-question.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/yes-no-question/checkbox-yes-no-dynamic.jigx).
:::
::::

:::CodeblockTabs
check-box (static)

```yaml
children:
  - type: component.form
    instanceId: agreement-form
    options:
      children:
        - type: component.checkbox
          instanceId: agreement
          options:
            label: I agree
            isRequired: true
            initialValue: true
```

check-box (dynamic)

```yaml
children:
  - type: component.form
    instanceId: agreement-form
    options:
      children:
        - type: component.checkbox
          instanceId: agreement
          options:
            label: =@ctx.datasources.checkbox-options[0].agreement
            isRequired: true
            initialValue: true
```

datasources (dynamic)

```yaml
datasources:
  checkbox-options:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/checkbox
      query: |
        SELECT
          id,
          '$.order',
          '$.day',
          '$.agreement'
        FROM [default/checkbox] ORDER by '$.order'
```
:::
:::::

:::::ExpandableHeading
### Checkbox on Form - Multiple Selection

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Multiple checkbox selection](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/MCeJFm_9bW3uwfB47U1Uk_ikqrb22eirxfob4os15bcheckbox-multi.PNG "Multiple checkbox selection")
:::

:::VerticalSplitItem
This example displays a question you can answer by selecting multiple checkboxes. The most common answers are already checked for better user experience, but the selection can always be changed.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/multiple-selection/checkbox-multiple-selection.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/multiple-selection/checkbox-multiple-dynamic.jigx)
:::
::::

:::CodeblockTabs
checkbox-multiple (static)

```yaml
children:
  - type: component.form
    instanceId: work-engagement-form
    options:
      children:
        - type: component.checkbox
          instanceId: sunday
          options:
            label: Sunday
            isRequired: false
        - type: component.checkbox
          instanceId: monday
          options:
            label: Monday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: tuesday
          options:
            label: Tuesday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: wednesday
          options:
            label: Wednesday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: thursday
          options:
            label: Thursday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: friday
          options:
            label: Friday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: saturday
          options:
            label: Saturday
            isRequired: false
```

checkbox-multiple (dynamic)

```yaml
children:
  - type: component.form
    instanceId: work-engagement-form
    options:
      children: 
         - type: component.checkbox
           instanceId: sunday
           options:
             label: =@ctx.datasources.checkbox-options[0].day
             isRequired: false
         - type: component.checkbox
           instanceId: monday
           options:
             label: =@ctx.datasources.checkbox-options[1].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: tuesday
           options:
             label: =@ctx.datasources.checkbox-options[2].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: wednesday
           options:
             label: =@ctx.datasources.checkbox-options[3].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: thursday
           options:
             label: =@ctx.datasources.checkbox-options[4].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: friday
           options:
             label: =@ctx.datasources.checkbox-options[5].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: saturday
           options:
             label: =@ctx.datasources.checkbox-options[6].day
             isRequired: false
```

datasources (dynamic)

```yaml
datasources:
  checkbox-options:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/checkbox
      query: |
        SELECT
          id,
          '$.order',
          '$.day',
          '$.agreement'
        FROM [default/checkbox] ORDER by '$.order'
```
:::
:::::

## **See also**

- [State]()

