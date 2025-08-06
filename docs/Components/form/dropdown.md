# dropdown

Dropdown fields in forms streamline the user experience by offering a compact, scrollable list of options, saving space and reducing clutter. They help guide users through data selections while minimizing input errors and enhancing form navigation.

::Image[]{alt="Dropdown preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3Opq5FI49WK91cD2RFcpO_dropdown.png" size="90" caption="Dropdown preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3Opq5FI49WK91cD2RFcpO_dropdown.png" width="800" height="457" darkWidth="800" darkHeight="457"}

:::hint{type="info"}
The `dropdown` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure for dropdown** |                                                                                                          |
| ------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `instanceId`                    | The unique identifier for the dropdown component.                                                        |
| `label`                         | Provide a label/name for the dropdown. 'Label' is displayed as a placeholder when no value is specified. |
| `data`                          | Use an expression that evaluates to either an array of options or sections.                              |
| `item`                          | The `item` property use component of **dropdown-item** that includes: `title` and `value`.               |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="210">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>color</code></p>
    </td>
    <td selected="false" align="left">
      <p>Sets the color of the dropdown property based on conditions by using the <code>when</code> property. First evaluated to <code>true</code> will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to show text under the dropdown indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling with a red exclamation icon on the right.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to guide users by showing text under the dropdown. Helper text is displayed only when there is no errorText.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the title. A list of icons is available. See  for more information.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>initialValue</code> is the value that will be displayed in the dropdown when the form is initially loaded. You can use this property to preset the dropdown with a default value so that you do not have to manually select it. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the dropdown field, it resets the field back to it's <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the dropdown will get focus immediately after the form is displayed.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the dropdown will be hidden on the form. If set to <code>false</code> the field will be shown.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isIgnored</code></p>
    </td>
    <td selected="false" align="left">
      <p>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isMultiple</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> allows you to select multiple items inside the dropdown. Set to <code>false</code> only allows a single selection in the dropdown.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isOptionalLabelHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isRequired</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> when the field is required. Useful when you use it in form submission. Set to <code>false</code> the dropdown is optional and will have (optional) in the label.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isSearchable</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> allows the items in the dropdown to be searchable. A search bar is added to the top of the dropdown list. For the search field to function the <code>data</code> property should be configured with a filter expression, e.g. <code>=$filter(@ctx.datasources.employees-static, function($v){$contains($string($v.firstname),$string(@ctx.components.dropdown-in.state.searchText != null ? @ctx.components.dropdown-in.state.searchText:''))})[]</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isSearchAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If set to <code>true</code> the searchable input will get focus immediately when opened.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>nextProperty</code></p>
    </td>
    <td selected="false" align="left">
      <p>Name of the property you want to focus next in the form when you use return/next on a keyboard.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following property settings are available:</p>
      <ul>
      <li><code>flex</code> - Flex property if rendered inside row.</li>
      <li><code>isBusy</code> - Displays spinner on right side of field. It removes any  configured icon.</li>
      <li><code>isDisabled</code> - disables the dropdown preventing the dropdown-items popup from displaying.</li>
      <li><code>isPositive</code> - a green icon displays on the right of the dropdown field.
      More than one can be true. It will be evaluated based on priority.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to show in the dropdown, e.g. you can configure the first dropdown-item for be selected by default when the form loads. For example,
      <code>value: =@ctx.datasources.employees-static[0].firstName</code></p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options for dropdown-item</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>description</code></p>
    </td>
    <td selected="false" align="left">
      <p>Description of steps displayed on list items as subtitles.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>instanceId</code></p>
    </td>
    <td selected="false" align="left">
      <p>The unique identifier for the dropdown-item component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>leftElement</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following elements can be added in the dropdown component, which will display on the left of the dropdown-item <code>title</code>:</p>
      <ul>
      <li><code>avatar</code></li>
      <li><code>icon</code></li>
      <li><code>image</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>subtitle</code></p>
    </td>
    <td selected="false" align="left">
      <p>The subtitle for the dropdown item.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Title displayed on list item. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value of the item. It has to be unique for each item and is usually the ID of the record from the datasource.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="167">
  <tr>
    <td selected="false" align="left">
      <p><strong>Actions</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onChange</code></p>
    </td>
    <td selected="false" align="left">
      <p>The action is triggered when the content in the <code>dropdown</code> is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218,126">
  <tr>
    <td selected="false" align="left">
      <p><strong>State Configuration</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Key</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Notes</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.component.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>searchText
      selected
      value</p>
    </td>
    <td selected="false" align="left">
      <p>State is the variable of the component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>activeItemId
      now</p>
    </td>
    <td selected="false" align="left">
      <p>Global state variable that can be used throughout the solution.</p>
    </td>
  </tr>
</table>

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
        FROM [default/employees] 
        WHERE '$.category' = "employees" ORDER BY '$.firstname' ASC
```
:::
:::::

:::::ExpandableHeading
### Multiple select dropdown

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A8sWkbH9ukD4sFkCujOot_ngcd8fozzsjh6nz3j0ogdropdown-multipleiphone13blueportrait.png" size="80" position="center" caption="Multiple dropdown-items " alt="Multiple dropdown-items " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A8sWkbH9ukD4sFkCujOot_ngcd8fozzsjh6nz3j0ogdropdown-multipleiphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Cky4zkcmv7RgRSRqw_SoP_06x339zv728sfuekadodropdown-multiple2iphone13blueportrait.png" size="78" position="center" caption="Dropdown with multiple selected" alt="Dropdown with multiple selected" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Cky4zkcmv7RgRSRqw_SoP_06x339zv728sfuekadodropdown-multiple2iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
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
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UjhHKuhR5Xnqy4qpWZY1y_hwnkejspnia9o0tkhs3tudropdown-searchiphone13blueportrait.png" size="78" position="center" caption="Dropdown with search" alt="Dropdown with search" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UjhHKuhR5Xnqy4qpWZY1y_hwnkejspnia9o0tkhs3tudropdown-searchiphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F67oAjjxBTXdDph_dp5dC_mcvfx2gwtac4mfepaabx6dropdown-search-2iphone13blueportrait.png" size="80" position="center" caption alt="Dropdown with search" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F67oAjjxBTXdDph_dp5dC_mcvfx2gwtac4mfepaabx6dropdown-search-2iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
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

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZLtcAYaEPxEK7rdQiwCCd_ddown-default-value.png" size="80" position="center" caption="Dropdown with default value" alt="dropdown with default value" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZLtcAYaEPxEK7rdQiwCCd_ddown-default-value.png" width="800" height="794" darkWidth="800" darkHeight="794"}

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

- [State](https://docs.jigx.com/state)

