---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# field-row

The field-row component contains other input components and displays them on the same row. This component does not indicate a new row; all components are automatically placed in a new row. Instead, this component ensures that items are placed next to instead of underneath each other.

{% include "../../.gitbook/includes/field-rows-can-be-used-in-t....md" %}

## Considerations

* Rows can contain input field components, such as text-field, number-field, email-field e.t.c.
* `field-row` is used on a [default jig](<../../docs/Jig Types/jig_default.md>) or in children components, such as:
  * On a [form](../../docs/Components/form/form.md) component
  * Nested under [section](section.md) components
* A maximum of three components can be displayed per row in a default width ratio of 1:1:1.
* The width ratio of the input fields in the row can be adjusted by specifying the `options.style.flex` property in each of the children components, for example, 1:2:1.

{% include "../../.gitbook/includes/common-component-properties.md" %}

## Configuration options

<table><thead><tr><th width="188.44921875">Configuration options</th><th></th></tr></thead><tbody><tr><td><code>children</code></td><td>Define the nested components inside the <code>field-row</code> component. Use IntelliSense (Ctrl+Space) to see the list of available components.</td></tr></tbody></table>

## Examples and code snippets

### Field-row with style flex with input fields

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/cc-field-row-flex (1).png" alt="Field-row ratios with style flex " width="188"><figcaption><p>Field-row ratios with style flex</p></figcaption></figure>
{% endcolumn %}

{% column %}
Example showing how rows have been incorporated to display more than one component per row in certain instances. The ratio of the fields are set using the `style: flex` property.
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="row- (static)" %}
```yaml
# Field Row with Flex Style
# Demonstrates how to use component.field-row with flex ratios
# to control the proportional width of form fields in a row layout.
title: Field Row with Flex Style 
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1588333489536-0ec90908a41f?q=80&w=1447&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  # Section 1: Equal 1:1:2 ratio 
  # Three text fields in a single row.
  # Title and Initials each occupy 1 unit of width; Last name occupies 2 units.
  # Resulting layout: [Title 25%] [Initials 25%] [Last name 50%]
  - type: component.section
    options:
      title: Field row (Flex ratio -Equal 1:1:2)
      children:
        - type: component.field-row
          options:
            children:
              # Flex 1 - takes up 1/4 of the available row width
              - type: component.text-field
                instanceId: title
                options:
                  label: Title
                  style:
                    flex: 1
              # Flex 1 - takes up 1/4 of the available row width      
              - type: component.text-field
                instanceId: initials
                options:
                  label: Initials
                  style:
                    flex: 1
              # Flex 2 - takes up 2/4 (half) of the available row width      
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last name
                  style:
                    flex: 2
  # Section 2: Equal 2:1 ratio 
  # Two dropdowns in a single row.
  # Country occupies 2 units; Code occupies 1 unit.
  # Resulting layout: [Country ~67%] [Code ~33%]                 
  - type: component.section
    options:
      title: Field row (Flex ratio -Equal 2:1)
      children:
        - type: component.field-row
          options:
            children:
              # Flex 2 - takes up 2/3 of the available row width
              # Populated from the dial-code datasource; value = country name       
              - type: component.dropdown
                instanceId: country
                options:
                  label: Country
                  data: =@ctx.datasources.dial-code
                  item:
                    type: component.dropdown-item
                    options:
                      title: =@ctx.current.item.country
                      value: =@ctx.current.item.country
                  style:
                    flex: 2
              # Flex 1 - takes up 1/3 of the available row width
              # Populated from the dial-code datasource; value = dial code      
              - type: component.dropdown
                instanceId: code
                options:
                  label: Code
                  data: =@ctx.datasources.dial-code
                  item:
                    type: component.dropdown-item
                    options:
                      title: =@ctx.current.item.code
                      value: =@ctx.current.item.code
                  style:
                    flex: 1
  # Section 3: Equal 1:2:2 ratio 
  # Three number fields in a single row.
  # Amount takes 1 unit; Tax and Total each take 2 units.
  # Resulting layout: [Amount 20%] [Tax 40%] [Total 40%]                  
  - type: component.section
    options:
      title: Field row (Flex ratio -Equal 1:2:2)
      children:
        # Flex 1 - takes up 1/5 of the available row width
        # Raw numeric input for the base amount
        - type: component.field-row
          options:
            children:
              - type: component.number-field
                instanceId: amount
                options:
                  label: Amount
                  style:
                    flex: 1
              # Flex 2 - takes up 2/5 of the available row width
              # Displayed as a percentage (e.g. 0.05 - 5%)      
              - type: component.number-field
                instanceId: tax
                options:
                  label:
                    text: Tax %
                    format:
                      numberStyle: percent
                  value: 0.05
                  style:
                    flex: 2
              # Flex 2 - takes up 2/5 of the available row width
              # Read-only computed field
              # Uses component state to reactively reference sibling field values      
              - type: component.number-field
                instanceId: total
                options:
                  label:
                    text: Total
                    format:
                      numberStyle: currency
                      currency: USD
                  value: =@ctx.components.amount.state.value * @ctx.components.tax.state.value
                  style:
                    flex: 2
```
{% endtab %}

{% tab title="datasource (static)" %}
```yaml
datasources:
  dial-code:
    type: datasource.static
    options:
      data:
        - id: 1
          country: United States
          code: US
        - id: 2
          country: United Kingdom
          code: UK
        - id: 3
          country: India
          code: IN
        - id: 4
          country: South Africa
          code: SA
```
{% endtab %}
{% endtabs %}
