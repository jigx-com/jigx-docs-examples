---
title: Icon (Alpha)
slug: rCAT-i
description: Learn how to use the `component.icon` to enhance the style of standard or custom components with this step-by-step guide. Explore examples and code snippets for different icon sizes and styles. Create custom icon components in various shapes and sizes wit
createdAt: Tue Jun 06 2023 13:53:41 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 19:58:43 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="danger"}
This feature is currently in its **Alpha **stage of development.

- As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
- In this phase, the feature may contain bugs or behave unpredictably.
- Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
- We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.
  :::

The icon component can be integrated into custom components to enhance their visual appeal and functionality, such as adding an icon within a [Button (Alpha)](<./Button _Alpha_.md>) , displaying it in a [Card (Alpha)](<./Card _Alpha_.md>) , or embedding it in a [View (Alpha)](<./View _Alpha_.md>) . By customizing an icon, you can adjust its size, color, and shape, and even apply animations or conditional styling, ensuring seamless alignment with your application's design system and user experience.

For steps on creating a custom component, see [How to create a custom component](<./../Custom components _Alpha_.md>).

## Configuration options

You can use `when` and `instanceId` with `component.icon`, add the properties before the `options:` property. The available list of options is shown below. For the full list of properties, see [jc-icon](https://docs.jigx.com/jigx-icons) .

| **Options** | **value**                                                                                                                                                                          |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`     | Multiple, use IntelliSense to view the available list.                                                                                                                             |
| `emphasis`  | Changing the color, for example, brighter, bolder, or a contrasting hue.&#xA;`extra-low`&#xA;`high`&#xA;`low`&#xA;`low-medium`&#xA;`medium`                                        |
| `onPress`   | Multiple, use IntelliSense to view the list of available [actions](<./../Widgets/actions _buttons_.md>) to call. The action is called when the icon is pressed.                    |
| `shape`     | Determine the shape around the icon.&#xA;`circle`&#xA;`rounded` (default)&#xA;`square`                                                                                             |
| `size`      | Enter a number value or use an expression to determine the size of the icon.                                                                                                       |
| `type`      | Configure the icon's display as a standalone icon, within a shape, or in a duotone style. The following options are available:&#xA;`basic` (default)&#xA;`duotone`&#xA;`contained` |

## Examples and code snippets

The examples use a set of custom components called _sections_. The sections are for titles, spacing, and context. The _sections_ code is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).

:::::ExpandableHeading

### Icon sizes

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows the `component.icon` with different icon sizes using the `size:` property in a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section4.jigx).
2. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/icons/icon-sizes.jigx).
3. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/icons/icons-sizes.jigx).
   :::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-fr7_n4lVvW220aIUVfsGR-20241113-084145.png" size="70" position="center" caption="Icon sizes" alt="Icon sizes"}
:::
::::

:::CodeblockTabs
icon-sizes.jigx &#x20;

```yaml
# components/icon-sizes.jigx
type: component.default
children:
  - type: component.card
    options:
      children:
        - type: component.text
          options:
            value: Extra large
            emphasis: medium
            align: center
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon by typing the first two letters to invoke the list.
            icon: animation
            # Configure the size of the icon.
            size: extra-large

        - type: component.text
          options:
            value: Large
            emphasis: medium
            align: center
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon by typing the first two letters to invoke the list.
            icon: animation
            # Configure the size of the icon.
            size: large

        - type: component.text
          options:
            value: Medium
            emphasis: medium
            align: center
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon by typing the first two letters to invoke the list.
            icon: animation
            # Configure the size of the icon
            size: medium

        - type: component.text
          options:
            value: Regular
            emphasis: medium
            align: center
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon by typing the first two letters to invoke the list.
            icon: animation
            # Configure the size of the icon.
            size: regular

        - type: component.text
          options:
            value: Small
            emphasis: medium
            align: center
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon by typing the first two letters to invoke the list.
            icon: animation
            # Configure the size of the icon.
            size: small
```

icons-sizes.jigx

```yaml
# jigs/icons-sizes.jigx
title: Icons Sizes
type: jig.default
icon: pen-draw-1

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section4
    inputs:
      title: "Icon sizes"
  # Reference the custom component to display the icon sizes in the jig.
  - type: component.custom-component
    componentId: icon-sizes
```

:::
:::::

::::ExpandableHeading

### Icon shapes & types

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-qvyB3bcmZhUZFyyIrWOHN-20241113-103827.png" size="76" position="center" caption="Icon shapes" alt="Icons shapes"}

These examples demonstrate the various options for using icons with rounded, square and circled shapes in a [Card (Alpha)](<./Card _Alpha_.md>). By combining the `shape`, `type`, and `size` properties, you can achieve the desired appearance.

**Examples:**

1. See the _custom components_ example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/basic-elements/icons) for icons-1.0.jigx to icons-3.5.jigx.
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/icons).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).

:::CodeblockTabs
icon-1.0.jigx

```yaml
# components/icon-1.0.jigx
# See the YAML for icon-1.1.jigx to icon-1.5.jigx in GitHub, link provided above.
type: component.default
children:
  - type: component.card
    options:
      direction: row
      children:
        - type: component.icon
          options:
            icon: animation
            size: extra-large
            # Change the shape to circle or square to see the icon appearance change.
            shape: rounded
            type: basic

        - type: component.icon
          options:
            icon: animation
            size: large
            shape: rounded
            type: basic

        - type: component.icon
          options:
            icon: animation
            size: medium
            shape: rounded
            type: basic

        - type: component.icon
          options:
            icon: animation
            size: regular
            shape: rounded
            type: basic

        - type: component.icon
          options:
            icon: animation
            size: small
            shape: rounded
            type: basic
```

icons-rounded.jigx

```yaml
# jigs/icons-rounded.jigx
# See the YAML for sections in GitHub, link provided above.
title: Icons (Rounded)
type: jig.default
icon: pen-draw-1

children:
  - type: component.custom-component
    componentId: section4
    inputs:
      title: "1. Rounded"
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.0 - Basic"
  - type: component.custom-component
    componentId: icons-1.0
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.1 - Contained"
  - type: component.custom-component
    componentId: icons-1.1
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.2 - Duotone"
  - type: component.custom-component
    componentId: icons-1.2
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.3 - Card with color"
  - type: component.custom-component
    componentId: icons-1.3
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.4 - Icons with color"
  - type: component.custom-component
    componentId: icons-1.4
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "1.5 - Card with color + Icons with color"
  - type: component.custom-component
    componentId: icons-1.5
```

:::
::::

:::::ExpandableHeading

### Icon bar

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Create an icon bar within in a `component.card` by configuring multiple `component.icon`. Add an `onPress` event to each icon that opens its associated URL. You can configure the `onPress` event to call various available [actions](./../Actions.md).

**Example:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/icons/icons.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/icons/icons-bar.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ldb9jwQQ5se9SWGcUOMRO-20241113-104500.png" size="70" position="center" caption="Icon bar" alt="Icon bar"}
:::
::::

:::CodeblockTabs
icons.jigx

```yaml
# components/icons.jigx
type: component.default
children:
  # Configure a card to contain the icons in a row.
  - type: component.card
    options:
      direction: row
      children:
        # Add the icon component.
        - type: component.icon
          options:
            # Choose an icon.
            icon: shopping-cart-empty-1
            size: large
            # Configure the onPress event to call an action,
            # in this example when the icon is pressed a URL will open.
            onPress:
              type: action.open-url
              options:
                url: https://www.amazon.com

        - type: component.icon
          options:
            # Choose an icon.
            icon: mindfullness
            size: large
            # Configure the onPress event to call an action,
            # in this example when the icon is pressed a URL will open.
            onPress:
              type: action.open-url
              options:
                url: https://www.calm.com

        - type: component.icon
          options:
            # Choose an icon.
            icon: weather
            size: large
            # Configure the onPress event to call an action,
            # in this example when the icon is pressed a URL will open.
            onPress:
              type: action.open-url
              options:
                url: https://www.accuweather.com

        - type: component.icon
          options:
            # Choose an icon.
            icon: single-neutral
            size: large
            # Configure the onPress event to call an action,
            # in this example when the icon is pressed a URL will open.
            onPress:
              type: action.open-url
              options:
                url: https://www.linkedin.com

        - type: component.icon
          options:
            # Choose an icon.
            icon: location
            size: large
            # Configure the onPress event to call an action,
            # in this example when the icon is pressed a URL will open.
            onPress:
              type: action.open-url
              options:
                url: https://www.google.com/maps/
```

icons-bar.jigx

```yaml
# jigs/icons-bar.jigx
title: Icons Bar
type: jig.default
icon: picture-polaroid-human

children:
  - type: component.custom-component
    componentId: icons
```

:::
:::::
