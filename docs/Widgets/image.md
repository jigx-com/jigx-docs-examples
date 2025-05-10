---
title: image
slug: XtQx-image
description: Learn about the powerful "image" widget in Jig and its various configuration options in this comprehensive document. Discover how to display and style images, preload and cache for offline viewing, add titles and descriptions, and much more. Get inspired 
createdAt: Thu Jun 09 2022 20:14:59 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Mar 10 2025 09:33:23 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
The image widget is set up primarily for displaying an image on the Home Hub or jig.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BNwALszoXt-3CorKq-BBL_img3836.PNG" size="40" position="center" caption="Image widgets with title component" alt="Image widgets with title component"}


:::
::::

::::VerticalSplit{layout}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5UxSksZMj2iwk5GzfoX_G_img3834.PNG" size="44" position="center" caption="Image widgets" alt="Image widgets"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ANtYLUJTB1Wl5FkVYHIrE_img3837.PNG" size="40" position="center" caption alt="Image widgets with title component"}
:::
::::

:::hint{type="info"}
The images can be preloaded and cached using the asset folder's *images* file. The images will be displayed even when you are offline.  For more details, refer to [Assets]().
:::

## Configuration options

| **Core structure** |        |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `source`           |  For the URL of the image. The following can be used: &#xA;- https//: *imagesource*&#xA;- image from a datasource referenced in an expression &#xA;The image source (either a remote URL or a local file resource).This property can contain several remote URLs, specified together with their `width` and `height` and  `scale`.The native side will then choose the best uri to display based on the measured size of the image container. A `cache` property can be added to control how network requests interact with the local cache. Supported formats are png, jpg, jpeg, bmp, gif, webp (Android only), psd (iOS only). |

| **Other options**   |                                                                              |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `bottom`            | The [titles](https://docs.jigx.com/examples/titles) component will be added to the bottom of the widget.                                                                                                                                                 |
| `footer`            | Add text to the footer of the widget.                                      |
| `footerAlign`       | Align the footer text to `left`, `right`, `center`.                         |
| `height`            | Change constraints of an image's height. Use a proper `resizeMode` to achieve the best results in all different device resolutions.                                                     |
| `isContentOverlaid` | Specifiy if the [titles](<./Content widget components/titles.md>) component and description should overlay the image or placed above/ below the image. Use `true` for overlay, `false` for above or below.                                                                               |
| `placeholders`      | Specify a placeholder text to display if there is no data, for example - `title: No data to display`.                                                                                |
| `resizeMode`        | Determines how to resize the image when the frame doesn't match the raw image dimensions. &#xA;- `cover:` Scale the image uniformly (maintain the image's aspect ratio)so that both dimensions (width and height) of the image will be equal to or larger than the corresponding dimension of the view (minus padding).&#xA;- `contain:` Scale the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or less than the corresponding dimension of the view (minus padding).&#xA;- `stretch:` Scale width and height independently, This may change the aspect ratio of the source.&#xA;- `center:` Scale the image down so that it is completely visible, if bigger than the area of the view. The image will not be scaled up. |
| `top`               | The [titles](https://docs.jigx.com/examples/titles) component will be added to the top of the widget.                                                  |

## Examples and code snippets 

:::::ExpandableHeading
### Image widget 2x2

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IvjeY42pnn7Fwh6zp_bzb_wd-image22.PNG" size="80" position="center" caption="Image widget " alt="Image widget 2x2"}
:::

:::VerticalSplitItem
An `image` widget using 2x2 size with `component.titles` at the `bottom`  to add a name of the image and an `icon`.

**Examples**:
See the complete example using in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x2/image-2_2x2.jigx).


:::
::::

:::CodeblockTabs
image-2\_2x2.jigx

```yaml
 widgets:
  image2-2x2:
    type: widget.image
    options:
      source:
        uri: https://images.unsplash.com/photo-1476610182048-b716b8518aae?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2159&q=80      
      isContentOverlaid: false
      bottom: 
        type: component.titles
        options:
          title: Seljalandsfoss
          subtitle: Iceland
          icon: pin
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: image-2_2x2
          widgetId: image2-2x2
```
:::
:::::

:::::ExpandableHeading
### Image widget 2x4

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
An `image` widget using 2x4 size with `component.titles` at the `top`  to add a name `title` and email `subtitle` and an `icon`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x4/image-1_2x4.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qi0EVHoh4A4-Gv7lgFHo__wd-image24.PNG" size="80" position="center" caption="Image widget 2x4" alt="Image widget 2x4"}
:::
::::

:::CodeblockTabs
image-1\_2x4.jigx

```yaml
widgets:
  image1-2x4: 
    type: widget.image
    options:
      source:
        uri: https://images.unsplash.com/photo-1433086966358-54859d0ed716?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80
      isContentOverlaid: true
      top: 
        type: component.titles
        options:
          title: John Donald
          subtitle: john.donald@gmail.com
          icon: phone
          align: center
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: image-1_2x4
          widgetId: image1-2x4
```
:::
:::::

:::::ExpandableHeading
### Image widget 4x2

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/45b1aY0d9UNmxrtFAC8wl_wd-image42.PNG" size="80" position="center" caption="Image widget 4x2" alt="Image widget 4x2"}
:::

:::VerticalSplitItem
An `image` widget using 4x2 size with `component.titles` at the `bottom`  to add a location `title` and an `icon` on the right.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/image-2_4x2.jigx).


:::
::::

:::CodeblockTabs
image-2\_4x2

```yaml
widgets:      
  image2-4x2: 
    type: widget.image
    options:
      source:
        uri: https://images.unsplash.com/photo-1585848705732-e938bf971da6?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1546&q=80  
      isContentOverlaid: false
      bottom: 
        type: component.titles
        options:
          title: Orlicke Hory
          subtitle: Czech Republic
          icon: pin
          align: right
          iconColor: color4
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: image-2_4x2
          widgetId: image2-4x2
```
:::
:::::

:::::ExpandableHeading
### Image widget in group widget 4x2

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/c34eu2ef8d_IEH5l4Ydno_wd-imagegroup.PNG" size="80" position="center" caption="Group image widget 4x2" alt="Group image widget 4x2"}
:::

:::VerticalSplitItem
In this example two `image` widgets are combined into one `group` with the `component.title` at the `bottom` to show the score and team names.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/combined-image-image-1_4x2.jigx).
:::
::::

:::CodeblockTabs
combined-image-image-1\_4x2

```yaml
widgets:
  combined-image1-4x2: 
    type: widget.group
    options:
      children:
        - type: widget.image
          options:
            isContentOverlaid: false
            source:
              uri: https://seeklogo.com/images/O/oakland-athletics-logo-2BAC84D00D-seeklogo.com.png
            resizeMode: contain              
            bottom: 
              type: component.titles
              options:
                title: "3"
                subtitle: "Oakland Invaders"    
                align: center
        - type: widget.image
          options:
            isContentOverlaid: false
            source:
              uri: https://seeklogo.com/images/K/kane-county-cougars-logo-47AAB515C1-seeklogo.com.png
            resizeMode: contain
            bottom: 
              type: component.titles
              options:
                title: "2"
                subtitle: "Kane County Cougars"
                align: center
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: combined-image-image-1_4x2
          widgetId: combined-image1-4x2
```
:::
:::::

:::::ExpandableHeading
### Image widget in group widget 4x4

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The 4x4 `image` widget in this example is a simple widget with just an image shown. This is great when you want to combine the widget in another jig.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/D_FnGdR1a4YduCE4mOwd1_wd-image44.PNG" size="80" position="center" caption="Image widget 4x4" alt="Image widget 4x4"}
:::
::::

:::CodeblockTabs
image-widget 4x4

```yaml
widgets:      
  imageWidget4x4: 
    type: widget.image
    options:
      source:
        uri: https://images.unsplash.com/photo-1603988363607-e1e4a66962c6?q=80&w=1740&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D 
  
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: image-widget 4x4
          widgetId: imageWidget4x4
```
:::
:::::

