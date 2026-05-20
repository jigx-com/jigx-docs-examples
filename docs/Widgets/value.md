# value

{% columns %}
{% column %}
Show values and amounts for a quick overview or visual representation on a widget, such as sales targets or the number of orders to date. The value can be a number or date and time.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/wd-value-intro.png" alt="Value widgets" width="188"><figcaption><p>Value widgets</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Configuration options

<table><thead><tr><th width="145.1015625">Core options</th><th></th></tr></thead><tbody><tr><td><code>value</code></td><td>Provide the value to be shown on the widget surface. You can use a string, expression or datasource.</td></tr></tbody></table>

<table><thead><tr><th width="149.046875">Other options</th><th></th></tr></thead><tbody><tr><td><code>align</code></td><td>Align the value either <code>left</code>, <code>right</code> or <code>center</code>.</td></tr><tr><td><code>bottom</code></td><td>The component will be added to the bottom of the widget.</td></tr><tr><td><code>footer</code></td><td>Add text to the footer of the widget.</td></tr><tr><td><code>footerAlign</code></td><td>Align the footer text to <code>left</code>, <code>right</code>, <code>center</code>.</td></tr><tr><td><code>format</code></td><td>Various formats available for the value which is of type date and number, for example, currency.</td></tr><tr><td><code>placeholder</code></td><td>Specify a placeholder text to display if there is no data, for example - <code>title: No data to display</code>.</td></tr><tr><td><code>style</code></td><td>By default the value is positive. To show a negative value set the <code>style:</code> <code>isNegative</code> to <code>true</code>.</td></tr><tr><td><code>top</code></td><td>The component will be added to the top of the widget.</td></tr></tbody></table>

## Examples and code snippets

## Value widget (2x2)

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/wd-value1.png" alt="Value widget with number" width="177"><figcaption><p>Value widget with number</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example shows a value widget configured with a number value, a `format` unit and `align` right. A `component.title` is added at the `top` and `component.trend` at the `bottom` to show additional information.

**Examples**: See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-2x2.jigx). See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-2x2.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="value-widget-2x2 (static)" %}
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
{% endtab %}

{% tab title="value-widget-2x2 (dynamic)" %}
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
{% endtab %}

{% tab title="grid-item" %}
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
{% endtab %}
{% endtabs %}

## Value widget (2x4)

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/wd-valueDateTime.png" alt="Value widget with date and time" width="188"><figcaption><p>Value widget with date and time</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example shows a value widget configured with a date and time value and a `dateFormat` to show HH:mm and `align` center. A `component.title` is added at the `top` and at the `bottom` to provide additional information about the meeting.

**Examples**: See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-2x4.jigx). See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-2x4.jigx)
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="value-widget-2x4 (static)" %}
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
{% endtab %}

{% tab title="value-widget-2x4 (dynamic)" %}
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
{% endtab %}

{% tab title="grid-item" %}
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
{% endtab %}
{% endtabs %}

## Value widget (4x2)

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/wd-value42.png" alt="Value widget with currency format" width="188"><figcaption><p>Value widget with currency format</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example shows a value widget configured with an number value and a `Format` to show currency and `align` centre. A `component.title` is added at the `bottom` to provide additional information about the billing and quarter.

**Examples**: See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/static/value-static-4x2.jigx) See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/value/dynamic/value-dynamic-4x2.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="value-widget-4x2 (static)" %}
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
{% endtab %}

{% tab title="value-widget-4x2 (dynamic)" %}
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
{% endtab %}

{% tab title="grid-item" %}
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
{% endtab %}
{% endtabs %}
