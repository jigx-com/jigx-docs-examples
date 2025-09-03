# image

{% columns %}
{% column %}
You can use this component as a unique visual identifier. Display a profile photo, company logo, photo of products, and much more to improve your application's visual experience.

The `image` component can be part of the [header](jig-header.md) and as a child component in [jig.default](<../Jig Types/jig_default.md>).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/cc-image-intro.png" alt="Image Preview"><figcaption><p>Image Preview</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Configuration options

Some properties are common to all components, see [Common component properties](image.md) for a list and their configuration options.

<table><thead><tr><th width="151.33984375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>uri</code></td><td>The image source (either a remote URL or a local file resource). The currently supported formats are png, jpg, jpeg, bmp, gif, webp (Android only), psd (iOS only).</td></tr></tbody></table>

<table><thead><tr><th width="156.54296875">Other options</th><th></th></tr></thead><tbody><tr><td><code>height</code></td><td>Change the height of the image in pixels. Ensure a proper <code>resizeMode</code> is used to achieve the best results on different device resolutions. The default is set at 196 pixels.</td></tr><tr><td><code>resizeMode</code></td><td><p>Resize the image when the frame doesn't match the raw image dimensions. The following options are available:</p><ul><li><code>center</code> - If the image is bigger than the area it is scaled down making it completely visible. The image is not scaled up.</li><li><code>contain</code> - Scales the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or less than the corresponding dimension of the view (minus padding).</li><li><code>cover</code> - Scales the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or larger than the corresponding dimension of the view (minus padding).</li><li><code>stretch</code> - Scales the width and height of the image independently, This may change the aspect ratio of the <code>source</code>.</li></ul></td></tr><tr><td><code>subtitle</code></td><td>Adds a subtitle that is displayed on or next to the image based on image context.</td></tr><tr><td><code>title</code></td><td>Display the text content for the title that can be displayed on or next to the image based on the image context.</td></tr><tr><td><code>width</code></td><td>Change the width of the image in pixels. Ensure a proper <code>resizeMode</code> is used to achieve the best results on different device resolutions.</td></tr></tbody></table>

<table><thead><tr><th width="158.0703125">Actions</th><th></th></tr></thead><tbody><tr><td><code>onPress</code></td><td>The action is triggered when pressing on the image. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

## Considerations

* Dynamic Data cannot save images larger than 350K. Jigx does not recommend storing images in Dynamic Data or storing images as base64 in the Dynamic Data database.
* The images can be preloaded and cached using the asset folder's images file. The images will be displayed even when you are offline. For more details, refer to [Assets](https://docs.jigx.com/assets).

## Examples and code snippets

### Image in Header

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/cc-image-header.png" alt="Image in header" width="177"><figcaption><p>Image in header</p></figcaption></figure>
{% endcolumn %}

{% column %}
Image is used as a background picture in the header section.

**Examples:** See the example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/image/static-data/header-image/header-image.jigx). See the example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/image/dynamic-data/header-image/header-image-dynamic.jigx).

**Datasource:** See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/image-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/image.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="header (static)" %}
```yaml
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        title: Header image
        source:
          uri: =@ctx.datasources.story-static[0].image
```
{% endtab %}

{% tab title="header (dynamic)" %}
```yaml
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        title: Header image
        source:
          uri: =@ctx.datasources.story[2].photo
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  story-static:
    type: datasource.static
    options:
      data:
        - title: Work productivity
          description: How To Be More Productive at Work
          image: https://images.unsplash.com/photo-1456324504439-367cee3b3c32?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          thumbnail: https://images.unsplash.com/photo-1513128034602-7814ccaddd4e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80
          url: https://www.indeed.com/career-advice/career-development/ways-to-be-more-productive
          videoUrl: https://www.youtube.com/watch?v=4aYVLpY5FYU
        - title: Work productivity
          description: Reasons Why You are Not as Productive as You Can Be
          image: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          thumbnail: https://images.unsplash.com/photo-1609659893022-8a02377d8b08?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          url: https://www.lifehack.org/articles/productivity/8-reasons-productive-can-fix.html
          videoUrl: https://www.youtube.com/watch?v=z-7LPjiYBHU
        - title: Work productivity
          description: How to Stay Productive When Working From Home
          image: https://images.unsplash.com/photo-1620862657788-a403bdf6dd63?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1742&q=80
          thumbnail: https://images.unsplash.com/photo-1589591830600-7ba977995a5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          url: https://www.travelers.com/resources/home/working-remotely/10-tips-for-staying-productive-when-working-from-home
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  story:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/avatar
      query: |
        SELECT
          id,
          '$.category',
          '$.description',
          '$.header',
          '$.photo',
          '$.title',
          '$.video',
          '$.web-link'
        FROM [default/avatar] 
        WHERE '$.category' = "image-source"
```
{% endtab %}
{% endtabs %}

### Image in jig/default

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/cc-image-jig.png" alt="Image in a jig" width="176"><figcaption><p>Image in a jig</p></figcaption></figure>
{% endcolumn %}

{% column %}
Image as a children component in `default` jig.

**Examples**: See the example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/image/static-data/default-image/default-image.jigx). See the example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/image/dynamic-data/default-image/default-image-dynamic.jigx).

**Datasource**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/story-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/story.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="jig (static)" %}
```yaml
title: Image in jig/default
type: jig.default

children:
  - type: component.image
    options:
      title: Image
      subtitle: in jig/default
      source:
        uri: =@ctx.datasources.story-static[0].image
```
{% endtab %}

{% tab title="jig (dynamic)" %}
```yaml
title: Image in jig/default
type: jig.default

children:
  - type: component.image
    options:
      title: Image
      subtitle: in jig/default
      source:
        uri: =@ctx.datasources.story[2].photo
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  story-static:
    type: datasource.static
    options:
      data:
        - title: Work productivity
          description: How To Be More Productive at Work
          image: https://images.unsplash.com/photo-1456324504439-367cee3b3c32?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          thumbnail: https://images.unsplash.com/photo-1513128034602-7814ccaddd4e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80
          url: https://www.indeed.com/career-advice/career-development/ways-to-be-more-productive
          videoUrl: https://www.youtube.com/watch?v=4aYVLpY5FYU
        - title: Work productivity
          description: Reasons Why You are Not as Productive as You Can Be
          image: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          thumbnail: https://images.unsplash.com/photo-1609659893022-8a02377d8b08?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          url: https://www.lifehack.org/articles/productivity/8-reasons-productive-can-fix.html
          videoUrl: https://www.youtube.com/watch?v=z-7LPjiYBHU
        - title: Work productivity
          description: How to Stay Productive When Working From Home
          image: https://images.unsplash.com/photo-1620862657788-a403bdf6dd63?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1742&q=80
          thumbnail: https://images.unsplash.com/photo-1589591830600-7ba977995a5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          url: https://www.travelers.com/resources/home/working-remotely/10-tips-for-staying-productive-when-working-from-home
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  story:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/avatar
      query: |
        SELECT
          id,
          '$.category',
          '$.description',
          '$.header',
          '$.photo',
          '$.title',
          '$.video',
          '$.web-link'
        FROM [default/avatar] 
        WHERE '$.category' = "image-source"
```
{% endtab %}
{% endtabs %}
