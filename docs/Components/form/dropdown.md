# dropdown

Dropdown fields in forms streamline the user experience by offering a compact, scrollable list of options, saving space and reducing clutter. They help guide users through data selections while minimizing input errors and enhancing form navigation.

<figure><img src="../../../.gitbook/assets/cc-dropdown-intro.png" alt="Dropdown preview" width="375"><figcaption><p>Dropdown preview</p></figcaption></figure>

{% hint style="info" %}
The `dropdown` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
{% endhint %}

## Configuration options

Some properties are common to all components, see [Common component properties](dropdown.md) for a list and their configuration options.

<table><thead><tr><th width="229.08984375">Core structure for dropdown</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the dropdown component.</td></tr><tr><td><code>label</code></td><td>Provide a label/name for the dropdown. 'Label' is displayed as a placeholder when no value is specified.</td></tr><tr><td><code>data</code></td><td>Use an expression that evaluates to either an array of options or sections.</td></tr><tr><td><code>item</code></td><td>The <code>item</code> property use component of <strong>dropdown-item</strong> that includes: <code>title</code> and <code>value</code>.</td></tr></tbody></table>

<table><thead><tr><th width="225.46484375">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>Sets the color of the dropdown property based on conditions by using the <code>when</code> property. First evaluated to <code>true</code> will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</td></tr><tr><td><code>errorText</code></td><td>Add text, string, or expressions to show text under the dropdown indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling with a red exclamation icon on the right.</td></tr><tr><td><code>helperText</code></td><td>Add text, string, or expressions to guide users by showing text under the dropdown. Helper text is displayed only when there is no errorText.</td></tr><tr><td><code>icon</code></td><td>Add an icon to the title. A list of icons is available. See for more information.</td></tr><tr><td><code>initialValue</code></td><td>The <code>initialValue</code> is the value that will be displayed in the dropdown when the form is initially loaded. You can use this property to preset the dropdown with a default value so that you do not have to manually select it. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the dropdown field, it resets the field back to it's <code>initialValue</code>.</td></tr><tr><td><code>isAutoFocused</code></td><td>If <code>true</code> the dropdown will get focus immediately after the form is displayed.</td></tr><tr><td><code>isHidden</code></td><td>If <code>true</code> the dropdown will be hidden on the form. If set to <code>false</code> the field will be shown.</td></tr><tr><td><code>isIgnored</code></td><td>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</td></tr><tr><td><code>isMultiple</code></td><td>Set to <code>true</code> allows you to select multiple items inside the dropdown. Set to <code>false</code> only allows a single selection in the dropdown.</td></tr><tr><td><code>isOptionalLabelHidden</code></td><td>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> when the field is required. Useful when you use it in form submission. Set to <code>false</code> the dropdown is optional and will have (optional) in the label.</td></tr><tr><td><code>isSearchable</code></td><td>Set to <code>true</code> allows the items in the dropdown to be searchable. A search bar is added to the top of the dropdown list. For the search field to function the <code>data</code> property should be configured with a filter expression, e.g. <code>=$filter(@ctx.datasources.employees-static, function($v){$contains($string($v.firstname),$string(@ctx.components.dropdown-in.state.searchText != null ? @ctx.components.dropdown-in.state.searchText:''))})[]</code></td></tr><tr><td><code>isSearchAutoFocused</code></td><td>If set to <code>true</code> the searchable input will get focus immediately when opened.</td></tr><tr><td><code>nextProperty</code></td><td>Name of the property you want to focus next in the form when you use return/next on a keyboard.</td></tr><tr><td><code>style</code></td><td><p>The following property settings are available:</p><ul><li><code>flex</code> - Flex property if rendered inside row.</li><li><code>isBusy</code> - Displays spinner on right side of field. It removes any configured icon.</li><li><code>isDisabled</code> - disables the dropdown preventing the dropdown-items popup from displaying.</li><li><code>isPositive</code> - a green icon displays on the right of the dropdown field. More than one can be true. It will be evaluated based on priority.</li></ul></td></tr><tr><td><code>value</code></td><td>The value to show in the dropdown, e.g. you can configure the first dropdown-item for be selected by default when the form loads. For example, <code>value: =@ctx.datasources.employees-static[0].firstName</code></td></tr></tbody></table>

<table><thead><tr><th width="258.12109375">Other options for dropdown-item</th><th></th></tr></thead><tbody><tr><td><code>description</code></td><td>Description of steps displayed on list items as subtitles.</td></tr><tr><td><code>instanceId</code></td><td>The unique identifier for the dropdown-item component.</td></tr><tr><td><code>leftElement</code></td><td><p>The following elements can be added in the dropdown component, which will display on the left of the dropdown-item <code>title</code>:</p><ul><li><code>avatar</code></li><li><code>icon</code></li><li><code>image</code></li></ul></td></tr><tr><td><code>subtitle</code></td><td>The subtitle for the dropdown item.</td></tr><tr><td><code>title</code></td><td>Title displayed on list item. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more.</td></tr><tr><td><code>value</code></td><td>The value of the item. It has to be unique for each item and is usually the ID of the record from the datasource.</td></tr></tbody></table>

<table><thead><tr><th width="255.78515625">Actions</th><th></th></tr></thead><tbody><tr><td><code>onChange</code></td><td>The action is triggered when the content in the <code>dropdown</code> is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="216.1640625">State Configuration</th><th width="215.98828125">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>searchText selected value</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

## Examples and code snippets

### Default dropdown example

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/cc-dropdown-basic.png" alt="Dropdown-items" width="178"><figcaption><p>Dropdown-items</p></figcaption></figure>
{% endcolumn %}

{% column %}
**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/dropdown-dynamic.jigx).

**Datasources:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="dropdown (static)" %}
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
{% endtab %}

{% tab title="dropdown (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}

### Multiple select dropdown

{% columns %}
{% column %}
In this example, we will show you how you can set up your dropdown for multiple selections.

**Examples:**\
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-multiple-select.jigx).\
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/multiple-select-dynamic.jigx).

**Datasources:**\
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).\
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx)
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/cc-dropdown-multi.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% tabs %}
{% tab title=" multiple-select-dropdown (static)" %}
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
{% endtab %}

{% tab title="multiple-select-dropdown (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}

### Search dropdown

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/cc-dropdown-search.png" alt="Dropdown with search"><figcaption><p>Dropdown with search</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example, we can find the search function in our dropdown.

**Examples:**\
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-searchable.jigx).\
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/searchable-dynamic.jigx).

**Datasources:**\
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).\
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/dynamic-data/searchable-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}



{% tabs %}
{% tab title="search-dropdown (static)" %}
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
{% endtab %}

{% tab title="search-dropdown (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}

### Dropdown with a default value

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/cc-dropdown-defaultValue.png" alt="Dropdown with default value"><figcaption><p>Dropdown with default value</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example, we populate the first employee's name as the default value to show in the dropdown by using the `initialValue` property with an expression to return the first value from the datasource. Opening the dropdown shows the first checkbox selected.

**Examples:** See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-default-value.jigx).

**Datasources:** See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="search-dropdown (static)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}
{% endtabs %}

## See also

* [State](https://docs.jigx.com/state)
