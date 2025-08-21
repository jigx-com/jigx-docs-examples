---
title: onPress
slug: PAcW-on
createdAt: Fri May 31 2024 06:53:13 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Mar 07 2025 13:44:35 GMT+0000 (Coordinated Universal Time)
---

# onPress

Use the `onPress` event to add an action directly on the widget. This is particularly helpful in scenarios where you do not want to open a jig to perform an action, for example, tapping on a widget opens a URL or a modal.

## Configuration options

| `onPress` | Choose from the provided list of available actions, for example, use the `open-url` action to open a specific URL. |
| --------- | ------------------------------------------------------------------------------------------------------------------ |

## Examples and code snippets

### Widget with onPress

{% columns %}
{% column %}
In this example, tapping on the widget opens the [info-modal](../../Actions/info-modal.md) to display information regarding Jigx.

**Examples**: See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x2/onpress_4x2.jigx).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZgGAqF9hDC6MTTMJC2h3i\_jw-widget-onpress.PNG" size="60" position="center" caption="Widget with onPress" alt="Widget with onPress"}&#x20;
{% endcolumn %}
{% endcolumns %}

{% code title="grid.jigx" %}
```yaml
  - type: component.grid-item
    options:
      size: "1x1"
      children: 
        type: component.jig-widget
        options:
          jigId: onpress_4x2    
          onPress: 
            type: action.info-modal
            options:
              modal:
                title: Welcome to Jigx
                buttonText: Close
                element: 
                  type: image
                  uri: https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nuSx_84sbGbtJlBxRWI5G_landingpage-s.gif?format=webp&width=1280
```
{% endcode %}
