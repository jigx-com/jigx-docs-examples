---
title: set-solution-state
slug: 10ZM-set
createdAt: Thu Jan 09 2025 07:35:40 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Feb 20 2025 08:26:16 GMT+0000 (Coordinated Universal Time)
---

This action affects solutions, allowing dynamic UI updates and logic control. Proper management ensures consistent updates across the app. The setting of states updates the global solution state, acting as a global variable accessible by multiple jigs and components.

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| ### Core structure | ****                                                                                                              |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `changes`          | Specify the solution-state's `State Key` and provide the new state value using an expression, text or datasource. |
| `title`            | Provide the action button with a title, for example, Update.                                                      |

| ### Other options |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon]() to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                                                        |
| `isHidden`        | `false` hides the action button, `true` shows the action button. Default setting is `true`.                                                                                                                                                                                                                                                                                                                                        |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Considerations

- Multiple states can be added in index.jigx.
- Supports `initialValues` as nested objects.&#x20;

## Examples and code snippets 

:::::ExpandableHeading
### Set solution state

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
### Set solution state in the onFocus event

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
### Set and reset solution state in a jig (not sure this is makes sense?)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem

:::

:::VerticalSplitItem

:::
::::

```yaml
```
:::::



###

