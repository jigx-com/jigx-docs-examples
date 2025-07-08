---
title: Text (Alpha)
slug: lKrO-text
description: Learn how to add and style text in custom and standard components using the custom component "text". This document provides detailed instructions, configurations, and examples for aligning, coloring, decorating, emphasizing, and resizing text. Explore dif
createdAt: Tue Jun 06 2023 13:51:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 20:08:42 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="danger"}
This feature is currently in its **Alpha **stage of development.

- As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
- In this phase, the feature may contain bugs or behave unpredictably.
- Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
- We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.
  :::

The custom component _text_ allows adding text inside custom components. For example, adding text inside a [Card (Alpha)](<./Card _Alpha_.md>) or [View (Alpha)](<./View _Alpha_.md>).

For steps on creating a custom component, see [How to create a custom component](<./../Custom components _Alpha_.md>).

## Configuration options

You can use `when` and `instanceId` with `component.text`, add the properties before the `options` property. The available list of options is shown below.

| **Options**     | **value**                                                                                                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `align`         | Determine the text alignment, options are:&#xA;`center`&#xA;`left`&#xA;`right`                                                                                             |
| `color`         | Multiple, use IntelliSense to view the available list. See [Jigx color palette](https://docs.jigx.com/jigx-color-palette) to view the different colors.                    |
| `decoration`    | `line-through`&#xA;`underline`                                                                                                                                             |
| `emphasis`      | Change the text's brightness and boldness.&#xA;`high`&#xA;`low`&#xA;`low-medium`&#xA;`medium`                                                                              |
| `numberOfLines` | Use a number to indicate the number of lines of text.&#xA;Use an expression to determine the number of lines needed.                                                       |
| `onPress`       | Multiple, use IntelliSense to view the list of available [actions](<./../Widgets/actions _buttons_.md>) to call.                                                           |
| `size`          | Adjust the size of the text, the following sizes are available:&#xA;`extra-large`&#xA;`large`&#xA;`medium`&#xA;`regular`&#xA;`small`&#xA;`tiny`                            |
| `value`         | Provide the text to be used. You can use an [Expressions](https://docs.jigx.com/expressions), as well as [Localization](https://docs.jigx.com/localization).               |
| `weight`        | Determine how thick or bold the text must be, the following weights are available:&#xA;`bold`&#xA;`extra-bold`&#xA;`extra-light`&#xA;`light`&#xA;`regular`&#xA;`semi-bold` |

## Examples and code snippets

The examples use a set of custom components called _sections_. The sections are for titles, spacing, and context. The _sections_ code is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).

:::::ExpandableHeading

### Text font sizes

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-dxYQtS-bNSkPWJeZxXb-h-20241113-113134.png size="70" position="center" caption="Text font size" alt="Text font size"}
:::

:::VerticalSplitItem
This example shows the use of `component.text` with various font sizes configured using the `size` property, all displayed within a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).
2. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-1.jigx).
3. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-font-sizes.jigx).
   :::
   ::::

:::CodeblockTabs
text-1.jigx

```yaml
# components/text-1.jigx
type: component.default
children:
  - type: component.card
    options:
      color: color1
      direction: column
      children:
        - type: component.text
          options:
            value: Extra Large 123
            # Configure the font size of the text
            size: extra-large
        - type: component.text
          options:
            value: Large 123
            size: large
        - type: component.text
          options:
            value: Medium 123
            size: medium
        - type: component.text
          options:
            value: Regular 123
            size: regular
        - type: component.text
          options:
            value: Small 123
            size: small
        - type: component.text
          options:
            value: Tiny 123
            size: tiny
```

text-font-sizes.jigx

```yaml
# jigs/text-font-sizes.jigx
title: Text (Font Sizes)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Font sizes"
  # Reference the custom component to display in the jig.
  - type: component.custom-component
    componentId: text-1
```

:::
:::::

:::::ExpandableHeading

### Text with line through

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows how to apply strikethrough formatting to font of various sizes by using the `decoration: line-through` property of the `component.text`.

**Examples:**

1. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).
2. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-2.jigx).
3. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-line-through.jigx).
   :::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-qbyUXtdunBGIQRffCKP8C-20241113-113923.png" size="70" position="center" caption="Text with line through" alt="Text with line through"}
:::
::::

:::CodeblockTabs
text-2.jigx

```yaml
# components/text-line-through.jigx
type: component.default
children:
  - type: component.card
    options:
      color: color2
      direction: column
      children:
        - type: component.text
          options:
            value: Extra Large
            size: extra-large
            # decorate the text with a line through the text value
            decoration: line-through
        - type: component.text
          options:
            value: Large
            size: large
            decoration: line-through
        - type: component.text
          options:
            value: Medium
            size: medium
            decoration: line-through
        - type: component.text
          options:
            value: Regular
            size: regular
            decoration: line-through
        - type: component.text
          options:
            value: Small
            size: small
            decoration: line-through
        - type: component.text
          options:
            value: Tiny
            size: tiny
            decoration: line-through
```

\# text-line-through.jigx

```yaml
# jigs/text-line-through.jigx
title: Text (Line-through)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Line through"
  # Reference the custom component to display in the jig.
  - type: component.custom-component
    componentId: text-2
```

:::
:::::

:::::ExpandableHeading

### Text with underlining

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Hw1klMA74o6_8I9xaduNU-20241113-114815.png" size="70" position="center" caption="Underlined text" alt="Underlined text"}
:::

:::VerticalSplitItem
This example shows how to underline text with various font sizes using the `decoration: underline` property. The text is contained in a yellow [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-3.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-underline.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::
::::

:::CodeblockTabs
text-3.jigx

```yaml
# components/text-3.jigx
type: component.default
children:
  - type: component.card
    options:
      color: color3
      direction: column
      children:
        - type: component.text
          options:
            value: Extra Large
            size: extra-large
            # Underline text be using the decoration property.
            decoration: underline
        - type: component.text
          options:
            value: Large
            size: large
            decoration: underline
        - type: component.text
          options:
            value: Medium
            size: medium
            decoration: underline
        - type: component.text
          options:
            value: Regular
            size: regular
            decoration: underline
        - type: component.text
          options:
            value: Small
            size: small
            decoration: underline
        - type: component.text
          options:
            value: Tiny
            size: tiny
            decoration: underline
```

\# text-underline.jigx

```yaml
# jigs/text-custom-component.jigx
title: Text (Underline)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Underline"
  # Reference the custom component to display in the underlined text in the jig.
  - type: component.custom-component
    componentId: text-3
```

:::
:::::

:::::ExpandableHeading

### Text with emphasis

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows the `component.text` with various font sizes and emphasis styles, configured using the `emphasis` property, all displayed in a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-4.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-emphasis.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-QEETvY3gSRqzzh4tSWD1V-20241113-115730.png" size="70" position="center" caption="Text with emphasis" alt="Text with emphasis"}
:::
::::

:::CodeblockTabs
text-4.jigx

```yaml
# components/text-4.jigx
type: component.default
children:
  - type: component.card
    options:
      color: color4
      direction: column
      children:
        - type: component.text
          options:
            value: High
            size: extra-large
            #Add emphasis to text from bright to lighter
            emphasis: high

        - type: component.text
          options:
            value: Medium
            size: extra-large
            emphasis: medium

        - type: component.text
          options:
            value: Low medium
            size: extra-large
            emphasis: low-medium

        - type: component.text
          options:
            value: Low
            size: extra-large
            emphasis: low
```

text-emphasis.jigx

```yaml
# jigs/text-emphasis.jigx
title: Text (Emphasis)
type: jig.default
icon: text-book

children:
  - type: component.custom-component
    # Reference the custom component to display in the jig.
    # This custom component contains the view configuration to show the title.
    componentId: section2
    inputs:
      title: "Emphasis"
  # Reference the custom component to display text with emphasis in the jig.
  - type: component.custom-component
    componentId: text-4
```

:::
:::::

:::::ExpandableHeading

### Text with alignment

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-b39lj_DjMe63LB7r_FopZ-20241113-120533.png" size="70" position="center" caption="Text alignment" alt="Text alignment"}
:::

:::VerticalSplitItem
This example demonstrates various text alignments with varying font sizes using the `align` property, all displayed in a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-5.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-alignment.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::
::::

:::CodeblockTabs
text-5.jigx

```yaml
# components/text-5.jigx
type: component.default
children:
  - type: component.card
    options:
      color: color5
      direction: column
      children:
        - type: component.text
          options:
            value: Extra Large
            size: extra-large
            # Determine the alignment of the text value
            align: right
        - type: component.text
          options:
            value: Large
            size: large
            align: right
        - type: component.text
          options:
            value: Medium
            size: medium
            align: center
        - type: component.text
          options:
            value: Regular
            size: regular
            align: center
        - type: component.text
          options:
            value: Small
            size: small
            align: left
        - type: component.text
          options:
            value: Tiny
            size: tiny
            align: left
```

\# text-alignment.jigx

```yaml
# jigs/text-alignment.jigx
title: Text (Alignment)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Alignment"
  # Reference the custom component to display text with alignment in the jig.
  - type: component.custom-component
    componentId: text-5
```

:::
:::::

:::::ExpandableHeading

### Text over multiple lines

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how to control the number of text lines displayed in `component.text` using the `numberOfLines:` property, with the content displayed inside a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-6.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-number-lines.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-MjqAbpfVvW0TjoP4M-L2z-20241113-121315.png" size="70" position="center" caption="Multiple lines of text" alt="Multiple lines of text"}
:::
::::

:::CodeblockTabs
text-6.jigx

```yaml
# components/text-6.jigx
type: component.default
children:
  - type: component.card
    options:
      direction: column
      children:
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: extra-large
            # Determine how many lines of the text value can run over.
            numberOfLines: 3
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: large

            numberOfLines: 5
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: medium

            numberOfLines: 3
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: regular
            numberOfLines: 3
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: small
            numberOfLines: 3
        - type: component.text
          options:
            value: is designed to be inclusive, so remote team members truly feel like part of the group. By being able to use your own device, everyone is seen and heard clearly — and no one ever sounds “far from the mic.” Everyone stays engaged. No one steals the spotlight.
            size: tiny
            numberOfLines: 3
```

text-number-lines.jigx

```yaml
# jigs/text-number-lines.jigx
title: Text (Number Lines)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Number of lines"
  # Reference the custom component to display text spread over multiple lnies in the jig.
  - type: component.custom-component
    componentId: text-6
```

:::
:::::

:::::ExpandableHeading

### Text with color

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NDvPVznGR9XU44dCTG1Mm-20241113-122018.png" size="70" position="center" caption="Text with color" alt="Text with color"}
:::

:::VerticalSplitItem
This example shows how to set the color of text of varying font sizes, and spread over a number of lines by using the `color:` property, with the content displayed in a [Card (Alpha)](<./Card _Alpha_.md>).

**Examples:**

1. See the _custom component_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-7.jigx).
2. See the _jig_ example in [GitHub]("https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-colored.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::
::::

:::CodeblockTabs
text-7.jigx

```yaml
# components/text-7.jigx
type: component.default
children:
  - type: component.card
    options:
      direction: column

      children:
        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: extra-large
            numberOfLines: 3
            # Change the color of the text value.
            color: primary
        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: large
            numberOfLines: 3
            color: color1
        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: medium
            numberOfLines: 3
            color: color2

        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: regular
            numberOfLines: 3
            color: color3

        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: small
            numberOfLines: 3
            color: color4

        - type: component.text
          options:
            value: Is designed to be inclusive, so remote team members truly feel like part of the group.
            size: tiny
            numberOfLines: 3
            color: color5
```

\# text-colored.jigx

```yaml
# jigs/text-colored.jigx
title: Text (Colored)
type: jig.default
icon: text-book

children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: "Colored text"
  # Reference the custom component to display text in different colors in the jig.
  - type: component.custom-component
    componentId: text-7
```

:::
:::::

::::ExpandableHeading

### Text weights&#x20;

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4ZloD22zynAUqeBo0e5---20241113-130811.png" size="92" position="center" caption="text weights" alt="text weights"}

These examples demonstrate the various options for using text weights to ensure thickness and boldness of text combined with varying sizes, displayed in a [Card (Alpha)](<./Card _Alpha_.md>). By combining the `size`, and `weight` properties, you can achieve the desired appearance.

**Examples:**

1. See the _custom component_ example in <[GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/text/text-11.jigx).
2. See the _jig_ example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/basic-elements/text/text-regular-weights.jigx).
3. See the _section_ component example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/sections/section2.jigx).

:::CodeblockTabs
text-11.jigx

```yaml
# components/text-11.jigx
# See the YAML for text-8.jigx to text-13.jigx in GitHub,
# for the other weight examples, link provided above.
type: component.default
children:
  - type: component.card
    options:
      color: color6
      direction: column
      children:
        - type: component.text
          options:
            value: Extra Bold
            size: regular
            # Change the thickness and boldness of the text value.
            weight: extra-bold
        - type: component.text
          options:
            value: Bold
            size: regular
            weight: bold
        - type: component.text
          options:
            value: Semi Bold
            size: regular
            weight: semi-bold
        - type: component.text
          options:
            value: Regular
            size: regular
            weight: regular
        - type: component.text
          options:
            value: Light
            size: regular
            weight: light
        - type: component.text
          options:
            value: Extra light
            size: regular
            weight: extra-light
```

\# text-regular-weights.jigx

```yaml
# jigs/text-custom-component.jigx
title: Text
type: jig.default
icon: chat
children:
  # Reference the custom component to display in the jig.
  # This custom component contains the view configuration to show the title.
  - type: component.custom-component
    componentId: section2
    inputs:
      title: Extra large - Font Weights
  # Reference the custom component to display in the jig.
  - type: component.custom-component
    componentId: text-font-weights-extra-large
```

:::
::::
