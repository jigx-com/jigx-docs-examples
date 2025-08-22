# carousel

{% columns %}
{% column %}
The carousel is an interactive component that enables you to browse through a set of items visually appealing and intuitively, enhancing the overall experience by making navigation of content engaging and dynamic. The carousel component provides a set of items, such as images, products, or content, that can be browsed by swiping left or right. The carousel showcases multiple items in a horizontal scrolling format with only one item visible at a time. In addition to swipe gestures, navigation identifiers are included in dots or a counter. The dots/counter indicates the current position within the carousel.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-image.gif" alt="" width="166"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Configuration options

Some properties are common to all components, see [Common component properties](carousel.md) for a list and their configuration options.

<table><thead><tr><th width="145.9375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>data</code></td><td>The carousel requires a data source that will be used in the component to return the content, for, example, images or avatars. Any of the can be referenced to return the data.</td></tr><tr><td><code>instanceId</code></td><td>The unique identifier for the carousel.</td></tr><tr><td><code>type</code></td><td>The following components can be added in a carousel: component can be define with <code>title</code> and <code>subtitle</code> that overlays the image. <a href="card.md">card</a> - component allows you to add other components in a card layout in the carousel.</td></tr></tbody></table>

<table><thead><tr><th width="147.49609375">Other options</th><th></th></tr></thead><tbody><tr><td><code>counter</code></td><td>Set to <code>true</code> adds a counter to the top right corner of the carousel in the style similar to 1/4 to indicate the number of images or cards in the carousel. set to <code>false</code> hides the counter. The counter and pagination can be used together or individually, depending on the requirement.</td></tr><tr><td><code>isContained</code></td><td>Set to <code>true</code> places the content (type) in a container which creates a visually appealing frame around the content. Set to <code>false</code> the content fills the entire carousel.</td></tr><tr><td><code>pagination</code></td><td><p>Pagination is shown as dots at the bottom of the carousel. The following options exist:</p><ul><li><code>isContained</code> - created a grey container around the pagination dots improving visibility.</li><li><code>isHidden</code> - <code>false</code> hides the pagination, <code>true</code> shows the pagination.</li><li><code>position</code> - The pagination dots can be places <code>inside</code> or <code>outside</code> the carousel.</li></ul></td></tr></tbody></table>

## Considerations

* Carousel can only be used in a [jig.default](<../Jig Types/jig_default.md>).
* Styling, functionality, events can be configured on the `type` component, for example, `onPress` or `height` settings.
* The carousel uses the same approach as the list component when working with data, making it easy to configure using the `=@ctx.current.item.value` expression.
* Planning the layout of the carousel before you configure the component will save time, and ensure the correct component `type` is used.
* Consider limiting the number of images used for the carousel to have maximum effect.
* The card component is versatile, allowing you to combine multiple components into the carousel. For an example, see the carousel with card containing avatars, expander & location.

## Examples and code snippets

### Image carousel

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-image.gif" alt="Basic carousel" width="166"><figcaption><p>Basic carousel</p></figcaption></figure>
{% endcolumn %}

{% column %}
This examples displays images in the carousel. The `image` component is used with an overlapping `title` and `subtitle`. The `paginatio`n is configured to show `outside` of the carousel. An `onPress` event is added to the image component to open an `info-modal` displaying further information, in this case to book a test-drive.

**Example:** See the example in [GitHub](carousel.md).
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-image.jigx" %}
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
{% endcode %}

### Card carousel

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-card2 (1).gif" alt="Card in a carousel" width="144"><figcaption><p>Card in a carousel</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example the carousel uses a `card` component with a color property, within the card, there is an `image` component used to display the images, an `entity-field` component to describe the product. The card component creates a visually appealing container for the images. The `pagination` is configured `outside` of the carousel.

**Example:**\
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-card.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-card.jigx" %}
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
{% endcode %}

### Carousel contained

{% columns %}
{% column %}
This example uses a static datasource with an image component in the carousel. There are two carousels.

1. The first carousel is configured to `isContained: true` which creates a frame around the image, and rounds the image border. Pagination is also set with `isContained: true` to create a gray frame around the pagination dots.
2. The second carousel is set with `isContained: false` to display the image across the full screen. Pagination is also set to `isContained: false` to show the pagination dots in black.

**Example:**\
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-contained.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-contained.gif" alt="Carousel contained" width="144"><figcaption><p>Carousel contained</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-contained" %}
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
{% endcode %}

### Carousel with pagination (inside & outside)

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-pagination.gif" alt="Pagination" width="142"><figcaption><p>Pagination</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example uses a static datasource and shows how pagination can be placed either inside or outside the carousel. There are two carousels.

1. The first carousel is in a `card` with `color` and configured with `pagination: outside` which places the pagination outside under the carousel.
2. The second carousel is configured in an `image` with `pagination: inside` which overlays the image with the pagination. Pagination is also set to `isContained: true` to enhance the visibility of the pagination dots.

**Example:**\
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-pagination-inside-outside.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-pagination-inside-outside.jigx" %}
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
{% endcode %}

### Carousel with counter

{% columns %}
{% column %}
The carousel in this example uses Dynamic Data and a `counter` in the top right corner instead of pagination. The counter displays the number of items in the carousel and position of the current item. The example uses a `composite` jig to create a master detail jig, allowing you to tap on the image in the carousel and the corresponding detail is shown below.

**Example:**\
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-counter.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-counter.gif" alt="Carousel with counter" width="142"><figcaption><p>Carousel with counter</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="carousel-counter.jigx" %}
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
{% endtab %}

{% tab title="carousel-composite.jigx" %}
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
{% endtab %}

{% tab title="service-details.jigx" %}
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
{% endtab %}
{% endtabs %}

### Carousel with pagination (contained)

{% columns %}
{% column %}
In this example there are two carousels:

1. The first shows the pagination with `isContained: true` with `position: inside` the carousel.
2. The second shows the pagination with `isContained: true` with `position:outside` the carousel.

**Example:**\
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-pagination-contained.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-pag-contained.gif" alt="Carousel - pagination and contained" width="144"><figcaption><p>Pagination &#x26; contained</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-pagination-contained.jigx" %}
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
{% endcode %}

### Carousel with card containing avatars & entity-fields

{% columns %}
{% column %}
The carousel in this example uses Dynamic Data with a colored `card` component. In the card component the `avatar` and `entity-field` components are configured.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/carousel/carousel-card-avatar.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CC-carousel-avatar.gif" alt="Carousel with card " width="142"><figcaption><p>Carousel with card</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% code title="carousel-card-avatar.jigx" %}
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
{% endcode %}
