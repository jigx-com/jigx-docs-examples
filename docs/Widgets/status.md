# status

{% columns %}
{% column %}
This widget visually represents a status using a combination of icons and colors. The status widget can be used alone or combined with another widget inside a [group](status.md) widget.

The status returned is based on a Boolean condition.
{% endcolumn %}

{% column %}
:::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tXAcZO-9QGzYEwDiMbZNh\_img3839.PNG" size="74" position="center" caption="Status widget" alt="Status widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tXAcZO-9QGzYEwDiMbZNh\_img3839.PNG" width="800" height="1732" darkWidth="800" darkHeight="1732"} ::: ::::


{% endcolumn %}
{% endcolumns %}

## Configuration options

<table><thead><tr><th width="135.328125">Core options</th><th></th></tr></thead><tbody><tr><td><code>statuses</code></td><td><p>Define at least one or more statuses based on conditions. First evaluated to true will be used. The <code>statuses</code> property includes:</p><ul><li><code>when</code> - the condition when the status should be shown</li><li><code>icon</code> - the icon that should be shown</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="141.85546875">Other options</th><th></th></tr></thead><tbody><tr><td><code>bottom</code></td><td>The component will be added to the bottom of the widget.</td></tr><tr><td><code>color</code></td><td>Choose a color from the provided for the icon. The default color is black if the property is not specified in the YAML.</td></tr><tr><td><code>footer</code></td><td>Add text to the footer of the widget.</td></tr><tr><td><code>footerAlign</code></td><td>Align the footer text to <code>left</code>, <code>right</code>, <code>center</code>.</td></tr><tr><td><code>placeholder</code></td><td>Specify a placeholder text to display if there is no data, for example - <code>title: No data to display</code>.</td></tr><tr><td><code>top</code></td><td>The component will be added to the top of the widget.</td></tr></tbody></table>

## Examples and code snippets

### Status widget (2x2)

{% columns %}
{% column %}
::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tnCD7-eQIE\_OqJABIWIRi\_statusiphone13blueportrait.png" size="74" position="center" caption="Status widget" alt="Status widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tnCD7-eQIE\_OqJABIWIRi\_statusiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"} :::


{% endcolumn %}

{% column %}
In this example the status widget is configured to show a positive icon for the `when: true` property.

**Examples**: See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/status/static-data/status-static.jigx). See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/status/dynamic-data/status-dynamic.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="status (static)" %}
```yaml
widgets:
  statusStatic-2x2: 
    type: widget.status
    options:
      statuses:
        - when: true
          icon: check-circle-1
          color: color2
          bottom:
            type: component.titles
            options:
              title: Correct
              align: center
              style:
                isPositive: true
```
{% endtab %}

{% tab title="status-with-expression" %}
```yaml
widgets:
  2x2: 
    type: widget.status
    options:
      statuses:
        - when: =@ctx.datasources.trip-dynamic.flight = 'A 0123' ? true :false
          icon: check-circle-1
          color: color2
          bottom:
            type: component.titles
            options:
              title: Flight was found
              align: center
              style:
                isPositive: true
```
{% endtab %}

{% tab title="status (dynamic)" %}
```yaml
widgets:
  statusDD-2x2: 
    type: widget.status
    options:
      statuses:
        - when: =@ctx.system.isOffline != true
          icon: check-circle-1
          color: color2
          bottom:
            type: component.titles
            options:
              title: Online
              align: center
              style:
                isPositive: true
          
        - when: =@ctx.system.isOffline
          icon: alert-circle
          color: color4
          bottom:
            type: component.titles
            options:
              title: Offline
              align: center
              style:
                isNegative: true
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: status
          widgetId: statusStatic-2x2
```
{% endtab %}
{% endtabs %}

### Status widget (2x4)

{% columns %}
{% column %}
&#x20;In this example the `status` widget is configured to show different `icons` and details depending on the status of a mobile device's battery. The `when:` property is used three times to detemine the status and depending if the `when` evaluates to `true` then the details for that `when` property is shown.

**Examples**: See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x4/status-1_2x4.jigx).
{% endcolumn %}

{% column %}
:::VerticalSplitItem ::Image\[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WTumYhYzqm5kEe-lKlCCK-20240808-084743.PNG" size="74" position="center" caption="Status widget 2x4" alt="Status widget 2x4" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WTumYhYzqm5kEe-lKlCCK-20240808-084743.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"} ::: ::::


{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="status-1_2x4" %}
```yaml
widgets:
  status1-2x4: 
    type: widget.status
    options:
      statuses:
        # Battery less than 25 %
        - when: =@ctx.datasources.device.battery <= 25 ? true:false
          icon: battery-charge
          top:
            type: component.titles
            options:
              icon: mobile-phone-1
              title: =@ctx.datasources.device.device-owner
              subtitle: =@ctx.datasources.device.device-name
              align: center
              iconColor: color14
          bottom:
            type: component.titles
            options:
              title: =@ctx.datasources.device.battery & ' ' & '%'
              subtitle: Battery
              align: center   
          color: negative

        # Battery less than 50 %  
        - when: =@ctx.datasources.device.battery <= 50 ? true:false
          icon: battery-charge
          top:
            type: component.titles
            options:
              icon: mobile-phone-1
              title: =@ctx.datasources.device.device-owner
              subtitle: =@ctx.datasources.device.device-name
              align: center
              iconColor: color14
          bottom:
            type: component.titles
            options:
              title: =@ctx.datasources.device.battery & ' ' & '%'
              subtitle: Battery
              align: center              
          color: warning

        # Battery more than 50 %
        - when: =@ctx.datasources.device.battery > 50 ? true:false
          icon: battery-charge
          top:
            type: component.titles
            options:
              icon: mobile-phone-1
              title: =@ctx.datasources.device.device-owner
              subtitle: =@ctx.datasources.device.device-name
              align: center
              iconColor: color14
          bottom:
            type: component.titles
            options:
              title: =@ctx.datasources.device.battery & ' ' & '%'
              subtitle: Battery
              align: center              
          color: positive
  
```
{% endtab %}

{% tab title="datasource" %}
```yaml
title: Status widget 1 (2x4)
type: jig.default

datasources:
  device:
    type: datasource.static
    options:
      data:
        - device-name: iPhone 14 Pro
          device-owner: Barry Hudson
          battery: 30 # Try to change the number
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x4"
      children: 
        type: component.jig-widget
        options:
          jigId: status-1_2x4
          widgetId: status1-2x4
```
{% endtab %}
{% endtabs %}

### Status widget(4x2)

{% columns %}
{% column %}
::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7VYbPDMKaVncUxzZOFVTz\_wd-status4x2.PNG" size="74" position="center" caption="Status Widget 4x2" alt="Status Widget 4x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7VYbPDMKaVncUxzZOFVTz\_wd-status4x2.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::


{% endcolumn %}

{% column %}
In this example the status widget shows that 4 tests failed with `component.titles` to provide more information.

**Examples**: See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/status-1_4x2.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="status-1_4x2.jigx" %}
```yaml
widgets: 
  status1-4x2: 
    type: widget.status
    options:
      footer: 
        text: test
      statuses:
        - when: true # use an expression to eveluate the true statement
          icon: remove-circle
          color: negative
          
          bottom:
            type: component.titles
            options:
              title: 4 Tests 
              subtitle: Failed  
              align: center   
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "4x2"
      children: 
        type: component.jig-widget
        options:
          jigId: status-1_4x2
          widgetId: status1-4x2
```
{% endtab %}
{% endtabs %}
