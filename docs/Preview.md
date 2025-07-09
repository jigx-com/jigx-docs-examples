# Preview

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Add a preview for the following [Components](./Components.md):
\- [widgets](#)
\- [list-item](./Components/list/list-item.md)
\- [event](./Components/event.md)&#x20;
The preview is triggered by _long-pressing_ the widget or item. The _long-press_ action can be used on:

1. Widgets
2. List-items on widget
3. onPress action on list-item or event.
   :::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg" size="84" position="center" caption="Preview " alt="Preview" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg"}
:::
::::

### Configuration options

| **Core structure**                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actions`                         | These [actions (buttons)](<./Widgets/actions _buttons_.md>) can be added to the preview:<br>[action-list](./actions/action-list.md)<br>[execute-entities](./actions/execute-entities.md)<br>[execute-entity](./actions/execute-entity.md)<br>[go-to](./actions/go-to.md)<br>[open-url](./actions/open-url.md)<br>[reset-state](./actions/reset-state.md)<br>[set-state](./actions/set-state.md)<br>[sync-entities](./actions/sync-entities.md)<br>[confirm](./actions/confirm.md) |
| `children`                        | Two components available to use in a preview mode:[Entity](./Preview/Entity.md)                                                                                                                                                                                                                                                                                                                                                                                                   |
| [Web-view](./Preview/Web-view.md) |
| `header`                          | The [jig-header](./Components/jig-header.md) is can be part of the displayed preview.                                                                                                                                                                                                                                                                                                                                                                                             |
| `isCompact`                       | When set to `true` the size of the preview will be adjusted to its content.                                                                                                                                                                                                                                                                                                                                                                                                       |

:::hint{type="warning"}

1. Currently issues could be experienced when displaying the header's `title` and `subtitle` in the preview.
2. Using the `action.go-to` within an action [action-list](./Actions/action-list.md) does not trigger the preview popup.
   :::
