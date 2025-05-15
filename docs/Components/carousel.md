# carousel

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The carousel is an interactive component that enables you to browse through a set of items visually appealing and intuitively, enhancing the overall experience by making navigation of content engaging and dynamic. The carousel component provides a set of items, such as images, products, or content, that can be browsed by swiping left or right. The carousel showcases multiple items in a horizontal scrolling format with only one item visible at a time. In addition to swipe gestures, navigation identifiers are included in dots or a counter. The dots/counter indicates the current position within the carousel.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pLg81p_Qw_0sw3Cpl7fOT_cc-carousel-image.gif" size="68" position="center" caption="Carousel" alt="Carousel" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pLg81p_Qw_0sw3Cpl7fOT_cc-carousel-image.gif"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`             | The carousel requires a data source that will be used in the component to return the content, for, example, images or avatars. Any of the [Data Providers](<./../Data Providers.md>) can be referenced to return the data.                                       |
| `instanceId`       | The unique identifier for the carousel.                                                                                                                                                                                                                          |
| `type`             | The following components can be added in a carousel:&#xA;[image](./image.md) component can be define with `title` and `subtitle` that overlays the image.&#xA;[card](./card.md) - component allows you to add other components in a card layout in the carousel. |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `counter`         | Set to `true` addes a counter to the top right corner of the carousel in the style similiar to 1/4 to indicate the number of images or cards in the carousel. set to `false` hides the counter. The counter and pagination can be used together or individually depending on the requirement.                                                               |
| `isContained`     | Set to `true` places the content (type) in a container which creates a visually appealing frame around the content. Set to `false` the content fills the entire carousel.                                                                                                                                                                                   |
| `pagination`      | Pagination is shown as dots at the bottom of the carousel. The following options exist:&#xA;`isContained` - created a grey container around the pagination dots improving visibility.<br />`isHidden` - `false` hides the pagination, `true` shows the pagination.<br />`position` - The pagination dots can be places `inside` or `outside` the carousel.  |

## Considerations

- Carousel can only be used in a [jig.default](<./../Jig Types/jig_default.md>).
- Styling, functionality, events can be configured on the `type` component, for example, `onPress` or `height` settings.
- The carousel uses the same approach as the list component when working with data, making it easy to configure using the `=@ctx.current.item.value` expression.
- Planning the layout of the carousel before you configure the component will save time, and ensure the correct component `type` is used.
- Consider limiting the number of images used for the carousel to have maximum effect.
- The card component is versatile, allowing you to combine multiple components into the carousel. For an example, see the [carousel with card containing avatars, expander & location](#). 

## Examples and code snippets

:::::ExpandableHeading
### Image carousel

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/j-Pmuzvmaecc7tfl8Yz8q_cc-carousel-image.gif" size="80" position="center" caption="Carousel with image" alt="Carousel with image" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/j-Pmuzvmaecc7tfl8Yz8q_cc-carousel-image.gif"}
:::

:::VerticalSplitItem
This examples displays images in the carousel. The `image` component is used with an overlapping `title` and `subtitle`. The `paginatio`n is configured to show `outside` of the carousel. An `onPress` event is added to the image component to open an `info-modal` displaying further information, in this case to book a test-drive.

**Example:**
See the example in [GitHub]("https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-image.jigx).
:::
::::

:::CodeblockTabs
carousel-image.jigx

```yaml
title: Carousel with image
type: jig.default

datasources:
  models:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Model A
          price: $ 48000  
          image: https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?q=80&w=2566&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 2
          name: Model B
          price: $ 30000  
          image: https://images.unsplash.com/photo-1555353540-64580b51c258?q=80&w=2556&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 3
          name: Model c
          price: $ 27000   
          image: https://images.unsplash.com/photo-1502877338535-766e1452684a?q=80&w=2672&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 4
          name: Model D
          price: $ 15000  
          image: https://images.unsplash.com/photo-1522932467653-e48f79727abf?q=80&w=2630&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D    

children:
  - type: component.carousel
    
    options:
      
      data: =@ctx.datasources.models
      item: 
        type: component.card
        options:
          children:
            - type: component.image
              options:
                title: New Models
                subtitle: Power and luxury
                onPress: 
                  type: action.info-modal
                  options:
                    modal:
                      title: Today's luxury 
                      buttonText: Book a test drive
                      element: 
                        type: image
                        uri: =@ctx.current.item.image
                  
                source:
                  uri: =@ctx.current.item.image
      isContained: true
      pagination:
        isContained: false
        isHidden: false
        position: outside
      counter:
        isHidden: true

  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Welcome to carX
            children:
              - type: component.entity-field
                options:
                  label: ''
                  value:
                   At Premier Auto Sales, we pride ourselves on delivering an exceptional car-buying experience tailored to meet the diverse needs of our valued customers. With a vast selection of the latest models from top manufacturers, alongside a curated collection of certified pre-owned vehicles, we ensure that you find the perfect car to match your lifestyle and budget.
                  isMultiline: true
        - type: component.entity-field
          options:
            label: Visit our showroom
            value: 24 Main road, Houston, Texaz
        - type: component.entity-field
          options:
            label: Call us today!
            value: 10-234-5556
```
:::
:::::

:::::ExpandableHeading
### Card carousel

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1EXfr7epzL-6O3iIBpG-C_cc-carousel-card2.gif" size="80" position="center" caption="Carousel with card" alt="Carousel with card" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1EXfr7epzL-6O3iIBpG-C_cc-carousel-card2.gif"}
:::

:::VerticalSplitItem
In this example the carousel uses a `card` component with a color property, within the card, there is an `image` component used to display the images, an `entity-field` component to describe the product. The card component creates a visually appealing container for the images.  The `pagination` is configured `outside` of the carousel.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-card.jigx).
:::
::::

:::CodeblockTabs
carousel-card.jigx

```yaml
title: Carousel with card
type: jig.default

children:
  - type: component.carousel
    options:
      data: =@ctx.datasources.products-dynamic
      item: 
        type: component.card
        options:
          children:
            - type: component.image
              options:
                source:
                  uri: =@ctx.current.item.uri
            - type: component.entity
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Product
                      value: =@ctx.current.item.title 
          color: color1
      isContained: true
      pagination:
        isContained: false
        isHidden: false
        position: outside
      counter:
        isHidden: true
```
:::
:::::

:::::ExpandableHeading
### Carousel contained

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example uses a static datasource with an image component in the carousel. There are two carousels.

1. The first carousel is configured to `isContained: true` which creates a frame around the image, and rounds the image border. Pagination is also set with `isContained: true` to create a gray frame around the pagination dots.
2. The second carousel is set with `isContained: false` to display the image across the full screen. Pagination is also set to `isContained: false` to show the pagination dots in black.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-contained.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9gbNHXGLefsRDubTljt7l_cc-carousel-contained.gif" size="80" position="center" caption="Carousel contained" alt="Carousel contained" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9gbNHXGLefsRDubTljt7l_cc-carousel-contained.gif"}
:::
::::

:::CodeblockTabs
carousel-contained

```yaml

title: Carousel contained
type: jig.default

datasources:
  products:
    type: datasource.static
    options:
      data:
        - id: 1
          image: https://images.unsplash.com/photo-1523275335684-37898b6baf30?q=80&w=2599&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 2
          image: https://plus.unsplash.com/premium_photo-1676717962720-d9a812c8f8c9?q=80&w=2748&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 3
          image: https://images.unsplash.com/photo-1568386453619-84c3ff4b43c5?q=80&w=2728&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 4
          image: https://images.unsplash.com/photo-1479064555552-3ef4979f8908?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 5
          image: https://images.unsplash.com/photo-1492707892479-7bc8d5a4ee93?q=80&w=2193&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 6
          image: https://images.unsplash.com/photo-1593998066526-65fcab3021a2?q=80&w=2669&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.section
    options:
      title: Carousel contained & pagination contained
      children:
        - type: component.carousel
          options:
            isContained: true
            pagination: 
              isContained: true
              position: outside
              
            data: =@ctx.datasources.products
            item:
              type: component.image
              options:
                source:
                  uri: =@ctx.current.item.image
  - type: component.section
    options:
      title: Carousel not contained & pagination not contained
      children:
        - type: component.carousel
          options:
            isContained: false
            pagination: 
              isContained: false
              position: outside  
            data: =@ctx.datasources.products
            item:
              type: component.image
              options:
                source:
                  uri: =@ctx.current.item.image
```
:::
:::::

:::::ExpandableHeading
### Carousel with pagination (inside & outside)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lZduG0Ik22bypmuuyutye_cc-carousel-pagination.gif" size="80" position="center" caption="Carousel with pagination" alt="Carousel with pagination" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lZduG0Ik22bypmuuyutye_cc-carousel-pagination.gif"}
:::

:::VerticalSplitItem
This example uses a static datasource and shows how pagination can be placed either inside or outside the carousel. There are two carousels.

1. The first carousel is in a `card` with `color` and configured with `pagination: outside` which places the pagination outside under the carousel.
2. The second carousel is configured in an `image` with `pagination: inside` which overlays the image with the pagination. Pagination is also set to `isContained: true` to enhance the  visibility of the pagination dots.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-pagination-inside-outside.jigx).
:::
::::

:::CodeblockTabs
carousel-pagination-inside-outside.jigx

```yaml
title: Carousel with pagination
type: jig.default

datasources:
  products:
    type: datasource.static
    options:
      data:
        - id: 1
          image: https://images.unsplash.com/photo-1523275335684-37898b6baf30?q=80&w=2599&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 2
          image: https://plus.unsplash.com/premium_photo-1676717962720-d9a812c8f8c9?q=80&w=2748&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 3
          image: https://images.unsplash.com/photo-1568386453619-84c3ff4b43c5?q=80&w=2728&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 4
          image: https://images.unsplash.com/photo-1479064555552-3ef4979f8908?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 5
          image: https://images.unsplash.com/photo-1492707892479-7bc8d5a4ee93?q=80&w=2193&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 6
          image: https://images.unsplash.com/photo-1593998066526-65fcab3021a2?q=80&w=2669&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.section
    options:
      title: Carousel with card & pagination (outside)
      children:
        - type: component.carousel
          options:
            data: =@ctx.datasources.products
            item: 
              type: component.card
              options:
                children:
                  - type: component.image
                    options:
                      source:
                        uri: =@ctx.current.item.image
                color: color2
            pagination:
              position: outside
              isContained: false
        
  - type: component.section
    options:
      title: Carousel with image & pagination (inside)
      children:
        - type: component.carousel
          options:
            data: =@ctx.datasources.products
            item: 
              type: component.image
              options:
                source:
                  uri: =@ctx.current.item.image
            pagination:
              position: inside
              isContained: true
```
:::
:::::

:::::ExpandableHeading
### Carousel with counter

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The carousel in this example uses Dynamic Data and a `counter` in the top right corner instead of pagination. The counter displays the number of items in the carousel and position of the current item.
The example uses a `composite` jig to create a master detail jig, allowing you to tap on the image in the carousel and the corresponding detail is shown below.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-counter.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ypD9O_llX4-cvZGwXkM1L_cc-carousel-counter.gif" size="80" position="center" caption="Carousel with counter" alt="Carousel with counter" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ypD9O_llX4-cvZGwXkM1L_cc-carousel-counter.gif"}
:::
::::

:::CodeblockTabs
carousel-counter.jigx

```yaml
title: Carousel with counter
type: jig.default

outputs:
  output-key: =@ctx.solution.state.servicesId
    
children:
  - type: component.carousel
    options:  
      data: =@ctx.datasources.cleaning-services-dynamic
      item: 
        type: component.image
        options:
          source:
            uri: =@ctx.current.item.image
          title: =@ctx.current.item.service
          onPress: 
            type: action.set-state
            options:
              state: =@ctx.solution.state.servicesId
              value: =@ctx.current.item.id
      isContained: true
      pagination:
        isHidden: true
      counter:
        isHidden: false
        
```

carousel-composite.jigx

```yaml
type: jig.composite
title: Cleaning Services

children:
  - jigId: carousel-counter
  - jigId: service-details
    instanceId: service_deets
    inputs:
      id: =@ctx.solution.state.servicesId
```

service-details.jigx

```yaml
title: =@ctx.datasources.cleaningServices.service != null ? "Service details":" "
type: jig.default
placeholders:
  - title: Please choose a service
    when: =@ctx.datasources.cleaningServices.service != null ? false:true
    icon: loading-data
      

datasources:
  cleaningServices:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - entity: default/cleaning-services
      queryParameters:
        servId: =@ctx.solution.state.servicesId
  
      query: | 
        SELECT 
          id,
          '$.area', 
          '$.description',
          '$.hourlyrate',
          '$.illustratuion',
          '$.image',
          '$.indoor',
          '$.onceoffrate',
          '$.service',
          '$.time' 
        FROM [default/cleaning-services] WHERE id = @servId

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: =@ctx.datasources.cleaningServices.image

children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaningServices.service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaningServices.area
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaningServices.time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaningServices.indoor
                  contentType: checkbox
        - type: component.entity-field
          options:
            label: Description
            value: =@ctx.datasources.cleaningServices.description
            isMultiline: true
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =(@ctx.datasources.cleaningServices.hourlyrate) != 'NA' ? '$ ' & $number(@ctx.datasources.cleaningServices.hourlyrate):'NA'
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: ='$ ' & $number(@ctx.datasources.cleaningServices.onceoffrate)
                  isHidden: =(@ctx.datasources.cleaningServices.onceoffrate) = null ? true:false
```
:::
:::::

:::::ExpandableHeading
### Carousel with pagination (contained)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example there are two carousels:

1. The first shows the pagination with `isContained: true` with `position: inside` the carousel.
2. The second shows the pagination with `isContained: true` with `position:outside` the carousel.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-pagination-contained.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/sj8QxKZPoS3jYJdhiCvS7_cc-carousel-pag-contained.gif" size="80" position="center" caption="Carousel with contained pagination" alt="Carousel with contained pagination" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/sj8QxKZPoS3jYJdhiCvS7_cc-carousel-pag-contained.gif"}
:::
::::

:::CodeblockTabs
carousel-pagination-contained.jigx

```yaml
title: Carousel with pagination (contained)
type: jig.default

datasources:
  models:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Model A
          price: $ 48000  
          image: https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?q=80&w=2566&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 2
          name: Model B
          price: $ 30000  
          image: https://images.unsplash.com/photo-1555353540-64580b51c258?q=80&w=2556&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 3
          name: Model c
          price: $ 27000   
          image: https://images.unsplash.com/photo-1502877338535-766e1452684a?q=80&w=2672&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - id: 4
          name: Model D
          price: $ 15000  
          image: https://images.unsplash.com/photo-1522932467653-e48f79727abf?q=80&w=2630&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D    

children:
  - type: component.section
    options:
      title: Carousel with pagination contained (inside)
      children:
        - type: component.carousel
          options:
            data: =@ctx.datasources.models
            item: 
              type: component.image
              options:
                title: New Models
                subtitle: Power and luxury   
                source:
                  uri: =@ctx.current.item.image
            isContained: false
            pagination:
              isContained: true
              isHidden: false
              position: inside
                  
  - type: component.section
    options:
      title: Carousel with pagination contained (outside)
      children:
       - type: component.carousel
         options:
           data: =@ctx.datasources.models
           item: 
             type: component.card
             options:
               children:
                - type: component.image
                  options:
                    title: New Models
                    subtitle: Power and luxury 
                    source:
                      uri: =@ctx.current.item.image     
           pagination:
                isContained: true
                isHidden: false
                position: outside    
```
:::
:::::

### Carousel with card containing avatars & entity-fields

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The carousel in this example uses Dynamic Data with a colored `card` component. In the card component the  `avatar` and `entity-field` components are configured.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-card-avatar.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/X_GIlacEm0Nc0eLOwKiTt_cc-carousel-avatar.gif" size="80" position="center" caption="Carousel with avatar" alt="Carousel with avatar" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/X_GIlacEm0Nc0eLOwKiTt_cc-carousel-avatar.gif"}
:::
::::

:::CodeblockTabs
carousel-card-avatar.jigx

```yaml
title: Carousel with avatars
type: jig.default

children:
  - type: component.carousel
    options:
      data: =@ctx.datasources.users
      item: 
        type: component.card
        options:
          children:
            - type: component.avatar
              options:
                title: =@ctx.current.item.name
                uri: =@ctx.current.item.uri
                size: large
                align: center
            - type: component.entity
              options:
                children:
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Name
                            value: =@ctx.current.item.name
                        - type: component.entity-field
                          options:
                            label: Position
                            value: =@ctx.current.item.position
                        - type: component.entity-field
                          options:
                            label: Status
                            value: =@ctx.current.item.status                       
          color: color3
      isContained: true
      pagination:
        position: outside
        isContained: true

```
:::

