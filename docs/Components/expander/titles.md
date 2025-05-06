---
title: titles
slug: h1bm-titles
description: Learn how to use a versatile text display component with optional icons, titles, subtitles, and customizable styles. This document offers examples and code snippets for implementing the component with both static and dynamic data, including provided datas
createdAt: Thu Jun 09 2022 19:55:14 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 24 2024 09:32:28 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The titles component displays a title, subtitle, comment, or any type of text content with an icon which is optional.&#x20;
:::

:::VerticalSplitItem
::Image[]{alt="Titles Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/URj78rz7Ik4FkLEZN1I8u_titles.png" size="86" width="1125" height="242" caption="Titles Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/URj78rz7Ik4FkLEZN1I8u_titles.png"}
:::
::::

## ****Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| ### Core structure | ****                                                                                                                                                                                           |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Add text on the `centerElements` of the `component.expander`. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more. |

| ### Other options | ****                                                                                                                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `align`           | The alignment of the content inside of your component. Where the container and text should be aligned, the options are:<br />* `left`
* `right`
* `center`                                                   |
| `icon`            | Add an icon to the title. A list of icons is available. See [Jigx icons]() for more information.                                                                                                             |
| `iconColor`       | Sets the color of the icon, choose a color from the provided color palette. Default color is black if the property is not specified in the YAML. See the list of available colors in [Jigx color palette](). |
| `style`           | The following styling sets are available:<br />* `isNegative`
* `isPositive`
* `isWarning`                                                                                                                   |
| `subtitle`        | Add a  `subtitle`/ short description of the component.                                                                                                                                                       |

## Consideration

- `component.titles` can only be used in the `centerElement` of the  `component.expander`

## Examples and code snippets ****

:::::ExpandableHeading
### Expander with titles in a header

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/evtS4oSL4t4yGt7Gcg4AV_bzjgtccktzcmqfgs-mdseexpander-with-titles-in-a-headeriphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/evtS4oSL4t4yGt7Gcg4AV_bzjgtccktzcmqfgs-mdseexpander-with-titles-in-a-headeriphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption="Expander with titles" alt="Expander with titles"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2gXn9HMZZgzoE38Wt91ZE_ivsv2bndlkg7ebc6cdb8zexpander-with-titles-in-a-header2iphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2gXn9HMZZgzoE38Wt91ZE_ivsv2bndlkg7ebc6cdb8zexpander-with-titles-in-a-header2iphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption alt="Expander with titles"}
:::
::::

**Examples:**

See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/static-data/expander.jigx" target="_blank">GitHub</a>.
See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/dynamic-data/expander-dynamic-data.jigx" target="_blank">GitHub</a>.&#x20;

**Datasource:**

See the full datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/expander-dynamic.jigx" target="_blank">GitHub</a>.&#x20;

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

