---
title: value
slug: VEDJ-value
description: Learn how to use the versatile widget described in this document to quickly display values or amounts with customizable configurations. With options to add titles, trend components, and additional text, this widget allows for a tailored overview. Explore 
createdAt: Thu Jun 09 2022 20:16:23 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Mar 10 2025 10:05:42 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Show values and amounts for a quick overview or visual representation on a widget, such as sales targets or the number of orders to date. The value can be a number or date and time.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/OcTCGbkBbgy4XAiSLXL8F_img92bc27cc2344-1.jpeg" size="72" position="center" caption="Value widget" alt="Value widget"}
:::
::::

## Configuration options

| **Core options** |                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| `value`          | Provide the value to be shown on the widget surface. You can use a string, expression or datasource. |

| ### Other options | ****                                                                                                                                |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `align`           | Align the value either `left`, `right` or `center`.                                                                                 |
| `bottom`          | The <a href="https://docs.jigx.com/examples/titles" target="_blank">titles</a> component will be added to the bottom of the widget. |
| `footer`          | Add text to the footer of the widget.                                                                                               |
| `footerAlign`     | Align the footer text to `left`, `right`, `center`.                                                                                 |
| `format`          | Various formats available for the value which is of type date and number, for example, currency.                                    |
| `placeholder`     | Specify a placeholder text to display if there is no data, for example - `title: No data to display`.                               |
| `style`           | By default the value is positive. To show a negative value set the `style:` `isNegative` to `true`.                                 |
| `top`             | The <a href="https://docs.jigx.com/examples/titles" target="_blank">titles</a> component will be added to the top of the widget.    |

## Examples and code snippets

:::::ExpandableHeading
### Value widget (2x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GYzrsAD8f1eWOTTTZwaBG_img7893iphone13blueportrait.png" size="74" position="center" caption="Value widget with number" alt="Value widget with number"}
:::

:::VerticalSplitItem
This example shows a value widget configured with a number value, a `format` unit and `align` right. A `component.title` is added at the `top` and `component.trend` at the `bottom` to show additional information.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-2x2.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-2x2.jigx).
:::
::::

:::CodeblockTabs
value-widget-2x2 (static)

```yaml
widgets:
  valueStatic-2x2: 
    type: widget.value
    options:
      top: 
        type: component.titles
        options:
          title: Solana
          subtitle: USDT
          align: left
          icon: currency-dollar
          iconColor: color2
      value: 212
      format:
        unit: "SOL"  
      align: right
      bottom: 
        type: component.trend
        options:
          title: 92,40 USDT / SOL          
          style:
            isAlignRight: false
            isValueBottom: true
          value: +21.2
          format:
            numberStyle: unit
            unit: percent
```

value-widget-2x2 (dynamic)

```yaml
widgets:
  valueDD-2x2: 
    type: widget.value
    options:
      top: 
        type: component.titles
        options:
          title: =@ctx.datasources.value1.cryptoName
          subtitle: =@ctx.datasources.value1.currency
          align: left
          icon: currency-dollar
          iconColor: color2
          
      value: =@ctx.datasources.value1.cryptoValue
      format:
        unit: =@ctx.datasources.value1.cryptoSymbol
      align: right

      bottom: 
        type: component.trend
        options:
          title: =@ctx.datasources.value1.rate & " " & @ctx.datasources.value1.currency & " / " & @ctx.datasources.value1.cryptoSymbol          
          style:
            isAlignRight: false
            isValueBottom: true
          value: =@ctx.datasources.value1.movement
          format:
            numberStyle: unit
            unit: percent
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: value-widget-2x2
          widgetId: valueStatic-2x2
```
:::
:::::

:::::ExpandableHeading
### Value widget (2x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pXxBUeIjMcGUuZkQPjG9g_img7894iphone13blueportrait.png" size="78" position="center" caption="Value widget with date and time" alt="Value widget with date and time"}
:::

:::VerticalSplitItem
This example shows a value widget configured with a date and time value and a `dateFormat` to show HH\:mm and `align` center. A `component.title` is added at the `top` and at the `bottom` to provide additional information about the meeting.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-2x4.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-2x4.jigx)
:::
::::

:::CodeblockTabs
value-widget-2x4 (static)

```yaml
widgets:    
  valueStatic-2x4:
    type: widget.value
    options:
      align: center
      value: 2022-10-27T14:00:14+0100
      format:
        dateFormat: HH:mm
        unit: Meeting time
      bottom:
        type: component.titles
        options:
          icon: "phone"
          iconColor: color4
          align: center
          title: Jane Stevens
          subtitle: "+420 665 778 998"
      top:
        type: component.titles
        options:
          icon: "calendar"
          iconColor: color9
          align: center
          title: 
            text: 2022-10-27T14:41:13+0100
            format: 
              dateFormat: l
          subtitle: 
            text: 60 Minutes
```

value-widget-2x4 (dynamic)

```yaml
widgets:    
  valueDD-2x4:
    type: widget.value
    options:
      align: center
      value: =@ctx.datasources.value2.meetingTime
      format:
        dateFormat: HH:mm
        unit: =@ctx.datasources.value2.description
        
      bottom:
        type: component.titles
        options:
          icon: "phone"
          iconColor: color4
          align: center
          title: =@ctx.datasources.value2.name
          subtitle: =@ctx.datasources.value2.phoneNumber
      top:
        type: component.titles
        options:
          icon: "calendar"
          iconColor: color9
          align: center
          title: 
            text: =@ctx.datasources.value2.nextMeetingTime
            format: 
              dateFormat: l
          
          subtitle: 
            text: =@ctx.datasources.value2.timeLeft & " Minutes" 
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x4"
      children: 
        type: component.jig-widget
        options:
          jigId: value-widget-2x4
          widgetId: valueStatic-2x4
```
:::
:::::

:::::ExpandableHeading
### Value widget (4x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mTH88SQVn-lvJEtmPiR5__img7895iphone13blueportrait.png" size="80" position="center" caption="Value widget with currency format" alt="Value widget with currency format"}
:::

:::VerticalSplitItem
This example shows a value widget configured with an number value and a `Format` to show currency and `align` centre. A `component.title` is added at the `bottom` to provide additional information about the billing and quarter.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-4x2.jigx)
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-4x2.jigx).
:::
::::

:::CodeblockTabs
value-widget-4x2 (static)

```yaml
widgets:
  value-s-4x2: 
    type: widget.value
    options:
      value: "2329999"
      align: center
      format:
        numberStyle: currency
      bottom: 
        type: component.titles
        options:
          align: center
          title: Company Billing
          subtitle: Q3 / 2022
```

value-widget-4x2 (dynamic)

```yaml
widgets:
  value-dd-4x2: 
    type: widget.value
    options:
      value: =@ctx.datasources.value3.billingValue
      align: center
      format:
        numberStyle: currency
      bottom: 
        type: component.titles
        options:
          align: center
          title: =@ctx.datasources.value3.title
          subtitle: =@ctx.datasources.value3.subtitle
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "4x2"
      children: 
        type: component.jig-widget
        options:
          jigId: value-widget-4x2
          widgetId: value-s-4x2
```
:::
:::::

