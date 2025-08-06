# Preview

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Add a preview for the following [Components](./Components.md):

- [widgets](Widgets.md)
- [list-item](./Components/list/list-item.md)
- [event](./Components/event.md)
  The preview is triggered by *long-pressing* the widget or item. The *long-press* action can be used on:

1. Widgets
2. List-items on widget
3. onPress action on list-item or event.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg" size="84" position="center" caption="Preview " alt="Preview" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4T0YtpHHfAVeSh0QvkAni_microsoftteams-image-6.jpg" width="800" height="1208" darkWidth="800" darkHeight="1208"}
:::
::::

## Configuration options

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `actions`          | These can be added to the preview:&#xA;[action-list](https://docs.jigx.com/examples/action-list)&#xA;[execute-entities](https://docs.jigx.com/examples/execute-entities)&#xA;[execute-entity](https://docs.jigx.com/examples/execute-entity)&#xA;[go-to](https://docs.jigx.com/examples/go-to)&#xA;[open-url](https://docs.jigx.com/examples/open-url)&#xA;[reset-state](https://docs.jigx.com/examples/reset-state)&#xA;[set-state](https://docs.jigx.com/examples/set-state)&#xA;[sync-entities](https://docs.jigx.com/examples/sync-entities)&#xA;[confirm](https://docs.jigx.com/examples/confirm) |
| `children`         | Two components available to use in a preview mode:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `header`           | The is can be part of the displayed preview.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `isCompact`        | When set to `true` the size of the preview will be adjusted to its content.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

:::hint{type="warning"}
1. Currently issues could be experienced when displaying the header's `title` and `subtitle` in the preview.
2. Using the `action.go-to` within an action [action-list](./Actions/action-list.md) does not trigger the preview popup.
:::

