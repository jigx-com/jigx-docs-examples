# status

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This widget visually represents a status using a combination of icons and colors. The status widget can be used alone or combined with another widget inside a <a href="https://docs.jigx.com/examples/group" target="_blank">widget/group</a>.

The status returned is based on a boolean condition.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tXAcZO-9QGzYEwDiMbZNh_img3839.PNG" size="74" position="center" caption="Status widget" alt="Status widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tXAcZO-9QGzYEwDiMbZNh_img3839.PNG"}
:::
::::

## Configuration options

| **Core options** |                                                                                                                                                                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `statuses`       | Define at least one or more statuses based on conditions. First evaluated to true will be used.&#xA;The `statuses` property includes:<br>* `when` - the condition when the status should be shown
* `icon` - the icon that should be shown |

| **Other options** |                                                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `bottom`          | The [titles](https://docs.jigx.com/examples/titles) component will be added to the bottom of the widget.                                   |
| `color`           | Choose a color from the provided [color palette](#) for the icon. The default color is black if the property is not specified in the YAML. |
| `footer`          | Add text to the footer of the widget.                                                                                                      |
| `footerAlign`     | Align the footer text to `left`, `right`, `center`.                                                                                        |
| `placeholder`     | Specify a placeholder text to display if there is no data, for example - `title: No data to display`.                                      |
| `top`             | The [titles](https://docs.jigx.com/examples/titles) component will be added to the top of the widget.                                      |

## Examples and code snippets

:::::ExpandableHeading
### Status widget (2x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tnCD7-eQIE_OqJABIWIRi_statusiphone13blueportrait.png" size="74" position="center" caption="Status widget" alt="Status widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tnCD7-eQIE_OqJABIWIRi_statusiphone13blueportrait.png"}
:::

:::VerticalSplitItem
In this example the status widget is configured to show a positive icon for the `when: true` property.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/status/static-data/status-static.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/status/dynamic-data/status-dynamic.jigx).
:::
::::

:::CodeblockTabs
status (static)

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

status-with-expression

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

status (dynamic)

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

grid-item

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
:::
:::::

:::::ExpandableHeading
### Status widget (2x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example the `status` widget is configured to show different `icons` and details depending on the status of a mobile device's battery.  The `when:` property is used three times to detemine the status and depending if the `when` evaluates to `true` then the details for that `when` property is shown.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x4/status-1_2x4.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WTumYhYzqm5kEe-lKlCCK-20240808-084743.PNG" size="74" position="center" caption="Status widget 2x4" alt="Status widget 2x4" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WTumYhYzqm5kEe-lKlCCK-20240808-084743.PNG"}
:::
::::

:::CodeblockTabs
status-1\_2x4

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

datasource

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

grid-item

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
:::
:::::

:::::ExpandableHeading
### Status widget(4x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7VYbPDMKaVncUxzZOFVTz_wd-status4x2.PNG" size="74" position="center" caption="Status Widget 4x2" alt="Status Widget 4x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7VYbPDMKaVncUxzZOFVTz_wd-status4x2.PNG"}
:::

:::VerticalSplitItem
In this example the status widget shows that 4 tests failed with `component.titles `to provide more information.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/status-1_4x2.jigx).
:::
::::

:::CodeblockTabs
status-1\_4x2.jigx

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

grid-item

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
:::
:::::

