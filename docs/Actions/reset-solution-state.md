---
title: reset-solution-state
slug: 5aMt-reset
createdAt: Thu Jan 09 2025 07:36:32 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Feb 20 2025 08:26:41 GMT+0000 (Coordinated Universal Time)
---

This action affects the solution's overall state, allowing dynamic UI updates and logic control. Resetting the solution state removes any temporary data and returns it to its original, unmodified (default/initial value) state configuration.

## Configuration options

Some properties are common to all components, see [Common component properties](docId:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `changes`          | Specify the solution-state's `State Key` , the state will be reset to the initial solution state value for this key. |
| `title`            | Provide the action button with a title, for example, Reset.                                                          |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon](https://docs.jigx.com/jigx-icons) to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                        |
| `isHidden`        | `false` hides the action button, `true` shows the action button. Default setting is `true`.                                                                                                                                                                                                                                                                                                                                        |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Examples and code snippets

:::::ExpandableHeading

### Reset solution state

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem

:::

:::VerticalSplitItem

:::
::::

```yaml

```

:::::

:::::ExpandableHeading

### Reset solution state in the onRefresh event

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem

:::

:::VerticalSplitItem

:::
::::

```yaml

```

:::::

:::::ExpandableHeading

### Reset solution state in a jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem

:::

:::VerticalSplitItem

:::
::::

```yaml

```

:::::
