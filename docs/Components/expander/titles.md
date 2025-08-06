# titles

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The titles component displays a title, subtitle, comment, or any type of text content with an icon which is optional.
:::

:::VerticalSplitItem
::Image[]{alt="Titles Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/URj78rz7Ik4FkLEZN1I8u_titles.png" size="86" caption="Titles Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/URj78rz7Ik4FkLEZN1I8u_titles.png" width="800" height="172" darkWidth="800" darkHeight="172"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Add text on the `centerElements` of the `component.expander`. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more. |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>align</code></p>
    </td>
    <td selected="false" align="left">
      <p>The alignment of the content inside of your component. Where the container and text should be aligned, the options are:</p>
      <ul>
      <li><code>left</code></li>
      <li><code>right</code></li>
      <li><code>center</code></li>
      </ul>
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
      <p><code>iconColor</code></p>
    </td>
    <td selected="false" align="left">
      <p>Sets the color of the icon, choose a color from the provided color palette. Default color is black if the property is not specified in the YAML. See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following styling sets are available:</p>
      <ul>
      <li><code>isNegative</code></li>
      <li><code>isPositive</code></li>
      <li><code>isWarning</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>subtitle</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add a <code>subtitle</code>/ short description of the component.</p>
    </td>
  </tr>
</table>

## Consideration

- `component.titles` can only be used in the `centerElement` of the `component.expander`

## Examples and code snippets

:::::ExpandableHeading
### Expander with titles in a header

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/evtS4oSL4t4yGt7Gcg4AV_bzjgtccktzcmqfgs-mdseexpander-with-titles-in-a-headeriphone13blueportrait.png" size="80" position="center" caption="Expander with titles" alt="Expander with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/evtS4oSL4t4yGt7Gcg4AV_bzjgtccktzcmqfgs-mdseexpander-with-titles-in-a-headeriphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2gXn9HMZZgzoE38Wt91ZE_ivsv2bndlkg7ebc6cdb8zexpander-with-titles-in-a-header2iphone13blueportrait.png" size="80" position="center" caption alt="Expander with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2gXn9HMZZgzoE38Wt91ZE_ivsv2bndlkg7ebc6cdb8zexpander-with-titles-in-a-header2iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
:::
::::

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/static-data/expander.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/dynamic-data/expander-dynamic-data.jigx).

**Datasource:**

See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/expander-dynamic.jigx)

:::CodeblockTabs
expander (static)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.titles
          options:
            title: July Nelson
            subtitle: Manager
            icon: person
            align: left
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Phone
                        value: "3249432812"
                    - type: component.entity-field
                      options:
                        label: Email
                        value: july@first.com
              - type: component.entity-field
                options:
                  label: Address
                  value: 141 Harbor Dr Claymont, Delaware(DE), 19703
        - type: component.bar-chart
          options:
            chart:
              title:
                text: Last year revenue
            legend:
              isHidden: true
            series:
              - data: =@ctx.datasources.series1
```

expander (dynamic)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.titles
          options:
            title: =@ctx.datasources.expander-dynamic.firstname & ' ' & @ctx.datasources.expander-dynamic.lastname
            subtitle: =@ctx.datasources.expander-dynamic.position
            icon: person
            align: left
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Phone
                        value: =@ctx.datasources.expander-dynamic.phone
                    - type: component.entity-field
                      options:
                        label: Email
                        value: =@ctx.datasources.expander-dynamic.email
              - type: component.entity-field
                options:
                  label: Address
                  value: =@ctx.datasources.expander-dynamic.address
        - type: component.bar-chart
          options:
            chart:
              title:
                text: Last year revenue
            legend:
              isHidden: true
            series:
              - data: =@ctx.datasources.series1-dynamic
```

datasources (dynamic)

```yaml
datasources:
  expander-dynamic:
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
          '$.date_from', 
          '$.date_to', 
          '$.email',
          '$.phone', 
          '$.position', 
          '$.address', 
          '$.category' 
        FROM [default/employees] WHERE '$.firstname' = "July" AND '$.category' = 'employees'
```
:::
:::::

