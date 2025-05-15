# dropdown

Dropdown fields in forms streamline the user experience by offering a compact, scrollable list of options, saving space and reducing clutter. They help guide users through data selections while minimizing input errors and enhancing form navigation.

::Image[]{alt="Dropdown preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3Opq5FI49WK91cD2RFcpO_dropdown.png" size="90" caption="Dropdown preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3Opq5FI49WK91cD2RFcpO_dropdown.png"}

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure for dropdown** |                                                                                                          |
| ------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `instanceId`                    | The unique identifier for the dropdown component.                                                        |
| `label`                         | Provide a label/name for the dropdown. 'Label' is displayed as a placeholder when no value is specified. |
| `data`                          | Use an expression that evaluates to either an array of options or sections.                              |
| `item`                          | The `item` property use component of **dropdown-item** that includes: `title` and `value`.               |

| **Other options**       |                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`                 | Sets the color of the dropdown property based on conditions by using the `when` property. First evaluated to `true` will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette](#).                                                                                                                                   |
| `errorText`             | Add text, string, or expressions to show text under the dropdown indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling with a red exclamation icon on the right.                                                                                                                                                                                                                                               |
| `helperText`            | Add text, string, or expressions to guide users by showing text under the dropdown. Helper text is displayed only when there is no errorText.                                                                                                                                                                                                                                                                                                        |
| `icon`                  | Add an icon to the title. A list of icons is available. See [Jigx icons](#) for more information.                                                                                                                                                                                                                                                                                                                                                    |
| `initialValue`          | The `initialValue` is the value that will be displayed in the dropdown when the form is initially loaded. You can use this property to preset the dropdown with a default value so that you do not have to manually select it. Using the `reset-state` action with `initialValues` does not clear the dropdown field, it resets the field back to it's `initialValue`.                                                                               |
| `isAutoFocused`         | If `true` the dropdown will get focus immediately after the form is displayed.                                                                                                                                                                                                                                                                                                                                                                       |
| `isHidden`              | If `true` the dropdown will be hidden on the form. If set to `false` the field will be shown.                                                                                                                                                                                                                                                                                                                                                        |
| `isIgnored`             | When `true`, the field will be ignored when submitting the form and the content will not be stored.                                                                                                                                                                                                                                                                                                                                                  |
| `isMultiple`            | Set to `true` allows you to select multiple items inside the dropdown. Set to `false` only allows a single selection in the dropdown.                                                                                                                                                                                                                                                                                                                |
| `isOptionalLabelHidden` | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.                                                                                                                                                                                                                                                                                       |
| `isRequired`            | Set to `true` when the field is required. Useful when you use it in form submission. Set to `false` the dropdown is optional and will have (optional) in the label.                                                                                                                                                                                                                                                                                  |
| `isSearchable`          | Set to `true` allows the items in the dropdown to be searchable. A search bar is added to the top of the dropdown list. For the search field to function the `data` property should be configured with a filter expression, e.g. `=$filter(@ctx.datasources.employees-static, function($v){$contains($string($v.firstname),$string(@ctx.components.dropdown-in.state.searchText != null ? @ctx.components.dropdown-in.state.searchText:''))})[]`     |
| `isSearchAutoFocused`   | If set to `true` the searchable input will get focus immediately when opened.                                                                                                                                                                                                                                                                                                                                                                        |
| `nextProperty`          | Name of the property you want to focus next in the form when you use return/next on a keyboard.                                                                                                                                                                                                                                                                                                                                                      |
| `style`                 | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays spinner on right side of field. It removes any  configured icon.&#xA;- `isDisabled` - disables the dropdown preventing the dropdown-items popup from displaying.&#xA;- `isPositive` - a green icon displays on the right of the dropdown field.&#xA;More than one can be true. It will be evaluated based on priority. |
| `value`                 | The value to show in the dropdown, e.g. you can configure the first dropdown-item for be selected by default when the form loads. For example, `value: =@ctx.datasources.employees-static[0].firstName `                                                                                                                                                                                                                                             |

| **Other options for dropdown-item** |                                                                                                                                                                   |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `description`                       | Description of steps displayed on list items as subtitles.                                                                                                        |
| `instanceId`                        | The unique identifier for the dropdown-item component.                                                                                                            |
| `leftElement`                       | The following elements can be added in the dropdown component, which will display on the left of the dropdown-item `title`:&#xA;`avatar`<br />`icon`<br />`image` |
| `subtitle`                          | The subtitle for the dropdown item.                                                                                                                               |
| `title`                             | Title displayed on list item. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more.    |
| `value`                             | The value of the item. It has to be unique for each item and is usually the ID of the record from the datasource.                                                 |

| **Actions** |                                                                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `onChange`  | The action is triggered when the content in the `dropdown` is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |

| **State Configuration**  | **Key**                           | **Notes**                                                          |
| ------------------------ | --------------------------------- | ------------------------------------------------------------------ |
| `=@ctx.component.state.` | searchText&#xA;selected&#xA;value | - State is the variable of the component.                          |
| `=@ctx.solution.state.`  | activeItemId&#xA;now              | \* Global state variable that can be used throughout the solution. |

## Examples and code snippets

:::::ExpandableHeading
### Default dropdown example

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Dropdown-items ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_XXgxlmitjefB9T8gvB4u_zomhxdlxcxc7dlkm5z6ydropdown-defaultiphone13blueportrait.png "Dropdown-items ")
:::

:::VerticalSplitItem
**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/dropdown-dynamic.jigx).

**Datasources:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx).
:::
::::

:::CodeblockTabs
dropdown (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =@ctx.datasources.employees-static
            label: Select employees
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                value: =@ctx.current.item.firstname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.img
```

dropdown (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =@ctx.datasources.employees-dynamic
            label: Select employees
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                value: =@ctx.current.item.firstname
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.picture
```

datasources (static)

```yaml
datasources:
  employees-static:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: July
          lastname: Nellson
          position: manager
          img: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 2
          firstname: Karl
          lastname: Fisher
          position: Salesman
          img: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
        - id: 3
          firstname: Mary
          lastname: Gomez
          position: DEV
          img: https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 4
          firstname: John
          lastname: Donald
          position: Marketing
          img: https://images.unsplash.com/photo-1566492031773-4f4e44671857?q=80&w=1287&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
```

datasources (dynamic)

```yaml
datasources:
  employees-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/employees
      query: |
        SELECT 
          id,
          '$.firstname',
          '$.lastname',
          '$.picture', 
          '$.modify', 
          '$.date_from', 
          '$.date_to', 
          '$.email',
          '$.phone', 
          '$.percentage', 
          '$.category', 
          '$.photo',
          '$.time'
        FROM [default/employees] WHERE '$.category' = "employees" ORDER BY '$.firstname' ASC
```
:::
:::::

:::::ExpandableHeading
### Multiple select dropdown

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A8sWkbH9ukD4sFkCujOot_ngcd8fozzsjh6nz3j0ogdropdown-multipleiphone13blueportrait.png" size="80" position="center" caption="Multiple dropdown-items " alt="Multiple dropdown-items " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A8sWkbH9ukD4sFkCujOot_ngcd8fozzsjh6nz3j0ogdropdown-multipleiphone13blueportrait.png"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Cky4zkcmv7RgRSRqw_SoP_06x339zv728sfuekadodropdown-multiple2iphone13blueportrait.png" size="78" position="center" caption="Dropdown with multiple selected" alt="Dropdown with multiple selected" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Cky4zkcmv7RgRSRqw_SoP_06x339zv728sfuekadodropdown-multiple2iphone13blueportrait.png"}
:::
::::

In this example, we will show you how you can set up your dropdown for multiple selections.

**Examples:**

See the full example using static data in \<[GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-multiple-select.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/multiple-select-dynamic.jigx).

**Datasources:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx)

:::CodeblockTabs
multiple-select-dropdown (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =@ctx.datasources.employees-static
            label: Select employees
            isMultiple: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                value: =@ctx.current.item.firstname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.img
```

multiple-select-dropdown (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =@ctx.datasources.employees-dynamic
            label: Select employees
            isMultiple: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                value: =@ctx.current.item.firstname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.photo
```

datasources (static)

```yaml
datasources:
  employees-static:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: July
          lastname: Nellson
          position: manager
          img: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 2
          firstname: Karl
          lastname: Fisher
          position: Salesman
          img: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
        - id: 3
          firstname: Mary
          lastname: Gomez
          position: DEV
          img: https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 4
          firstname: John
          lastname: Doe
          position: Marketing
          img: https://images.unsplash.com/photo-1548449112-96a38a643324?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
```

datasources (dynamic)

```yaml
datasources:
  employees-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/employees
      query: |
        SELECT 
          id,
          '$.firstname',
          '$.lastname',
          '$.picture', 
          '$.modify', 
          '$.date_from', 
          '$.date_to', 
          '$.email',
          '$.phone', 
          '$.percentage', 
          '$.category', 
          '$.photo',
          '$.time'
        FROM [default/employees] WHERE '$.category' = "employees" ORDER BY '$.firstname' ASC
```
:::
:::::

:::::ExpandableHeading
### Search dropdown

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UjhHKuhR5Xnqy4qpWZY1y_hwnkejspnia9o0tkhs3tudropdown-searchiphone13blueportrait.png" size="78" position="center" caption="Dropdown with search" alt="Dropdown with search" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UjhHKuhR5Xnqy4qpWZY1y_hwnkejspnia9o0tkhs3tudropdown-searchiphone13blueportrait.png"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F67oAjjxBTXdDph_dp5dC_mcvfx2gwtac4mfepaabx6dropdown-search-2iphone13blueportrait.png" size="80" position="center" caption alt="Dropdown with search" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F67oAjjxBTXdDph_dp5dC_mcvfx2gwtac4mfepaabx6dropdown-search-2iphone13blueportrait.png"}
:::
::::

In this example, we can find the search function in our dropdown.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-searchable.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/searchable-dynamic.jigx).

**Datasources:**
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/searchable-dynamic.jigx).

:::CodeblockTabs
search-dropdown (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =$filter(@ctx.datasources.employees-static, function($v){$contains($string($v.firstname),$string(@ctx.components.dropdown-in.state.searchText != null ? @ctx.components.dropdown-in.state.searchText:''))})[]
            label: Select employees
            isSearchable: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                value: =@ctx.current.item.firstname
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.img
```

search-dropdown (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data: =@ctx.datasources.employees-dropdown
            label: Select employees
            isSearchable: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                value: =@ctx.current.item.firstname
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.picture
```

datasources (static)

```yaml
datasources:
  employees-static:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: July
          lastname: Nellson
          position: manager
          img: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 2
          firstname: Karl
          lastname: Fisher
          position: Salesman
          img: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
        - id: 3
          firstname: Mary
          lastname: Gomez
          position: DEV
          img: https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 4
          firstname: John
          lastname: Doe
          position: Marketing
          img: https://images.unsplash.com/photo-1548449112-96a38a643324?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
```

datasources (dynamic)

```yaml
title: Dropdown
type: jig.default

datasources:
  employees-dropdown:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/employees
      query: |
        SELECT 
          id,
          '$.firstname',
          '$.lastname',
          '$.picture', 
          '$.modify', 
          '$.date_from', 
          '$.date_to', 
          '$.email',
          '$.phone', 
          '$.percentage', 
          '$.category', 
          '$.photo',
          '$.time'
         FROM [default/employees] WHERE '$.firstname' LIKE '%'||@search||'%' OR @search IS NULL
      queryParameters:
        '@search': =@ctx.components.dropdown-in.state.searchText
```
:::
:::::

::::ExpandableHeading
### Dropdown with a default value

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZLtcAYaEPxEK7rdQiwCCd_ddown-default-value.png" size="80" position="center" caption="Dropdown with default value" alt="dropdown with default value" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZLtcAYaEPxEK7rdQiwCCd_ddown-default-value.png"}

In this example, we populate the first employee's name as the default value to show in the dropdown by using the `initialValue` property with an expression to return the first value from the datasource. Opening the dropdown shows the first checkbox selected.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-default-value.jigx).

**Datasources:**
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).

:::CodeblockTabs
search-dropdown (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            data:  =$filter(@ctx.datasources.employees-static, function($v){$contains($string($v.firstname),$string(@ctx.components.dropdown-in.state.searchText != null ? @ctx.components.dropdown-in.state.searchText:''))})[]
            initialValue: =@ctx.datasources.employees-static[0].firstname 
            label: Select an employee
            isSearchable: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
              
                value: =@ctx.current.item.firstname
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement: 
                  element: avatar
                  text: ''
                  uri: =@ctx.current.item.img         
```

datasources (static)

```yaml
datasources:
  employees-static:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: July
          lastname: Nellson
          position: manager
          img: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 2
          firstname: Karl
          lastname: Fisher
          position: Salesman
          img: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
        - id: 3
          firstname: Mary
          lastname: Gomez
          position: DEV
          img: https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
        - id: 4
          firstname: John
          lastname: Doe
          position: Marketing
          img: https://images.unsplash.com/photo-1548449112-96a38a643324?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
```
:::
::::

## See also

- [State](#)

