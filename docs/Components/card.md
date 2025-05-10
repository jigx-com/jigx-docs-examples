---
title: card
slug: JFrM-ca
createdAt: Thu Jun 06 2024 13:21:20 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Mar 04 2025 06:43:54 GMT+0000 (Coordinated Universal Time)
---

The card is a versatile and visually appealing UI element that encapsulates and presents information or interactive content in a structured, consistent, and user-friendly manner. It enhances the app's usability by organizing content into manageable, self-contained units that are easy to navigate and interact with. Each card typically includes a mix of text, images, and interactive elements, creating a self-contained unit of content.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LFWTucW7Hd-Gh2mU4HA29_cc-card-overview.png" size="80" position="center" caption="Cards" alt="Cards"}

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |          |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| `children`         | Configure a component or multiple components in a card. See [Components](./../Components.md) for a list of available components.  |
| `instanceId`       | Give the card component a unique id that can be referenced throughout the jig.                                                    |

| **Other options** |                                                                                                                                                            |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`           | Sets the color of the card. Choose a color from the provided [Jigx color palette](). Default color is white if the property is not specified in the YAML.  |
| `style`           | When `isDisabled` is set to `true`, the card appears opaque, indicating that it is unavailable for selection. By default `isDisabled` is set to `false`.   |

| ### Actions |                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------- |
| `onPress`   | Choose from the provided list of available actions, for example, use the `go-to` action to open a different jig. |

## Considerations

- *Jig-level:* The card component is only available for use in a [default](<./../Jig Types/jig_default.md>) jig.
- *Component-level: *The [carousel](./carousel.md) component has the option to use the card component within the carousel to create a visually appealing carousel.

## Examples and code snippets

:::::ExpandableHeading
### Card containing a form

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/AGHA6ALv3_4Jlm-EYHqE4_cc-card.PNG" size="80" position="center" caption="Card containing a form" alt="Card containing a form"}
:::

:::VerticalSplitItem
In this example the card component wraps the form component to create a visual container around the form.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/card/card-basic.jigx).
:::
::::

:::CodeblockTabs
card-basic.jigx

```yaml

title: Form in a card
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1682685797736-dabb341dc7de?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.hikerInfo-dd.state.data
    
children:
  - type: component.card
    options:
      children:
        - type: component.form
          instanceId: hikerInfo-dd
          options:
            isDiscardChangesAlertEnabled: false
            children:
              - type: component.text-field
                instanceId: name
                options:
                  label: Hiker's name
              - type: component.text-field
                instanceId: contact
                options:
                  label: Mobile number
              - type: component.media-field
                instanceId: photo
                options:
                  imageQuality: 80
                  imageCropping: 
                    width: 64
                    height: 64
                  label: Profile photo
                  mediaType: image

actions:
  - children:
       - type: action.execute-entity
         options:
          title: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/hikers
          method: create
          data:
            name: =@ctx.components.name.state.value
            contact: =@ctx.components.contact.state.value
            photo: =@ctx.components.photo.state.value
          onSuccess: 
            type: action.go-back                                   
```
:::
:::::

:::::ExpandableHeading
### Card in a carousel

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1EXfr7epzL-6O3iIBpG-C_cc-carousel-card2.gif" size="80" position="center" caption="Carousel with card" alt="Carousel with card"}
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
### Cards with color

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows three cards.

1. The first card contains the `avatar`, `expander`, `entity-field` and `location` components with the` color: color3` property.
2. The second card contains a `line-chart` component with the `color: color14` property set.
3. The third card contains an `image` and `entity-field` components with the `color: color6` property set.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/card/card-color.jigx).
:::

:::VerticalSplitItem
![Cards with color](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BnatBgEmVsruHZlnCqBlK_cc-card-color.PNG "Cards with color")
:::
::::

:::CodeblockTabs
card-color.jigx

```yaml
title: Cards with color
description: Card with color and multiple components
type: jig.default  

children:
  - type: component.card
    options:
      children:
        - type: component.avatar
          options:
            title: Customer
            uri: =@ctx.datasources.users[3].uri
            size: large
            align: center
        - type: component.expander
          options:
            header:
              centerElement: 
                type: component.titles
                options:
                  title: =@ctx.datasources.users[3].name
                  subtitle: =@ctx.datasources.users[3].position
            isInitiallyCollapsed: true
            onContentPress: 
              type: action.go-back
        
            children:
                  - type: component.location
                    options:
                      viewPoint:
                        centerPosition: middle
                        address: =@ctx.datasources.users[3].address
                        zoomLevel: 10                         
      color: color3
  - type: component.card
    options:
      children: 
      - type: component.line-chart
        options:
          chart:
            height: 150
            isAnimated: true
          yAxis:
            min: 0
            labels:
              format:
                numberStyle: currency
                compactDisplay: short
                notation: compact
            tickAmount: 8
            isFirstTickHidden: true
            isFirstLabelHidden: true
          xAxis:
            categories:
              - Q1
              - Q2
              - Q3
              - Q4
          series:
            - data: =[{"x":"Q1/19", "y":25000, "color":"color2"}, {"x":"Q2/19", "y":32000, "color":"color2"}, {"x":"Q3/19", "y":45000, "color":"color2"}, {"x":"Q4/19", "y":86000, "color":"color2"}]
              name: Year 2019
              animation:
                  direction: left-to-right
              layout: area-gradient
              dataLabels:
                - isEnabled: true
            - data: =[{"x":"Q1/20", "y":12000, "color":"color3"}, {"x":"Q2/20", "y":48000, "color":"color3"}, {"x":"Q3/20", "y":36000, "color":"color3"}, {"x":"Q4/20", "y":120000, "color":"color3"}]
              name: Year 2020
              animation:
                  direction: left-to-right
              layout: area-gradient
              dataLabels:
                - isEnabled: true      
          legend:
            isHidden: false
      color: color14
      
  - type: component.card
    options:
      children:
        - type: component.image
          options:
            height: 150
            source:
              uri: https://images.unsplash.com/photo-1504389557830-b293439b92d0?q=80&w=2580&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - type: component.entity
          options:
            children:
              - type: component.entity-field
                options:
                  label: Location
                  value: Cliff Edge lighthouse
      color: color6
  
```

users.jigx (datasource)

```yaml
type: datasource.static
options:
  data:
    - name: Boris Miranda
      position: UX Designer
      uri: https://randomuser.me/api/portraits/men/32.jpg
      uri-text: BM
      status: Accepted
      address: 204 Governor Printz Blvd, Claymont, DE 19703, United States
      
    - name: Santiago Hampton
      position: Senior Frontend Developer
      uri: https://randomuser.me/api/portraits/men/46.jpg
      uri-text: SH
      status: Accepted
      address: 1035 Cambridge St, Cambridge, MA 02141
        
    - name: Tom Sellers
      position: QA Engineer
      uri: https://randomuser.me/api/portraits/men/97.jpg
      uri-text: TS
      status: Declined
      address: 141 Harbor Dr Claymont, Delaware(DE), 19703
        
    - name: Anne Dopp
      position: HR Administrator
      uri: https://randomuser.me/api/portraits/women/79.jpg
      uri-text: AD
      status: Accepted
      address: 8400 Governor Printz Blvd, Claymont, DE 19703, United States
        
    - name: Zuzana Moudra
      position: HR Business Partner
      uri: https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-0.3.5&q=80&fm=jpg&crop=faces&fit=crop&h=200&w=200&s=046c29138c1335ef8edee7daf521ba50
      uri-text: ZM
      status: Accepted
      address: 800 Skipjack Ln, Claymont, DE 19703, United States
      
    - name: Jane Stevens 
      position: HR Generalist
      uri: https://images.unsplash.com/photo-1520813792240-56fc4a3765a7?ixlib=rb-1.2.1&q=80&fm=jpg&crop=faces&fit=crop&h=200&w=200&ixid=eyJhcHBfaWQiOjE3Nzg0fQ
      uri-text: JS
      status: Declined
      address: 399-301 Chapel Ave, Claymont, DE 19703, USA
            
```
:::
:::::

:::::ExpandableHeading
### Card with style

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/St6oYKOw2poUb2nO16RLi_cc-card-disabled.PNG" size="80" position="center" caption="Card with style" alt="Card with style"}
:::

:::VerticalSplitItem
This jig contains two cards, the first appears disabled using the `isDisabled: true` property and the second card the `isDisabled` property is set to `false`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/card/card-style.jigx).
:::
::::

:::CodeblockTabs
card-style.jigx

```yaml
title: card style - disabled
type: jig.default

children:
  - type: component.section
    options:
      title: Card with style disabled
      children:
        - type: component.card
          instanceId: card-style
          options:
            color: color10
            style:
              isDisabled: true
            onPress: 
              type: action.go-back
            children:
              - type: component.image
                options:
                  source:
                    uri: https://images.unsplash.com/photo-1612539465222-c20af6006413?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

  - type: component.section
    options:
      title: Card with style enabled
      children:
        - type: component.card
          instanceId: card-enabled
          options:
            color: color10
            style:
              isDisabled: false
            onPress: 
              type: action.go-back
            children:
              - type: component.image
                options:
                  source:
                    uri: https://images.unsplash.com/photo-1612539465222-c20af6006413?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
                
```
:::
:::::

:::::ExpandableHeading
### Card with onPress

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
The card component can be configured with an `onPress` event. In this example when the card is pressed a `go-to` component is configured to take you to the product list jig with items on sale.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/card/card-onPress.jigx).
:::

:::VerticalSplitItem
![Card with onPress](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/E7GRbm2QRkLlrDR9NkuwC_cc-card-onpress.PNG "Card with onPress")
:::
::::

:::CodeblockTabs
card-onPress

```yaml
title: card with onPress
type: jig.default

children:
  - type: component.card
    instanceId: card1
    options:
      color: color9
      onPress: 
        type: action.go-to
        options:
          linkTo: product-item-simple
      children:
        - type: component.image
          options:
            source:
              uri: https://images.unsplash.com/photo-1472851294608-062f824d29cc?q=80&w=2304&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        - type: component.entity
          options:
            children:
              - type: component.entity-field
                options:
                  label: ''
                  value: Shop now
                  rightIcon: arrow-button-right-1
                
```
:::
:::::

