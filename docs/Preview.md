# Preview

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Add a preview for the following [Components](./Components.md):
\- [widgets](#)
\- [list-item](./Components/list/list-item.md)
\- [event](./Components/event.md)&#x20;
The preview is triggered by *long-pressing* the widget or item. The *long-press* action can be used on:

1. Widgets
2. List-items on widget
3. onPress action on list-item or event.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg" size="84" position="center" caption="Preview " alt="Preview" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg"}
:::
::::

### Configuration options

| **Core structure** |                                                                                                                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actions`          | These [actions (buttons)](<./Widgets/actions _buttons_.md>) can be added to the preview:<br />* [action-list]()
* [execute-entities]()
* [execute-entity]()
* [go-to]()
* [open-url]()
* [reset-state]()
* [set-state]()
* [sync-entities]()
* [confirm]() |
| `children`         | Two components available to use in a preview mode:<br />*  [Entity](./Preview/Entity.md)
* [Web-view](./Preview/Web-view.md) &#x20;                                                                                                                        |
| `header`           | The [jig-header](./Components/jig-header.md) is can be part of the displayed preview.                                                                                                                                                                      |
| `isCompact`        | When set to `true` the size of the preview will be adjusted to its content.                                                                                                                                                                                |

:::hint{type="warning"}
1. Currently issues could be experienced when displaying the header's `title` and `subtitle` in the preview.
2. Using the `action.go-to` within an action [action-list](./Actions/action-list.md) does not trigger the preview popup.
:::

