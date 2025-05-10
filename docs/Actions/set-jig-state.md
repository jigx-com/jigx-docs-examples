---
title: set-jig-state
slug: aVwm-set
createdAt: Thu Jan 09 2025 07:34:47 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 26 2025 09:42:10 GMT+0000 (Coordinated Universal Time)
---

This action affects jigs, allowing dynamic UI updates and logic control. Setting the jig state updates the state of the jig, acting as a jig variable accessible by the instance of the jig and components.

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `changes`          | Specify the jig-state's `State Key` and provide the new state value using an expression, text or datasource. |
| `title`            | Provide the action button with a title, for example, Save.                                                   |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon]() to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                                                        |
| `isHidden`        | `false` hides the action button, `true` shows the action button. Default setting is `true`.                                                                                                                                                                                                                                                                                                                                        |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

