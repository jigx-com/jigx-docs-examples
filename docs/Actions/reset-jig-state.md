---
title: reset-jig-state
slug: ibTc-rest
createdAt: Thu Jan 09 2025 07:36:05 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Apr 25 2025 06:58:40 GMT+0000 (Coordinated Universal Time)
---

Actions for modifying or resetting various application states. These operations affect components, jigs, solutions, or the overall state, allowing dynamic UI updates and logic control. Proper management ensures consistent updates across the app. Resetting of states removes any data and returns it to its original, unmodified state and default configuration.

## Configuration options

| **Core structure** |                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `changes`          | Specify the jig-state's `State Key` , the state will be reset to the initial jig state value for this key. |
| `title`            | Provide the action button with a title, for example, Revert.                                               |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon](https://docs.jigx.com/jigx-icons) to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                        |
| `isHidden`        | `false` hides the action button, `true` shows the action button. Default setting is `true`.                                                                                                                                                                                                                                                                                                                                        |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |
