# video-player

This component is used to play a video in [headers](./jig-header.md), or as components in a [jig.default](<./../Jig Types/jig_default.md>).

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `URL`              | Specify the URL for the video. The URL format can be:&#xA;- A direct URL, for example, [https://player.vimeo.com/video/76979871&#xA;](https://player.vimeo.com/video/76979871)- An embeded URL, for example,&#xA;`<iframe src="https://player.vimeo.com/video/76979871?quality=720p"></iframe>`<br />-A URL referenced in a datasource, for example, &#xA;`url: =@ctx.datasources.video-player-dynamic.uri` |

| **Other options** |                                                                                                                                                                                                                                                                                                                                          |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `autoplay`        | Set to `true` will automatically start playing the video. Set to `false` requires you to press the play button. Default setting is `false`.                                                                                                                                                                                              |
| `loop`            | For continuous looping of the video set the property to `true`. Default setting is `false`.                                                                                                                                                                                                                                              |
| `ratio`           | There are 2 options:&#xA;- 16:9&#xA;- 4:3                                                                                                                                                                                                                                                                                                |
| `title`           | The title of the video.&#xA;-With a `16:9` ratio, the text overlays at the bottom left of the video. <br />-With a `4:3` ratio the text displays under the video.&#xA;`Title` and `subtitle` must be configured together for the text to display on the video. Using either one on their own will result in no text being displayed.     |
| `subtitle`        | The subtitle of the video. &#xA;-With a `16:9` ratio, the text overlays at the bottom left of the video. <br />-With a `4:3` ratio the text displays under the video.&#xA;`Title` and `subtitle` must be configured together for the text to display on the video. Using either one on their own will result in no text being displayed. |

## Considerations

- We recommend using a paid Vimeo subscription which gives you access to the mp4 link that allows the byline and other attributes to be hidden. You require a paid Vimeo membership to obtain the mp4 Vimeo link. Follow the steps in [Vimeo direct links to video files](https://help.vimeo.com/hc/en-us/articles/12426150952593-Direct-links-to-video-files) to copy the mp4 link.
- For Vimeo videos, set up your OAuth token once in the Vimeo app and then use it for all videos. See the following resources on creating tokens:
  1. [How-do-I-create-an-API-app](https://help.vimeo.com/hc/en-us/articles/12427832381457-How-do-I-create-an-API-app)
  2. [How-do-I-generate-a-personal-access-token](https://help.vimeo.com/hc/en-us/articles/12427789081745-How-do-I-generate-a-personal-access-token#:~\:text=Go%20to%20your%20Apps%20page,metadata%20public%20on%20vimeo.com.)
  3. [How-can-I-test-the-API-on-the-Developer-Site](https://help.vimeo.com/hc/en-us/articles/12427789133201-How-can-I-test-the-API-on-the-Developer-Site).
- When configuring video settings for Vimeo and YouTube videos, preferably use the settings within the respective apps first before setting URL parameters, this ensure videos display as expected in the Jigx App.

## Examples and code snippets

:::::ExpandableHeading
### Video player as children of the jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-kpulDNlHd1-TlkW_6Hc0_cc-videoinjig.PNG" size="80" position="center" caption="video-player" alt="video-player" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-kpulDNlHd1-TlkW_6Hc0_cc-videoinjig.PNG"}
:::

:::VerticalSplitItem
This example shows a video player inside a jig. The ratio is only set for non-YouTube videos.

**Examples**:
See the full example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/video-player/static-data/video-player-in-jig/video-player-in-jig.jigx).
See the full example using dynamic data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/video-player/dynamic-data/video-player-in-jig/video-player-jig-dynamic.jigx).

**Datasource**:
See the full datasource for dynamic data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/video-player-dynamic.jigx).
:::
::::

:::CodeblockTabs
videoplayer (static)

```yaml
children:
  - type: component.video-player
    options:
      url: https://cdn.pixabay.com/video/2021/09/15/88697-606080045_small.mp4
      title: Team work
      subtitle: Video-player usage examples
      autoplay: false
      loop: true
      ratio: "4:3"
```

videoplayer (dynamic)

```yaml
children:
  - type: component.video-player
    options:
      url: =@ctx.datasources.video-player-dynamic.uri
      title: =@ctx.datasources.video-player-dynamic.title
      subtitle: =@ctx.datasources.video-player-dynamic.subtitle
      autoplay: false
      loop: true
      ratio: "4:3"
```

datasources (dynamic)

```yaml
datasources:
  video-player-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/links
      query: |
        SELECT
          '$.uri',
          '$.title',
          '$.subtitle',
          '$.category'
        FROM [default/links] WHERE '$.category' = "video-player"
```
:::
:::::

:::::ExpandableHeading
### Video player in header

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/syc3quPN1_3GaWZtNVxPY_cc-videoinheader.PNG" size="80" position="center" caption="video - player" alt="video - player" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/syc3quPN1_3GaWZtNVxPY_cc-videoinheader.PNG"}
:::

:::VerticalSplitItem
This example shows the video player as a jig header. Ideal for product videos.

**Examples:**

See the complete example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/video-player/static-data/video-player-in-header/video-player-in-header.jigx).
See the complete example using dynamic data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/video-player/dynamic-data/video-player-in-header/video-player-header-dynamic.jigx).

**Datasource**:
See the complete datasource for dynamic data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/samples/jigx-samples/datasources/adhoc-components/video-player-dynamic.jigx).
:::
::::

:::CodeblockTabs
videoplayer-header (static)

```yaml
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.video-player
      options:
        url: https://cdn.pixabay.com/video/2023/10/01/183108-870151713_small.mp4
        autoplay: true
        loop: true
        ratio: "16:9"
```

videoplayer-header (dynamic)

```yaml
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.video-player
      options:
        url: =@ctx.datasources.video-player-dynamic.uri
        autoplay: true
        loop: true
        ratio: "16:9"
```

datasources (dynamic)

```yaml
datasources:
  video-player-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/links
      query: |
        SELECT
          '$.uri',
          '$.title',
          '$.subtitle',
          '$.category'
        FROM [default/links] WHERE '$.category' = "video-player"
```
:::
:::::

