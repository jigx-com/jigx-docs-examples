# View (Alpha)

:::hint{type="danger"}
This feature is currently in its **Alpha** stage of development.

- As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
- In this phase, the feature may contain bugs or behave unpredictably.
- Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
- We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.

:::

The `component.view` is an empty container similar to the \<div> element in CSS or HTML.  Use the view component for layouts. The YAML always has the `style:` property under which all style elements such as color and direction for rows and columns are located, and the `children:` property for adding other components such as avatar, text, and icons. Multiple layers of the view component can be used to create UI requirements. You can also place a `component.card` inside the view and vice versa. If you are unfamiliar with CSS or HTML, there are several resources available, such as [https://www.w3schools.com/](https://www.w3schools.com/), that can assist you when configuring a view component.

For steps on creating a custom component, see [How to create a custom component](<./../Custom components _Alpha_.md>).

## Configuration options

You can use `when` and `instanceId` with `component.view`, add the properties before the `options:` property. The available list of style options is shown below.

| **Options**      | **Value**                                       |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `alignContent`   | Determine how content in the view will be aligned, applies to any component contained in the view. The following options are available:&#xA;`center`&#xA;`flex-end`&#xA;`flex-start`&#xA;`space-around`&#xA;`space-between`&#xA;`stretch`   |
| `alignItems`     | Available options include:&#xA;`baseline`&#xA;`center`&#xA;`flex-end`&#xA;`flex-start` &#xA;`stretch`           |
| `alignSelf`      | Available options include:&#xA;`auto`&#xA;`baseline`&#xA;`center`&#xA;`flex-end`&#xA;`flex-start` &#xA;`stretch`      |
| `background`     | `color` - multiple, use IntelliSense to view the available list. See [Jigx color palette](https://docs.jigx.com/jigx-color-palette) to view the different colors.&#xA;`emphasis` - change the brightness and boldness of the content in the view. Available options include:&#xA;- `high` &#xA;- `medium`<br>- `low`<br>- `extra-low`<br>- `low-medium`     |
| `border`         | Configure the border using these properties:&#xA;`bottom`&#xA;`color` - multiple, use IntelliSense to view the available list.&#xA;`emphasis` - `color`, `high`, `medium`, `low`, `extra-low`, `low-medium` &#xA;`end`&#xA;`left`&#xA;`right`&#xA;`start` - `style`&#xA;`style` - `solid`, `transparent`, `true`&#xA;`top`&#xA;`width` - use a number or expression.        |
| `bottom`         | Configure the spacing at the bottom of the view using these properties:&#xA;`large`&#xA;`medium`&#xA;`small`&#xA;`regular`&#xA;`minimal`&#xA;`none`     |
| `emphasis`       | Change the brightness and boldness of the content in the view. Available options include:&#xA;`high`&#xA;`medium`&#xA;`low` &#xA;`extra-low`&#xA;`low-medium`     |
| `flex`           | Available options include:&#xA;`basis`- use a number or expression.&#xA;`direction` - `column`, `column-reverse`, `row`, `row-reverse`&#xA;`grow` - use a number or expression&#xA;`shrink` - use a number or expression&#xA;`wrap` - `wrap`, `nowrap`, `wrap-reverse`&#xA;For more information on using the flex property, see [CSS-Tricks - A complete guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)                                                                                                                                          |
| `gap`&#xA;       | Configure the gap in the view. Available options include:&#xA;`column` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`large`&#xA;`medium`&#xA;`none`&#xA;`minimal`&#xA;`regular`&#xA;`row` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`small`  |
|`hasShadow` | A boolean property used to toggle the display of a shadow beneath the component. When set to `true`, the control renders with a subtle shadow effect, helping it stand out visually against the background. This enhances the visual hierarchy and depth in the mobile app interface. When set to `false` (or omitted), no shadow is applied. |
| `height`         | Determine the height of the view. Available options include:&#xA;`max`&#xA;`min`&#xA;`value`         |
| `justifyContent` | Available options include:&#xA;`center`  &#xA;`flex-end`&#xA;`flex-start`&#xA;`space-around`&#xA;`space-between`&#xA;`space-evenly`   |
| `left`           | Available options include:&#xA;`large`&#xA;`medium`&#xA;`small`&#xA;`regular`&#xA;`minimal`&#xA;`none`        |
| `margin`         | Configure different margins in the view, available options include:&#xA;`bottom` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`end` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`horizontal` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`large`&#xA;`left` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`medium`&#xA;`minimal`&#xA;`none`&#xA;`regular`&#xA;`right` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`small`&#xA;`start` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`top` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`vertical` - `large`, `medium`, `small`, `regular`, `minimal`, `none`   |
| `overflow`       | Available options include:&#xA;`hidden`&#xA;`scroll`&#xA;`visible`    |
| `padding`        | Configure different paddings in the view, available options include:&#xA;`bottom` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`end` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`horizontal` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`large`&#xA;`left` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`medium`&#xA;`minimal`&#xA;`none`&#xA;`regular`&#xA;`right` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`small`&#xA;`start` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`top` - `large`, `medium`, `small`, `regular`, `minimal`, `none`&#xA;`vertical` -  `large`, `medium`, `small`, `regular`, `minimal`, `none` |
| `position`       | Available options include:&#xA;`absolute`&#xA;`relative`       |
| `radius`         | Available options include:&#xA;`large`&#xA;`medium`&#xA;`regular`&#xA;`small`&#xA;`tiny`&#xA;`bottomLeft` - `large`, `medium`, `regular`, `small`, `tiny`&#xA;`bottomrRight` - `large`, `medium`, `regular`, `small`, `tiny`&#xA;`topRight` - `large`, `medium`, `regular`, `small`, `tiny`&#xA;`topLeft` - `large`, `medium`, `regular`, `small`, `tiny`                  |
| `right`          | Available options include:&#xA;`large`&#xA;`medium`&#xA;`small`&#xA;`regular`&#xA;`minimal`&#xA;`none`                             |
| `top`            | Available options include:&#xA;`large`&#xA;`medium`&#xA;`small`&#xA;`regular`&#xA;`minimal`&#xA;`none`                               |
| `width`          | Available options include:&#xA;`max`&#xA;`min`&#xA;`value`      |

## Considerations

- When using the `component.image` on custom components, the `isFlexible` property is available. If the property is set to `true`, the image will take the parent's space. If the parent has zero height or zero width, the image will not render. Set the `height` and `width` on the image, or set `isFlexible` to `true`.
- When using the `component.image` in the `component.view` to define the `height`, e.g., 100, and setting `isFlexible: true` for each image. This allows the images to grow into the parent component space.
- In styles, you cannot use `flexGrow` and `width` together. Use one or the other; if combined, the width property does not function, and the UI element will not render as designed.
- By default, `children` components are stacked in a column.
- To ensure that `text` and `icons` do not run over borders in the app, use `flex:grow:1` and `shrink:1` together.

## Example and code samples

:::ExpandableHeading

### Itinerary using views to create columns and rows

:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows using the `component.view` to create the layout for an itinerary. The `view` component creates a wrapper for the content,  rows to show content in, and columns to create spacing between the content. The `component.text` is used inside the view component to show the content and the `component.image` shows the required images.

Examples:

1. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/templates/itinerary/itinerary.jigx).
2. See the custom component in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/templates/itinerary/itinerary-day.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SZ4HP02vO6iboL96ULZoc-20241121-141538.png" size="70" position="center" caption="Itinerary view" alt="Itinerary view" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SZ4HP02vO6iboL96ULZoc-20241121-141538.png"}
:::
::::

:::CodeblockTabs
itinerary-day.jigx

```yaml
type: component.default
children:
  # WRAPPER - use the view component as a container for other components
  - type: component.view
    options:
      style:
        flex:
          direction: row  
          grow: 1
        padding: 
          horizontal: medium
          bottom: medium
        gap: medium
        justifyContent: flex-start
        alignItems: flex-start
      children:
        # TIME - use a view component to create the layout for a time column
        - type: component.view
          options:
            style:
              flex:
                direction: column
              emphasis: medium
              width: 50
            children:
              - type: component.text
                options:
                  value: =@ctx.inputs.time
                  align: left
        # CONTENT - use the view component to design the layout of content such as text in rows, and spaces between text
        - type: component.view
          options:
            style:
              flex:
                direction: column
                grow: 1
                shrink: 1
              gap: small
              border:
                bottom:
                  style: solid
                  emphasis: extra-low
              padding: 
                bottom: medium
                  
            children:
              - type: component.view
                options:
                  style:
                    flex: 
                      direction: row
                    justifyContent: flex-start
                    alignItems: center
                    gap: small
                  children:
                    - type: component.text
                      when: =@ctx.inputs.title
                      options:
                        value: =@ctx.inputs.title
                        align: left
                        weight: bold
                    - type: component.view
                      when: =@ctx.inputs.extra = true ? true:false
                      options:
                        style:
                          background:
                            color: color3
                          padding: 
                            vertical: minimal
                            horizontal: small
                          radius: tiny
                          flex: 
                            grow: 0
                          alignSelf: flex-start
                        children:
                        - type: component.text
                          options:
                            value: Extra
                            size: small
                                    
              - type: component.text
                when: =@ctx.inputs.duration != null ? true :false
                options:
                  value: =@ctx.inputs.duration
                  align: left
                  emphasis: medium
                  size: small
              - type: component.text
                when: =@ctx.inputs.description != null ? true :false
                options:
                  value: =@ctx.inputs.description
                  align: left
                  emphasis: medium
                  size: small
              - type: component.view
                when: =@ctx.inputs.image1 != null ? true :false
                options:
                  style: 
                    flex: 
                      direction: row
                    gap: small
                    height: 100
                  children:
                    - type: component.image
                      options:
                        source:
                          uri: =@ctx.inputs.image1
                        isFlexible: true
                    - type: component.image
                      options:
                        source:
                          uri: =@ctx.inputs.image2
                        isFlexible: true
                    - type: component.image
                      options:
                        source:
                          uri: =@ctx.inputs.image3
                        isFlexible: true                                          
```

itinerary.jigx

```yaml
title: Itinerary
type: jig.default

datasources:
  itinerary-day: 
    # Use static data to populate the itinerary 
    type: datasource.static
    options:
      data:
        - id: 1
          day: 1
          time: 09:00
          title: Morning Hike
          duration: 3 hours 30 mins
          description: Start your day with a refreshing morning hike through a nearby nature trail. Enjoy the scenic beauty and invigorating exercise as you explore the lush greenery and perhaps spot some wildlife.
        - id: 2
          day: 1
          time: 13:00
          title: Cooking Class
          duration: 1 hours 30 mins
          description: Enhance your culinary skills with an optional cooking class. Learn to prepare local delicacies under the guidance of expert chefs. This class offers hands-on experience and the opportunity to savor your delicious creations afterward.
          image1: https://images.unsplash.com/photo-1507048331197-7d4ac70811cf?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y29va2luZyUyMGNsYXNzfGVufDB8fDB8fHww&auto=format&fit=crop&w=900&q=60
          extra: true
        - id: 3
          day: 1
          time: 16:00
          title: City Tour
        - id: 4
          day: 1
          time: 18:00
          title: Sunset Cruise
          duration:
          description: Relax and unwind on a scenic sunset cruise. Set sail on tranquil waters, admire the picturesque views, and witness the breathtaking colors of the setting sun. This leisurely experience offers a perfect end to your day.
          image1: https://images.unsplash.com/photo-1642195349088-953f63a7d4df?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHN1bnNldCUyMGNydWlzZXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=900&q=60
          image2: https://images.unsplash.com/photo-1580541631950-7282082b53ce?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3J1aXNlfGVufDB8fDB8fHww&auto=format&fit=crop&w=900&q=60
        - id: 5
          day: 2
          time: 09:00
          title: Contemporary Art Museum Visit
          duration: 3 hours
          description:
          image1: https://images.unsplash.com/photo-1534235826754-0a3572d1d6d5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTF8fG11c2V1bXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=900&q=60
        - id: 6
          day: 2
          time: 13:00
          title: Guided Wine Tasting
          duration:
          description: Indulge in a guided wine tasting experience at a local vineyard. Discover the flavors and aromas of exquisite wines as you learn about the winemaking process. Expand your knowledge of different varieties and enjoy the sophistication of this activity (additional fee applies).
          image1: https://images.unsplash.com/photo-1568213816046-0ee1c42bd559?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8d2luZSUyMHRhc3Rpbmd8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=900&q=60
          image2: https://images.unsplash.com/photo-1513618827672-0d7c5ad591b1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTh8fHdpbmUlMjB0YXN0aW5nfGVufDB8fDB8fHww&auto=format&fit=crop&w=900&q=60
          image3: https://images.unsplash.com/photo-1598306442928-4d90f32c6866?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OXx8d2luZSUyMHRhc3Rpbmd8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=900&q=60
        - id: 7
          day: 2
          time: 15:00
          title:  Outdoor Adventure
          duration: 2 hours
          description: Get your adrenaline pumping with an outdoor adventure activity such as zip-lining, rock climbing, or kayaking. Challenge yourself, enjoy the thrill, and soak up the natural surroundings. This exciting experience will leave you with unforgettable memories.
        - id: 8
          day: 2
          time: 18:00
          title: Dinner and Live Music
          extra: true
            
children:
  # ITINERARY - use the view custom component in a jig        
  - type: component.custom-component      
    componentId: section2
    inputs:
      title: Day 1

  - type: component.list
    options:
      data: =@ctx.datasources.itinerary-day[day=1]
      maximumItemsToRender: 8
      item: 
        type: component.custom-component
        componentId: view-itinerary
        inputs:
          time: =@ctx.current.item.time 
          title: =@ctx.current.item.title
          duration: =@ctx.current.item.duration
          description: =@ctx.current.item.description
          image1: =@ctx.current.item.image1
          image2: =@ctx.current.item.image2
          extra: =@ctx.current.item.extra
                
  - type: component.custom-component      
    componentId: section2
    inputs:
      title: Day 2
  
  - type: component.list
    options:
      data: =@ctx.datasources.itinerary-day[day=2]
      maximumItemsToRender: 8
      item: 
        type: component.custom-component
        componentId: view-itinerary
        inputs:
          time: =@ctx.current.item.time 
          title: =@ctx.current.item.title
          duration: =@ctx.current.item.duration
          description: =@ctx.current.item.description
          image1: =@ctx.current.item.image1
          image2: =@ctx.current.item.image2
          image3: =@ctx.current.item.image3
          extra: =@ctx.current.item.extra     
```

:::

:::ExpandableHeading

### Other view layout examples

Explore a variety of additional code examples demonstrating the use of the `view` component on GitHub. These examples showcase different configurations and use cases to help you achieve  different layouts.

- [Layouts 1 - 10](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/basic-elements/layout)

:::
