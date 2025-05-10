---
title: actions (buttons)
slug: NnWj-actions
description: Learn how to enhance your widget by adding primary and secondary actions without the need to access the widget first. This document covers configuration options and examples for our versatile actions widget, which can be configured both within the widget 
createdAt: Thu Jun 09 2022 20:13:44 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Mar 10 2025 08:28:52 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This widget allows you to add primary and/or secondary actions (buttons) to a widget. This is a quick way for users to perform actions without needing to access a jig through the widget first.

- Any of the actions that are available in the [Actions](./../Actions.md) section can be configured on the widget.
- This widget can be configured in a [group](<./Content widget components/group.md>) widget, which allows you to group the actions with other widget types.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bXQzrMgA9C2WU-VcYpOYU_wd-actions.png" size="58" position="center" caption="Action widget"}
:::
::::

## ****Configuration options

| **Core structure** |                                                                        |
| ------------------ | ---------------------------------------------------------------------- |
| `onPress`          | Configure the action to be executed when the action button is pressed. |
| `title`            | Display the text content for the title.                                |

| **Other options** |                                                                                                       |
| ----------------- | ----------------------------------------------------------------------------------------------------- |
| `footer`          | Add text to the footer of the widget.                                                                 |
| `footerAlign`     | Align the footer text to `left`, `right`, `center`.                                                   |
| `placeholders`    | Specify a placeholder text to display if there is no data, for example - `title: No data to display`. |
| `primary`         | Configure a `title` and onPress properties for a primary action button.                               |
| `secondary`       | Configure a `title` and `onPress` properties for a secondary action button.                           |

## Examples and code snippets

:::::ExpandableHeading
### Example of actions widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VtuoNb4XzobXvjv_YNiP9_actionsiphone13blueportrait.png" size="80" position="center" caption="Actions widget" alt="Actions widget"}
:::

:::VerticalSplitItem
Here is an example of the actions button on the widget level. When the primary button is pressed, an avatar is shown, and when the secondary button (white with blue text) is pressed, the color palette is shown.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/action/actions.jigx).
:::
::::

:::CodeblockTabs
actions-widget

```yaml
widgets:
  actions-2x2:
    type: widget.actions
    options:
      footer: Show more
      footerAlign: center
      primary:
        title: Avatar info
        onPress:
          type: action.go-to
          options:
            linkTo: avatar-field-example
      secondary:
        title: Color palette
        onPress:
          type: action.go-to
          options:
            linkTo: color-palete
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
          jigId: actions-widget
          widgetId: actions-2x2
```
:::
:::::

