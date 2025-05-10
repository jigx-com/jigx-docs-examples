---
title: Preview
slug: wgp2-overview
description: Learn how to add a preview to widgets, list-items, and events by long-pressing them with this comprehensive document. Adjust the preview size based on your content using the "isCompact" configuration option. Explore the available child components such as 
createdAt: Tue Feb 14 2023 10:07:05 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Mar 07 2024 08:56:23 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Add a preview for the following [Components](./Components.md):
\- [widgets]()
\- [list-item](./Components/list/list-item.md)
\- [event](./Components/event.md)&#x20;
The preview is triggered by *long-pressing* the widget or item. The *long-press* action can be used on:

1. Widgets
2. List-items on widget
3. onPress action on list-item or event.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg" size="84" position="center" caption="Preview " alt="Preview"}
:::
::::

### Configuration options

| **Core structure** | s                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `actions`          | These [actions (buttons)](<./Widgets/actions _buttons_.md>) can be added to the preview :<br />* [action-list](./Actions/action-list.md)
* [confirm](./Actions/confirm.md)
* [execute-entities](./Actions/execute-entities.md)
* [execute-entity](./Actions/execute-entity.md)
* [go-to](./Actions/go-to.md)
* [open-url](./Actions/open-url.md)
* [reset-state](./Actions/reset-state.md)
* [set-state](./Actions/set-state.md)
* [sync-entities](./Actions/sync-entities.md) |
| `children`         | Two components available to use in a preview mode:<br />* [Entity](./Preview/Entity.md)
* [Web-view](./Preview/Web-view.md)                                            |
| `header`           | The [jig-header](./Components/jig-header.md) is can be part of the displayed preview.                                                                              |
| `isCompact`        | When set to `true` the size of the preview will be adjusted to its content.                                                                                            |

:::hint{type="warning"}
1. Currently issues could be experienced when displaying the header's `title` and `subtitle` in the preview.
2. Using the `action.go-to` within an action [action-list](./Actions/action-list.md) does not trigger the preview popup.
:::

