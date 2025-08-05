# Combine custom & standard components (Alpha)

:::hint{type="danger"}
This feature is currently in its **Alpha** stage of development.

- As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
- In this phase, the feature may contain bugs or behave unpredictably.
- Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
- We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.
:::

Combining [Custom components (Alpha)](<./../Custom components _Alpha_.md>) with [Standard components](./../Components.md) enables the creation of advanced functionality and rich user interfaces. Standard components, such as [stepper](./../Components/stepper.md) , [progress-bar](./../Components/progress-bar.md) , and [countdown](./../Components/countdown.md) , provide a reliable foundation for common interactions, ensuring consistency and usability. By integrating custom components and tailored elements designed to meet specific requirements, you can extend this functionality to create dynamic features like interactive menus, tabbed navigation, and toggles with unique behaviors. This blend allows for a balance between efficiency and creativity, enabling apps to stand out with innovative designs while maintaining intuitive user experiences.

Additionally, you can take this further by **creating entirely new components** through the clever use of custom components or by combining standard and custom components. These new components can encapsulate specialized functionality, offer unique visual elements, or address specific user needs, opening up endless possibilities for tailored solutions. To ensure the reuse of custom components in the same jig or in different jigs, you can use [Inputs & outputs (Alpha)](https://docs.jigx.com/inputs-and-outputs-alpha).

This approach encourages modular development, fostering scalability and adaptability, whether for small projects or enterprise-grade applications.

Here are code examples to illustrate combining custom and standard components to build advanced features.

### Considerations

- When using `component.image` in a custom component, the `height` property must be specified as part of the `size` property. Otherwise, validation errors occur, see below:

:::CodeblockTabs
Correct YAML

```yaml
# Correct YAML snippet for using the height property in the image component,
# when used in a custom component.
- type: component.image
          options:
            size: 
              height: 196
            source:
              uri: https://images
```

Incorrect YAML

```yaml
# Incorrect YAML snippet for using the height property in the image component,
# when used in a custom component.
- type: component.image
          options:
            height: 196
            source:
              uri: https://images     
```
:::

## Example and code samples

The examples use a set of custom components called *sections*. The sections are for titles, spacing, and context. The *sections* code is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).

:::::ExpandableHeading
### Countdown

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-3qwiIlmNqKU__uU3e5yrB-20241114-092231.png" size="48" position="center" caption="Countdown" alt="Countdown" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-3qwiIlmNqKU__uU3e5yrB-20241114-092231.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::

:::VerticalSplitItem
In this example, the first `component.countdown` is a standard component and the following four are custom components. Here, the `component.countdown` is configured in a `component.card` with color.

**Example:**

1. See the *section* component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/countdown).
3. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/countdown/countdown.jigx).
:::
::::

:::CodeblockTabs
countdown.jigx

```yaml
# jigs/countdown.jigx 
title: Countdown
type: jig.default
icon: time-reverse

children:
  - type: component.custom-component
    componentId: section2
    inputs:
      title: STANDARD COMPONENTS
# Standard countdown component.      
  - type: component.countdown
    options:
      expiresAt: =$fromMillis($toMillis($now()) + (14 * 24 * 60 * 60 * 1000))
      labels:
        position: top
        isVisible: true
      align: stretch
  - type: component.custom-component
    componentId: section2
    inputs:
      title: CUSTOM COMPONENTS
  - type: component.custom-component
    componentId: section2
    inputs:
      title: Small
# Custom countdown component contained in a card, aligned left, & size set to small.      
  - type: component.custom-component
    componentId: countdown
  - type: component.custom-component
    componentId: section2
    inputs:
      title: Medium
# Custom countdown component contained in a card with a color & size set to medium.         
  - type: component.custom-component
    componentId: countdown2
  - type: component.custom-component
    componentId: section2
    inputs:
      title: Large   
# Custom countdown component contained in a card with color & size set to large.      
  - type: component.custom-component
    componentId: countdown3
  - type: component.custom-component
    componentId: section2
    inputs:
      title: Extra Large   
# Custom countdown component contained in a card with color & size set to X-large.        
  - type: component.custom-component
    componentId: countdown4
```

countdown.jigx&#x20;

```yaml
# components/countdown.jigx 
type: component.default
children:
# Custom card component contains the standard countdown component.
  - type: component.card
    options:
      direction: column
      children:
# Standard countdown component.       
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + (14 * 24 * 60 * 60 * 1000))
            labels:
              position: bottom
              isVisible: true
            size: small
            align: left
```

countdown2.jigx

```yaml
# components/countdown2.jigx 
type: component.default
children:
# Custom card component contains the standard countdown component.
  - type: component.card
    options:
      color: color3
      children:
# Standard countdown component.      
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + (14 * 24 * 60 * 60 * 1000))
            labels:
              position: bottom
            size: medium
```

countdown3.jigx

```yaml
# components/countdown3.jigx 
type: component.default
children:
# Custom card component contains the standard countdown component.
  - type: component.card
    options:
      color: color4
      children:
# Standard countdown component.       
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + (14 * 24 * 60 * 60 * 1000))
            labels:
              position: top
            size: large
```

countdown4.jigx

```yaml
# components/countdown4.jigx 
type: component.default
children:
# Custom card component contains the standard countdown component.
  - type: component.card
    options:
      color: color5
      children:
# Standard countdown component.      
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + (14 * 24 * 60 * 60 * 1000))
            labels:
              position: bottom
            size: extra-large
```
:::
:::::

:::::ExpandableHeading
### Progress Bar

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, the `component.progress-bar`, is customized by adding a `component.card`, `component.icon`, and `component.text` to achieve the required appearance.

**Example:**

1. See the *section* component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/basic-elements/progressbar/progress-sample-1.jigx).
3. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-basic.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-k9S-WX-dQLP59hWunApnu-20241114-094230.png" size="48" position="center" caption="Progress-bar" alt="Progress-bar" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-k9S-WX-dQLP59hWunApnu-20241114-094230.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::
::::

:::CodeblockTabs
progressbar-basic.jigx

```yaml
# jigs/progressbar-basic.jigx
title: Progress Bars - Basic
type: jig.default
icon: loading-half

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1607434472257-d9f8e57a643d?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mzh8fGNvbWluZyUyMHNvb24lMjBsb2FkaW5nfGVufDB8fDB8fHww

children:
# Three progress bars customized by placing them in cards, 
# using views to create the correct layout using gaps.
  - type: component.custom-component
    componentId: progress-sample-1
# Icons create the stars and text.    
  - type: component.custom-component
    componentId: progress-sample-2
```

progress-sample-1.jigx

```yaml
# components/progress-sample1.jigx 
type: component.default
children:
# Custom component used to contain the standard progress-bar component.
  - type: component.view
    options:
      style:
        gap: medium
      children:     
        - type: component.card
          options:
            children:
# Standard progress-bar component.            
              - type: component.progress-bar
                options:
                  value:
                    current: =@ctx.solution.state.progressValue
                    max: 20
                  title:
                    value: Title
                    align: right
                    position: bottom
                  subtitle:
                    value: Subtitle
                    align: left
                    position: bottom    
# Custom card component contains the standard component.
        - type: component.card
          options:
            children:
# Standard progress-bar component.            
              - type: component.progress-bar
                options:
                  value:
                    current: =@ctx.solution.state.progressValue
                    max: 20
                  size: extra-large
                  title:
                    value: Title
                    align: left
                    position: top
                  subtitle:
                    value: Subtitle
                    align: right
                    position: bottom                      
# Custom card component contains the standard component.
        - type: component.card
          options:
            children:
              - type: component.view
                options:
                  style:
                    background:
                      color: color12
                  children:
 # Standard progress-bar component.                 
                    - type: component.progress-bar
                      options:
                        value:
                          current: =@ctx.solution.state.progressValue
                          max: 20
```

progress-sample-2.jigx

```yaml
# components/progress-sample2.jigx 
type: component.default
children:
# Custom card component contains the standard progress-bar component.
  - type: component.card
    options:
      children:
# View component determines the layout of the custom component.     
        - type: component.view
          options:
            style:
              gap: medium
              flex: 
                direction: row             
            children:
# View component determines the layout of the custom component.              
              - type: component.view
                options:
                  style:
                    flex: 
                      grow: 0
                    alignItems: center
                    justifyContent: center
                    padding: medium
                  children:
                    - type: component.text
                      options:
                        value: "4.7"
                        size: extra-large
                    - type: component.text
                      options:
                        value: out of 5
                        size: small
                        emphasis: medium  
# View component determines the layout of the custom component.                                         
              - type: component.view
                options:
                  style:
                    flex: 
                      grow: 1
                  children:
# View component determines the layout of the custom component.                   
                    - type: component.view
                      options:
                        style:
                          flex: 
                            grow: 1
                            direction: row
                          alignContent: center                          
                        children:
# View component determines the layout of the custom component. 
                          - type: component.view
                            options:
                              style:
                                flex: 
                                  direction: row
                                alignItems: center
                                width: 50
                                justifyContent: flex-end
                                emphasis: low-medium
                              children:
                              # Rating stars created using custom components.
                                - type: component.icon
                                  options:
                                    icon: rating-star
                                    size: extra-small
                                - type: component.icon
                                  options:
                                    icon: rating-star
                                    size: extra-small
                                - type: component.icon
                                  options:
                                    icon: rating-star
                                    size: extra-small
                                - type: component.icon
                                  options:
                                    icon: rating-star
                                    size: extra-small
                                - type: component.icon
                                  options:
                                    icon: rating-star
                                    size: extra-small                                                                                                                    
                          # Standard progress-bar component.
                          - type: component.progress-bar
                            options:
                              size: medium
                              value:
                                current: 0.5
                                max: 20
# View component determines the layout of the custom component. 
                    - type: component.view
                      options:
                        style:
                          flex: 
                            grow: 1
                            direction: row
                          alignContent: center
                        children:
# View component determines the layout of the custom component.                        
                          - type: component.view
                            options:
                              style:
                                flex: 
                                  direction: row
                                alignItems: center
                                width: 50
                                justifyContent: flex-end
                                emphasis: low-medium
                              children:
                              # Rating stars created using custom components.
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small                                                                                                               
                          # Standard progress-bar component.
                          - type: component.progress-bar
                            options:
                              size: medium
                              value:
                                current: 0.5
                                max: 20                                      
# View component determines the layout of the custom component.    
                    - type: component.view
                      options:
                        style:
                          flex: 
                            grow: 1
                            direction: row
                          alignContent: center                          
                        children:
# View component determines the layout of the custom component.                          
                          - type: component.view
                            options:
                              style:
                                flex: 
                                  direction: row
                                alignItems: center
                                width: 50
                                justifyContent: flex-end
                                emphasis: low-medium
                              children:
                              # Rating stars created using custom components.
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small                                                                                                                 
                          # Standard progress-bar component.
                          - type: component.progress-bar
                            options:
                              size: medium
                              value:
                                current: 0.5
                                max: 20    
# View component determines the layout of the custom component.                                        
                    - type: component.view
                      options:
                        style:
                          flex: 
                            grow: 1
                            direction: row
                          alignContent: center
                        children:
# View component determines the layout of the custom component.                                                    
                          - type: component.view
                            options:
                              style:
                                flex: 
                                  direction: row
                                alignItems: center
                                width: 50
                                justifyContent: flex-end
                                emphasis: low-medium
                              children:
                              # Rating stars created using custom components.
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small 
                          # Standard progress-bar component.
                          - type: component.progress-bar
                            options:
                              size: medium
                              value:
                                current: 0.5
                                max: 20                                        
# View component determines the layout of the custom component.  
                    - type: component.view
                      options:
                        style:
                          flex: 
                            grow: 1
                            direction: row
                          alignContent: center
                        children:
# View component determines the layout of the custom component.                        
                          - type: component.view
                            options:
                              style:
                                flex: 
                                  direction: row
                                alignItems: center
                                width: 50
                                justifyContent: flex-end
                                emphasis: low-medium
                              children:
                              # Rating stars created using custom components.
                              - type: component.icon
                                options:
                                  icon: rating-star
                                  size: extra-small                                                                                                                 
                          # Standard progress-bar component.
                          - type: component.progress-bar
                            options:
                              size: medium
                              value:
                                current: 0.5
                                max: 20   
                              title:
                                value: Title                               
```

:::

More examples of customized progress bars are available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar):

|   |   |
|:----------|:----------|
| [Progress-bar with details](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-details.jigx)    | [Progress-bar with top labels](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-top-labels.jigx)   |
| [Progress-bar sizes](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-sizes-dynamic.jigx) (Dynamic)    |[Progress-bar with bottom labels](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-bottom-labels.jigx)     |
| [Progress-bar steps](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/progressbar/progressbar-steps-dynamic.jigx)(Dynamic)   |     | 

:::

:::::

:::::ExpandableHeading

### Ratings

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Npl-iTbt3CbHZqYsyA1Xf-20241114-095208.png" size="48" position="center" caption="Ratings " alt="Ratings" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Npl-iTbt3CbHZqYsyA1Xf-20241114-095208.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::

:::VerticalSplitItem
This example demonstrates how you can create your own component using the custom components. Here various rating components are created by configuring the `component.view` and `component.text`.

**Example:**

1. See the *section* component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/rating).
3. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/rating/rating.jigx).

:::
::::

:::CodeblockTabs
rating.jigx

```yaml
# jigs/rating.jigx
title: Ratings
type: jig.default
icon: star-half

children:
  - type: component.section
    options:
      title: stars
      children:
# Custom component created using view & text components.     
        - type: component.custom-component
          componentId: rating-1

  - type: component.section
    options:
      title: stars with statistics
      children:
# Custom component created using view & text components.          
        - type: component.custom-component
          componentId: rating-2
          inputs: 
            rating: 4.5
            rating-number: 6.4

  - type: component.section
    options:
      title: Statistics
      children:
# Custom component created using view & text components.          
        - type: component.custom-component
          componentId: rating-3
          inputs: 
            rating: 4.5
            rating-number: 6.4   

  - type: component.section
    options:
      title: Emoji rating - emphasis
      children:
# Custom component created using view & text components.          
        - type: component.custom-component
          componentId: rating-4

  - type: component.section
    options:
      title: Emoji rating - background
      children:
# Custom component created using view & text components.          
        - type: component.custom-component
          componentId: rating-5
```

rating-1.jigx

```yaml
# components/rating-1.jigx 
type: component.default
children:
# Custom component created using view & text components. 
  - type: component.view
    options:
      style:
        flex: 
          direction: row
        justifyContent: space-evenly
      children:
        - type: component.text
          options:
            align: center
# Adding an onPress event sets the rating icons with the configured color & emphasis,
# when pressed.            
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 1
            size: extra-large
            color: =@ctx.solution.state.rating != null ? 'warning':'element'
            emphasis: =@ctx.solution.state.rating != null ? '':'low'
            value: ★
        - type: component.text
          options:
            align: center
# Adding an onPress event sets the rating icons with the configured color & emphasis,
# when pressed.              
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 2
            size: extra-large
            color: =$number(@ctx.solution.state.rating) > 1 ? 'warning':'element'
            emphasis: =$number(@ctx.solution.state.rating) > 1 ? '':'low'            
            value: ★
        - type: component.text
          options:
            align: center
# Adding an onPress event sets the rating icons with the configured color & emphasis,
# when pressed.              
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 3
            size: extra-large
            color: =$number(@ctx.solution.state.rating) > 2 ? 'warning':'element'
            emphasis: =$number(@ctx.solution.state.rating) > 2 ? '':'low'
            value: ★
        - type: component.text
          options:
            align: center
# Adding an onPress event sets the rating icons with the configured color & emphasis,
# when pressed.             
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 4
            size: extra-large
            color: =$number(@ctx.solution.state.rating) > 3 ? 'warning':'element'
            emphasis: =$number(@ctx.solution.state.rating) > 3 ? '':'low'
            value: ★
        - type: component.text
          options:
            align: center
# Adding an onPress event sets the rating icons with the configured color & emphasis,
# when pressed.              
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 5
            size: extra-large
            color: =$number(@ctx.solution.state.rating) > 4 ? 'warning':'element'
            emphasis: =$number(@ctx.solution.state.rating) > 4 ? '':'low'
            value: ★
            
```

rating-2.jigx

```yaml
# components/rating-2.jigx 
type: component.default
children:
# Custom component created using view & text components. 
  - type: component.view
    options:
      style:
        justifyContent: center
        alignItems: center
        gap: small
      children:
# The rating value is set in the text component.           
        - type: component.text
          options:
            value: =@ctx.inputs.rating-number & 'K' & ' RATINGS'
            emphasis: medium
            weight: semi-bold
            size: small
        - type: component.view
          options:
            style:
              gap: minimal
              alignItems: center
            children:
              - type: component.text
                options:
                  value: =@ctx.inputs.rating
                  size: large
                  weight: semi-bold
              - type: component.view
                options:
                  style:
                    flex:
                      direction: row
                    gap: minimal
                  children:
                    - type: component.text
                      options:
                        value: ★
                        size: medium
                        color: =@ctx.inputs.rating >= 1 ? 'warning':'element'
                        emphasis: =@ctx.inputs.rating >= 1 ? '':'low'
                    - type: component.text
                      options:
                        value: ★
                        size: medium
                        color: =@ctx.inputs.rating >= 2 ? 'warning':'element'
                        emphasis: =@ctx.inputs.rating >= 2 ? '':'low'
                    - type: component.text
                      options:
                        value: ★
                        size: medium
                        color: =@ctx.inputs.rating >= 3 ? 'warning':'element'
                        emphasis: =@ctx.inputs.rating >= 3 ? '':'low'
                    - type: component.text
                      options:
                        value: ★
                        size: medium
                        color: =@ctx.inputs.rating >= 4 ? 'warning':'element'
                        emphasis: =@ctx.inputs.rating >= 4 ? '':'low'
                    - type: component.text
                      options:
                        value: ★
                        size: medium
                        color: =@ctx.inputs.rating >= 4.5 ? 'warning':'element'
                        emphasis: =@ctx.inputs.rating >= 4.5 ? '':'low'
```

rating-3.jigx

```yaml
# components/rating-3.jigx 
type: component.default
children:
# View component determines the layout of the custom component. 
  - type: component.view
    options:
      style:
        justifyContent: center
        alignItems: center
        gap: small
      children:
# The rating value is set in the text component.      
        - type: component.text
          options:
            value: =@ctx.inputs.rating-number & 'K' & ' RATINGS'
            emphasis: medium
            weight: semi-bold
            size: small
        - type: component.view
          options:
            style:
              flex:
                direction: row
              gap: minimal
              alignItems: center
            children:
              - type: component.text
                options:
                  value: =@ctx.inputs.rating
                  size: extra-large
                  weight: semi-bold
                  emphasis: medium
              - type: component.text
                options:
                  value: ★
                  size: large
                  weight: semi-bold
                  emphasis: medium
```

rating-4.jigx

```yaml
# components/rating-4.jigx 
type: component.default
children:
# View component determines the layout of the custom component. 
  - type: component.view
    options:
      style:
        flex: 
          grow: 1
          shrink: 1
          basis: 1
          direction: row
        justifyContent: space-evenly
      children:
        - type: component.view
          options:
            style: {}
# Adding an onPress event sets the state when pressed.            
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 1 
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
# When the rating value is pressed the background is highlighted in a color.                   
                  emphasis: =$number(@ctx.solution.state.rating) = 1 ? '':'medium'
# The rating value is set to use an emoji instead of an icon.                      
                  value: 😭
        - type: component.view
          options:
            style: {}
# Adding an onPress event sets the state when pressed to the value.             
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 2 
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  emphasis: =$number(@ctx.solution.state.rating) = 2 ? '':'medium'
# The rating value is set to use an emoji instead of an icon.                      
                  value: ☹️
        - type: component.view
          options:
            style: {}
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 3  
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  emphasis: =$number(@ctx.solution.state.rating) = 3 ? '':'medium'
                  value: 😐
        - type: component.view
          options:
            style: {}
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 4 
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  emphasis: =$number(@ctx.solution.state.rating) = 4 ? '':'medium'
                  value: 🙂
        - type: component.view
          options:
            style: {}
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 5 
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  emphasis: =$number(@ctx.solution.state.rating) = 5 ? '':'medium'
                  value: 😍
```

rating-5.jigx

```yaml
# components/rating-5.jigx 
type: component.default
children:
# View component determines the layout of the custom component. 
  - type: component.view
    options:
      style:
        flex: 
          grow: 1
          shrink: 1
          basis: 1
          direction: row
        justifyContent: space-evenly
      children:
        - type: component.view
          options:
            style:
              justifyContent: center
              alignItems: center
              height: 60
              width: 60
              radius: large
# When the rating icon is pressed the background is highlighted in a color.               
              background:
                color: =$number(@ctx.solution.state.rating) = 1 ? 'color3':''
# Adding an onPress event sets the state when pressed.                 
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 1
            children:
# The rating value is set to use an emoji instead of an icon.          
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  value: 😭
        - type: component.view
          options:
            style:
              justifyContent: center
              alignItems: center
              height: 60
              width: 60
              radius: large
              background:
                color: =$number(@ctx.solution.state.rating) = 2 ? 'color3':''
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 2
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  value: ☹️
        - type: component.view
          options:
            style:
              justifyContent: center
              alignItems: center
              height: 60
              width: 60
              radius: large
              background:
                color: =$number(@ctx.solution.state.rating) = 3 ? 'color3':''
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 3
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  value: 😐
        - type: component.view
          options:
            style:
              justifyContent: center
              alignItems: center
              height: 60
              width: 60
              radius: large
              background:
                color: =$number(@ctx.solution.state.rating) = 4 ? 'color3':''
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 4
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  value: 🙂
        - type: component.view
          options:
            style:
              justifyContent: center
              alignItems: center
              height: 60
              width: 60
              radius: large
              background:
                color: =$number(@ctx.solution.state.rating) = 5 ? 'color3':''
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.rating
                value: 5
            children:
              - type: component.text
                options:
                  align: center
                  size: extra-large
                  value: 😍
```
:::
:::::

:::::ExpandableHeading

### Sections

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how you can create one custom component and reuse it multiple times, in this instance, in the same jig. We use `inputs` to show different data and elements in each reuse of the custom component. Here a standard `component.avatar` is combined with `component.view`, `component.text` and `component.icon`.

**Example:**

1. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_czeKbMWCCPZwwMK3bo5k-20241114-102305.png" size="48" position="center" caption="Sections" alt="Sections" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_czeKbMWCCPZwwMK3bo5k-20241114-102305.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::
::::

:::CodeblockTabs
section-header-greetings.jigx

```yaml
# jigs/section-header-greetings.jigx
title: Greetings
type: jig.default
icon: wave-hand

children:
  - type: component.section
    options:
      title: Greeting 1
      children:
# Custom component created using view, icon & text components. 
# Inputs are used to add the required data in the custom component.          
        - type: component.custom-component
          componentId: greetings
          inputs:
            avatar: https://t14345253.p.clickup-attachments.com/t14345253/34139efb-6a96-468d-9604-cb1b9484e2ff/avarat10.png?view=open
            avatar-size: regular
            name: John
            welcome-message: Hello
            linkTo: link-here
  - type: component.section
    options:
      title: Greeting with date
      children:
# Custom component created using view, icon & text components. 
# Inputs are used to add the required data in the custom component.          
        - type: component.custom-component
          componentId: greetings
          inputs:
            avatar: https://t14345253.p.clickup-attachments.com/t14345253/34139efb-6a96-468d-9604-cb1b9484e2ff/avarat10.png?view=open
            avatar-size: regular
            date: =$fromMillis($toMillis($now()), '[FNn], [D]. [M]. [Y]')
            name: John
            welcome-message: Hello
            linkTo: link-here
  - type: component.section
    options:
      title: Greeting with date and large avatar
      children:
# Custom component created using view, icon & text components. 
# Inputs are used to add the required data in the custom component.         
        - type: component.custom-component
          componentId: greetings
          inputs:
            avatar: https://t14345253.p.clickup-attachments.com/t14345253/34139efb-6a96-468d-9604-cb1b9484e2ff/avarat10.png?view=open
            avatar-size: large
            date: =$fromMillis($toMillis($now()), '[FNn], [D]. [M]. [Y]')
            name: John
            welcome-message: Hello
            linkTo: link-here
  - type: component.section
    options:
      title: Greeting with date and icon
      children:
# Custom component created using view, icon & text components. 
# Inputs are used to add the required data in the custom component.          
        - type: component.custom-component
          componentId: greetings
          inputs:
            avatar: https://t14345253.p.clickup-attachments.com/t14345253/34139efb-6a96-468d-9604-cb1b9484e2ff/avarat10.png?view=open
            avatar-size: regular
            date: =$fromMillis($toMillis($now()), '[FNn], [D]. [M]. [Y]')
            linkTo: link-here
            name: John
# The configuration of the right-icon inputs displays the right blue pencil icon.             
            right-icon: pencil
            right-icon-color: color9
            right-icon-link: link-here
            welcome-message: Hello
  - type: component.section
    options:
      title: Greeting with date and icon and large avatar
      children:
# Custom component created using view, icon & text components. 
# Inputs are used to add the required data in the custom component.         
        - type: component.custom-component
          componentId: greetings
          inputs:
            avatar: https://t14345253.p.clickup-attachments.com/t14345253/34139efb-6a96-468d-9604-cb1b9484e2ff/avarat10.png?view=open
            avatar-size: large
            date: =$fromMillis($toMillis($now()), '[FNn], [D]. [M]. [Y]')
            name: John
# The configuration of the right-icon inputs displays the right blue pencil icon.             
            right-icon: pencil
            right-icon-color: color9
            welcome-message: Hello
            right-icon-link: link-here
            linkTo: link-here
```

greetings.jigx

```yaml
# components/greetings.jigx 
type: component.default
children:
# Custom component created using view & text components. 
# View determines the layout.
  - type: component.view
    options:
      style:
        alignItems: center
        flex:
          direction: row
        gap: small
# Standard avatar component.  
      children:
        - type: component.avatar
          options:
            title: =@ctx.inputs.name
            size: =@ctx.inputs.avatar-size
            uri: =@ctx.inputs.avatar
# View is used to set the gap between the avatar and text.         
        - type: component.view
          options:
            style:
              flex:
                grow: 1
              gap: =@ctx.inputs.avatar-size = 'large' ? 'small':''
# Custom component text adds the message text. 
            children:
              - type: component.text
                options:
# Configure the text message to use inputs that is configured in the jig.                
                  size: =@ctx.inputs.avatar-size = 'large' ? 'large':'medium'
                  value: =@ctx.inputs.welcome-message & ', ' & @ctx.inputs.name
                  weight: semi-bold
                
              - type: component.view
                when: =@ctx.inputs.date != null
                options:
                  style:
                    justifyContent: center
                  children:
                    - type: component.text
                      options:
                        emphasis: high
                        size: small
 # Configure the text message to use a date input that is configured in the jig.                       
                        value: ="It's" & ' ' & @ctx.inputs.date

        - type: component.view
          when: =@ctx.inputs.right-icon != null
          options:
            style: {}
            children:
# Custom component icon dynamically set with inputs and styled with options.             
              - type: component.icon
                options:
                  color: =@ctx.inputs.right-icon-color
                  icon: =@ctx.inputs.right-icon
                  shape: circle
                  size: small
                  type: duotone
# Add an onPress event to go to another jig that is dynamically set in the jig using inputs.                
            onPress:
              type: action.go-to
              options:
                linkTo: =@ctx.inputs.right-icon-link
# Add an onPress event to go to another jig that is dynamically set in the jig using inputs.              
      onPress:
        type: action.go-to
        options:
          linkTo: =@ctx.inputs.linkTo
```

:::

More examples of customized sections are available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections):

|                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Section header samples](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-samples.jigx)        | [Section sizes - medium (extra-bold)](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-sizes-med-xbold.jigx) |
| [Section sizes - regular](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-sizes-reg.jigx)     | [Section sizes - large](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-sizes-large.jigx)                   |
| [Section sizes - medium](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-sizes-med.jigx)      | [Section sizes - extra large](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-sizes-extra-large.jigx)       |
| [Section header with subtitle](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/sections/section-header-subtitle.jigx) | 
 |

:::::

:::::ExpandableHeading

### Stepper

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Steppers](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SqhIJwlC1MtJGk9LMqLBA-20241114-102836.png "Steppers")
:::

:::VerticalSplitItem
This example demonstrates how you can create one custom component and reuse it multiple times, in this instance in the two different jigs. We use `inputs` to show the number of steps and current steps in each reuse of the custom component. Here a stepper component is created by configuring the `component.view`.

**Example:**

1. See the *section* component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/stepper/stepper1.jigx).
3. See the *jig* example in \<[GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style1-variations.jigx).

:::
::::

:::CodeblockTabs
stepper-style1.jigx

```yaml
# jigs/stepper-style1.jigx 
title: Stepper Style 1
type: jig.default
icon: phone-swap

children:
  - type: component.custom-component
    componentId: headline
    inputs:
      headline2: Stepper 1
      subtitle: |
        - numberOfSteps: 1-6 
        - currentStep: 1-6
      linkTo: stepper-style1-variations
      link: variations
# Custom component created using the view component. 
# Inputs are used to determine the number of steps and current step,
# in the custom component.      
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 3
```

stepper-style1-variations.jigx

```yaml
# jigs/stepper-style1-variations.jigx 
title: Stepper 1 - Variations
type: jig.default

children:
  - type: component.custom-component
    componentId: section2
    inputs:
      title: 2 Items     
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 2
      currentStep: 1
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 2
      currentStep: 2

  - type: component.custom-component
    componentId: section2
    inputs:
      title: 3 Items
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 3
      currentStep: 1
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 3
      currentStep: 2
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 3
      currentStep: 3  

  - type: component.custom-component
    componentId: section2
    inputs:
      title: 4 Items      
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 4
      currentStep: 1
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 4
      currentStep: 2
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 4
      currentStep: 3  
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 4
      currentStep: 4     


  - type: component.custom-component
    componentId: section2
    inputs:
      title: 5 Items
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 1
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 2
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 3  
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 4           
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 5
      currentStep: 5     


  - type: component.custom-component
    componentId: section2
    inputs:
      title: 6 Items
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 1
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 2
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 3  
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 4           
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 5    
  - type: component.custom-component
    componentId: stepper1
    inputs:
      numberOfSteps: 6
      currentStep: 6  
```

stepper1.jigx

```yaml
# components/stepper1.jigx 
type: component.default
# Specify the inputs used in the component.
inputs:
  numberOfSteps:
    default: 1
    required: true
    type: number
  currentStep:    
    default: 1
    required: true
    type: number

children:
# Use view to set the layout in the component.
  # Stepper
  - type: component.view
    options:
      style:
        flex: 
          grow: 1
          direction: row
        alignItems: center
        justifyContent: center
        
      children: 
# Configure the first blue point in the stepper.
        - type: component.view
          options:
            style:
              background:
                color: primary
              radius: large
              height: 24
              width: 24
            children: []
# Configure the blue line between the points in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 2
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 2 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 2 ? "":"low"
              height: 2
              flex: 
                grow: 1
              width: 
                min: 8
                max: 40                  
            children: []                        
# Configure the second blue point in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 2
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 2 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 2 ? "":"low"
              radius: large
              height: 24
              width: 24
            children: []  
# Configure the blue line between the points in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 3
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 3 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 3 ? "":"low"
              height: 2
              flex: 
                grow: 1
              width: 
                min: 8
                max: 40                  
            children: []                                                
# Configure the third blue point in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 3
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 3 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 3 ? "":"low"
              radius: large
              height: 24
              width: 24
            children: []   
# Configure the blue line between the points in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 4
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 4 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 4 ? "":"low"
              height: 2
              flex: 
                grow: 1
              width: 
                min: 8
                max: 40                  
            children: []                          
# Configure the fourth blue point in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 4
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 4 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 4 ? "":"low"
              radius: large
              height: 24
              width: 24
            children: []  
# Configure the blue line between the points in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 5
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 5 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 5 ? "":"low"
              height: 2
              flex: 
                grow: 1
              width: 
                min: 8
                max: 40                  
            children: []                          
# Configure the fifth blue point in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 5
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 5 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 5 ? "":"low"
              radius: large
              height: 24
              width: 24
            children: []   
# Configure the blue line between the points in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 6
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 6 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 6 ? "":"low"
              height: 2
              flex: 
                grow: 1
              width: 
                min: 8
                max: 40                  
            children: []                           
# Configure the sixth blue point in the stepper.
        - type: component.view
          when: =$number(@ctx.inputs.numberOfSteps) >= 6 
          options:
            style:
              background: 
                color: =$number(@ctx.inputs.currentStep) >= 6 ? "primary":"element"
                emphasis: =$number(@ctx.inputs.currentStep) >= 6 ? "":"low"
              radius: large
              height: 24
              width: 24
            children: []                                                                                                 
```
:::

More examples of customized sections are available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper):

|                                                                                                                                                                                                          |                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Stepper style 2](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style2.jigx) | [Stepper style 6](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style6.jigx) |
| [Stepper style 3](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style3.jigx) | [Stepper style 7](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style7.jigx) |
| [Stepper style 4]()                                                                                                                                                                                      | [Stepper style 8](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style8.jigx) |
| [Stepper style 5](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/stepper/stepper-style5.jigx) |                                                                                                                                                                                                          |
:::::

:::::ExpandableHeading

### Tabs

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how you can create custom components and reuse them multiple times. We use `inputs` to show the tab value, name, indicator and alignment in each reuse of the custom component. Here tab components are created by configuring the `component.view`. Additionally, we show how to reference a custom component inside a standard `component.list-item`.

**Example:**

1. See the *section* component example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/sections).
2. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/tabs).
3. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/tabs/tabs.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-a-MnTk6l7a1IoAevGnBKt-20241114-103014.png" size="48" position="center" caption="Tabs" alt="Tabs" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-a-MnTk6l7a1IoAevGnBKt-20241114-103014.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::
::::

:::CodeblockTabs
tabs.jigx

```yaml
# jigs/tabs.jigx
title: Tabs
type: jig.default
icon: app-window-four

onFocus:
  type: action.action-list
  options:
    isSequential: false
    actions:
      - type: action.set-state
        when: =$not($exists(@ctx.solution.state.tab))
        options:
          state: =@ctx.solution.state.tab
          value: tab2

datasources:
  store-feed-tabs:
    type: datasource.static
    options:
      data:
        - tabName: Tab 1
          tabValue: tab1
        - tabName: Tab 2
          tabValue: tab2
        - tabIndicator: true
          tabName: Tab 3
          tabValue: tab3
        - tabIndicator: true
          tabName: Tab 4
          tabValue: tab4
        - tabName: Tab 5
          tabValue: tab5
        - tabName: Tab 6
          tabValue: tab6
    
children:
  - type: component.section
    options:
      title: Static tabs - Center Align
      children:
# Custom component created using the view component. 
# Inputs are used to determine tab name, value, alignment and indicator.
        - type: component.custom-component
          componentId: tabs
          inputs:
            tabIndicator1: false
            tabIndicator2: true
            tabIndicator3: true
            tabIndicator4: true
            tabName1: Tab 1
            tabName2: Tab 2
            tabName3: Tab 3
            tabName4: Tab 4
            tabValue1: tab1
            tabValue2: tab2
            tabValue3: tab3
            tabValue4: tab4
            tabsAlignment: center
             
  - type: component.section
    options:
      title: Static tabs - Left Align
      children:
# Same custom component reused as above using the view component. 
# Using inputs you can change the appearance of the same custom component.
        - type: component.custom-component
          componentId: tabs
          inputs:
            tabIndicator1: false
            tabIndicator2: true
            tabIndicator3: true
            tabIndicator4: true
            tabName1: Tab 1
            tabName2: Tab 2
            tabName3: Tab 3
            tabName4: Tab 4
            tabValue1: tab1
            tabValue2: tab2
            tabValue3: tab3
            tabValue4: tab4
              
  - type: component.section
    options:
      title: Stretched static tabs
      children:
# Custom component created using the view component. 
# Inputs are used to determine tab name, value, and indicator.   
        - type: component.custom-component
          componentId: tabs-stretched
          inputs:
            tabIndicator1: false
            tabIndicator2: true
            tabIndicator3: true
            tabIndicator4: true
            tabName1: Tab 1
            tabName2: Tab 2
            tabName3: Tab 3
            tabName4: Tab 4
            tabValue1: tab1
            tabValue2: tab2
            tabValue3: tab3
            tabValue4: tab4
          
        - type: component.custom-component
          componentId: tabs-stretched
          inputs:
            tabIndicator1: false
            tabIndicator2: true
            tabName1: Tab 1
            tabName2: Tab 2
            tabValue1: tab1
            tabValue2: tab2
          
  - type: component.section
    options:
      title: List item tabs
      children:
        - type: component.list
          options:
            maximumItemsToRender: 8
            data: =@ctx.datasources.store-feed-tabs
            isHorizontal: true
            isHorizontalScrollIndicatorHidden: true
            item:
# Custom component created using the view component.
# Custom component added inside a standard list-item cpmponent. 
# Inputs are used to determine tab name, and value in th custom component.            
              type: component.custom-component
              componentId: list-item-tabs
              inputs:
                tabIndicator: =@ctx.current.item.tabIndicator
                tabName: =@ctx.current.item.tabName
                tabValue: =@ctx.current.item.tabValue
```

tabs.jigx

```yaml
# components/tabs.jigx
type: component.default
# Specify the inputs used in the component.
inputs:
  tabIndicator1:
    required: false
    type: boolean
    
  tabIndicator2:
    required: false
    type: boolean
    
  tabIndicator3:
    required: false
    type: boolean
    
  tabIndicator4:
    required: false
    type: boolean
    
  tabName1:
    required: true
    type: string
    
  tabName2:
    required: true
    type: string
    
  tabName3:
    required: false
    type: string
    
  tabName4:
    required: false
    type: string
    
  tabValue1:
    required: true
    type: string
    
  tabValue2:
    required: true
    type: string
    
  tabValue3:
    required: false
    type: string
    
  tabValue4:
    required: false
    type: string
    
  tabsAlignment:
    required: false
    type: string

children:
# Use the view component to create the layout. 
  - type: component.view
    options:
      style:
        border:
          bottom:
            style: solid
        flex:
          direction: row
          grow: 1
        justifyContent: center
        margin:
          vertical: medium
      children:
# Configure tab 1 using the view and text components.
        - type: component.view
          when: =@ctx.inputs.tabValue1 != null
          options:
            style:
              flex:
                direction: row
                grow: =@ctx.inputs.stretchTabs = true ? 1:0
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"               
            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center
# Use the text component to create the tab names.                          
                        children:             
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ? "":"medium"
                              value: =@ctx.inputs.tabName1
                              weight: bold                      
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
# Configure the view to show a red dot as an indicator next to the tab name.                                     
              - type: component.view
                when: =@ctx.inputs.tabIndicator1 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
# Configure the onPress event to switch tabs when pressed.                      
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue1
# Configure tab 2 using the view and text components.
        - type: component.view
          when: =@ctx.inputs.tabValue2 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"
            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center

                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ? "":"medium"
                              value: =@ctx.inputs.tabName2
                              weight: bold

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2

              - type: component.view
                when: =@ctx.inputs.tabIndicator2 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
# Configure the onPress event to switch tabs when pressed.     
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue2
# Configure tab 3 using the view and text components.
        - type: component.view
          when: =@ctx.inputs.tabValue3 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"

            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center

                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ? "":"medium"
                              value: =@ctx.inputs.tabName3
                              weight: bold
                                                  
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
                                      
              - type: component.view
                when: =@ctx.inputs.tabIndicator3 = true
                options:
                  style:
                    flex:
                      grow: 1                     
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
# Configure the onPress event to switch tabs when pressed.     
            onPress:
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue3
              type: action.set-state
# Configure tab 4 using the view and text components.
        - type: component.view
          when: =@ctx.inputs.tabValue4 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"
            children:
              - type: component.view
                options:
                  style:
                    gap: medium                   
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center                         
                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ? "":"medium"
                              value: =@ctx.inputs.tabName4
                              weight: bold                                                 
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
              - type: component.view
                when: =@ctx.inputs.tabIndicator4 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
# Configure the onPress event to switch tabs when pressed.     
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue4
```

tabs-stretched.jigx

```yaml
#components/tabs-stretched.jigx
type: component.default
# Specify the inputs used in the component.
inputs:
  tabIndicator1:
    required: false
    type: boolean
  tabIndicator2:
    required: false
    type: boolean
  tabIndicator3:
    required: false
    type: boolean
  tabIndicator4:
    required: false
    type: boolean
  tabName1:
    required: true
    type: string
  tabName2:
    required: true
    type: string
  tabName3:
    required: false
    type: string
  tabName4:
    required: false
    type: string
  tabValue1:
    required: true
    type: string
  tabValue2:
    required: true
    type: string
  tabValue3:
    required: false
    type: string
  tabValue4:
    required: false
    type: string
# Use the view component to create the layout.
children:
  - type: component.view
    options:
      style:
        border:
          bottom:
            style: solid
        flex:
          direction: row
          grow: 1
        margin:
          vertical: medium
# Configure tab 1 using the view and text components.
      children:
        - type: component.view
          when: =@ctx.inputs.tabValue1 != null
          options:
            style:
              flex:
                direction: row
                grow: 1
              gap: minimal
            children:
              - type: component.view
                options:
                  style:
                    flex:
                      grow: 1
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                            grow: 1
                          gap: minimal
                          justifyContent: center
                        children:
# Use the text component to create the tab name.                        
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ? "":"medium"
                              value: =@ctx.inputs.tabName1
                              weight: bold   
# Configure the view to show a red dot as an indicator next to the tab name.                                                      
                          - type: component.view
                            when: =@ctx.inputs.tabIndicator1 = true
                            options:
                              children: []
                              style:
                                background:
                                  color: negative
                                height: 6
                                radius: large
                                width: 6
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
# Configure the onPress event to switch tabs when pressed. 
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue1
 # Configure tab 2 using the view and text components.             
        - type: component.view
          when: =@ctx.inputs.tabValue2 != null
          options:
            style:
              flex:
                direction: row
                grow: 1
              gap: minimal
            children:
              - type: component.view
                options:
                  style:
                    flex:
                      grow: 1
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                            grow: 1
                          gap: minimal
                          justifyContent: center
# Use the text component to create the tab name. 
                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ? "":"medium"
                              value: =@ctx.inputs.tabName2
                              weight: bold
# Configure the view to show a red dot as an indicator next to the tab name.                            
                          - type: component.view
                            when: =@ctx.inputs.tabIndicator2 = true
                            options:
                              children: []
                              style:
                                background:
                                  color: negative
                                height: 6
                                radius: large
                                width: 6
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ?
                              "element":"transparent"
                          flex: 
                            grow: 1
# Configure the onPress event to switch tabs when pressed. 
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue2
# Configure tab 3 using the view and text components.                        
        - type: component.view
          when: =@ctx.inputs.tabValue3 != null
          options:
            style:
              flex:
                direction: row
                grow: 1
              gap: minimal
            children:
              - type: component.view
                options:
                  style:
                    flex:
                      grow: 1
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                            grow: 1
                          gap: minimal
                          justifyContent: center
# Use the text component to create the tab name. 
                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ? "":"medium"
                              value: =@ctx.inputs.tabName3
                              weight: bold 
# Configure the view to show a red dot as an indicator next to the tab name.                                                         
                          - type: component.view
                            when: =@ctx.inputs.tabIndicator3 = true
                            options:
                              children: []
                              style:
                                background:
                                  color: negative
                                height: 6
                                radius: large
                                width: 6
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
# Configure the onPress event to switch tabs when pressed. 
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue3
# Configure tab 4 using the view and text components.
        - type: component.view
          when: =@ctx.inputs.tabValue4 != null
          options:
            style:
              flex:
                direction: row
                grow: 1
              gap: minimal
            children:
              - type: component.view
                options:
                  style:
                    flex:
                      grow: 1
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                            grow: 1
                          gap: minimal
                          justifyContent: center
# Use the text component to create the tab name.                         
                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ? "":"medium"
                              value: =@ctx.inputs.tabName4
                              weight: bold
# Configure the view to show a red dot as an indicator next to the tab name.                             
                          - type: component.view
                            when: =@ctx.inputs.tabIndicator4 = true
                            options:
                              children: []
                              style:
                                background:
                                  color: negative
                                height: 6
                                radius: large
                                width: 6

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2
# Configure the onPress event to switch tabs when pressed. 
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue4
```

list-item-tabs.jigx

```yaml
#components/list-item-tabs.jigx
type: component.default
# Specify the inputs used in the component.
inputs:
  tabIndicator:
    required: false
    type: boolean
  tabName:
    required: true
    type: string
  tabValue:
    required: true
    type: string
# Use the view component to create the layout.
children:
  - type: component.view
    when: =@ctx.inputs.tabValue != null
    options:
      style:
        flex:
          basis: 1
          direction: row
          grow: 1
        gap: minimal
        padding:
          right: large
      children:
        - type: component.view
          options:
            style:
              gap: medium
            children:
              - type: component.view
                options:
                  style:
                    alignItems: center
                    flex:
                      direction: row
                    gap: minimal
                    justifyContent: center
                  children:
# Configure the tab name.                 
                    - type: component.text
                      options:
                        emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue ? "":"medium"
                        value: =@ctx.inputs.tabName
                        weight: bold

              - type: component.view
                options:
                  children: []
                  style:
                    background:
                      color: =@ctx.solution.state.tab = @ctx.inputs.tabValue ? "element":"transparent"
                    flex:
                      grow: 1
                    height: 2
# Configure the view to show a red dot as an indicator next to the tab name. 
        - type: component.view
          when: =@ctx.inputs.tabIndicator = true
          options:
            style:
              flex:
                grow: 1
            children:
              - type: component.view
                options:
                  children: []
                  style:
                    background:
                      color: negative
                    height: 6
                    radius: large
                    width: 6
# Configure the onPress event to switch tabs when pressed. 
      onPress:
        type: action.set-state
        options:
          state: =@ctx.solution.state.tab
          value: =@ctx.inputs.tabValue
```
:::
:::::

:::::ExpandableHeading
### Tags

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-CUZSlXSPFZahDNId27IH7-20241114-103058.png" size="50" position="center" caption="Tags" alt="Tags" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-CUZSlXSPFZahDNId27IH7-20241114-103058.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::

:::VerticalSplitItem
This example demonstrates how you can create tags in a custom component. We use `inputs` in the custom component to show the tag color and title. Here a tab component is created by configuring the `component.view` and `component.text`. Additionally, we show you how to reference a custom component inside a standard `component.list`, and use a second custom component to create an action allowing you to tap a link at the top to add new tag.

**Example:**

1. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/components/molecules-organisms/tags/tags.jigx).
2. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/tags/tags.jigx).
:::
::::

:::CodeblockTabs
tags.jigx

```yaml
#jigs/tags.jigx
title: Tags
type: jig.default
icon: tags-double-1

header:
  type: component.jig-header
  options:
    height: small
    children:
      options:
        source:
          uri: https://images.unsplash.com/photo-1578575737601-bd8f2557550c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHJlbGF4aW5nJTIwbmF0dXJlfGVufDB8MHwwfHx8MA%3D%3D&auto=format&fit=crop&w=800&q=60
      type: component.image

datasources:
  mydata:
    type: datasource.static
    options:
      data:
        - id: 1
          tags:
            - color: color1
              title: tag_1
            - color: color2
              title: tag_2
            - color: color3
              title: tag_3
            - color: color4
              title: tag_4
    
children:
  - type: component.custom-component
    componentId: header-2
    inputs:
      link: Add Tags
      title: ""
    
  - type: component.list
    when: =@ctx.datasources.mydata.tags != null
    options:
      maximumItemsToRender: 10
      data: =@ctx.datasources.mydata.tags
      isHorizontal: true
      isHorizontalScrollIndicatorHidden: true
      item:
# Custom component created using the view and text components.
# Custom component added inside a standard list-item component. 
# Inputs are used to determine tag color and text value.       
        type: component.custom-component
        componentId: view-todo-tags
        inputs:
          info: =@ctx.current.item
# Custom component created using the view and card components.
# Inputs are used to determine the onPress action's title.
  - type: component.custom-component
    when: =@ctx.datasources.mydata.tags = null
    componentId: add-button
    inputs:
      title: Add Tags
```

view-todo-tags.jigx

```yaml
# components/view-todo-tags.jigx
type: component.default
children:
# Use the view component to create the layout.
  - type: component.view
    options:
      style:
        background:
          color: =@ctx.inputs.info.color
        margin:
          left: medium
        padding: small
        radius:
          bottomLeft: tiny
          bottomRight: large
          topLeft: tiny
          topRight: large
      children:
# Configure the text on the tags using inputs.      
        - type: component.text
          options:
            value: =@ctx.inputs.info.title
```

add-button.jigx

```yaml
# components/add-button.jigx
type: component.default
# Create a button link to add a new tag. 
children:
  - type: component.card
    options:
      children:
        - type: component.view
          options:
            children:
              - type: component.icon
                options:
                  emphasis: medium
                  icon: add
                  size: small
# Use the text component to add a title on the button link.                
              - type: component.text
                options:
                  emphasis: medium
                  size: medium
                  value: =@ctx.inputs.title
            style:
              flex:
                direction: row
              gap: small
              justifyContent: center
              padding: minimal
# Configure the action to call when the button link is pressed.           
      onPress:
        type: action.action-list
        options:
          actions:
            - options:
                parameters:
                  data: =@ctx.inputs.data
                  id: =@ctx.inputs.id
                linkTo: add-notes
              type: action.go-to
              when: =@ctx.inputs.title = 'Add Notes'
          isSequential: true
```
:::
:::::

:::::ExpandableHeading
### Toggles

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how you can create a custom component providing the functionality to toggle. We use `inputs` to determine the toggle name, highlighting and value. Here a toggle component is created by configuring the `component.view` and `component.text`. Additionally, we show you how to reference a custom component inside a standard `component.list`. The custom component is configured with the `onPress` event to trigger an action when the toggle is pressed.

**Example:**

1. See the *custom component* example in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/components/molecules-organisms/toggles).
2. See the *jig* example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/d5eb38a64423482ed10703b0b2889709beee309c/quickstart/jigx-samples/jigs/custom-components/molecules-organisms/toggles/toggles.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_frjcbq6BgaicVmNICaMG-20241114-103225.png" size="48" position="center" caption="Toggles" alt="Toggles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_frjcbq6BgaicVmNICaMG-20241114-103225.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
:::
::::

:::CodeblockTabs
toggles.jigx

```yaml
#jigs/toggles.jigx
title: Toggles
type: jig.default
icon: toggle-setting-off

onFocus:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.set-state
        when: =$not($exists(@ctx.solution.state.list-item-switch))
        options:
          state: =@ctx.solution.state.tab
          value: ""

      - type: action.set-state
        when: =$not($exists(@ctx.solution.state.switch))
        options:
          state: =@ctx.solution.state.switch
          value: switch-item1

datasources:
  categories:
    type: datasource.static
    options:
      data:
        - category-name: All
          state-value: ""
        - category-name: Completed
          state-value: completed
        - category-name: In Progress
          state-value: in-progress
        - category-name: Closed
          state-value: closed

children:
  - type: component.section
    options:
      title: List item categories
      children:
        - type: component.list
          options:
            maximumItemsToRender: 8
            data: =@ctx.datasources.categories
            isHorizontal: true
            item:
# Custom component created using the view and text components.
# Custom component added inside a standard list component. 
# Inputs are used to determine toggle name and text value.            
              type: component.custom-component
              componentId: list-item-switch
              inputs:
                switchName: =@ctx.current.item.category-name
                switchValue: =@ctx.current.item.state-value


  - type: component.section
    options:
      title: Switch
      children:
        - type: component.custom-component
          componentId: switch
          inputs:
            extraSpace: false
            switchName1: Item 1
            switchName2: Item 2
            switchName3: Item 3
            switchValue1: switch-item1
            switchValue2: switch-item2
            switchValue3: switch-item3
            
  - type: component.section
    options:
      title: Switch - Highlighted
      children:
            item:
# Custom component created using the view and text components.
# Inputs are used to determine toggle name, and text value and highlighting.
        - type: component.custom-component
          componentId: switch
          inputs:
            extraSpace: false
            highlighted: true
            switchName1: Item 1
            switchName2: Item 2
            switchName3: Item 3
            switchValue1: switch-item1
            switchValue2: switch-item2
            switchValue3: switch-item3
            
  - type: component.section
    options:
      title: Switch with counters
      children:
        - type: component.custom-component
          componentId: switch
          inputs:
            extraSpace: false
            switchCount1: 3
            switchCount2: 1
            switchName1: Projects
            switchName2: Tasks
            switchValue1: switch-item1
            switchValue2: switch-item2
            
  - type: component.section
    options:
      title: Switch with counters - Highlighted
      children:
# Custom component created using the view and text components.
# Inputs are used to determine toggle name, and text value and highlighting.
        - type: component.custom-component
          componentId: switch
          inputs:
            extraSpace: false
            highlighted: true
            switchCount1: 3
            switchCount2: 1
            switchName1: Projects
            switchName2: Tasks
            switchValue1: switch-item1
            switchValue2: switch-item2
```

switch.jigx

```yaml
# components/switch.jigx
type: component.default
# Specify the inputs used in the component.   
inputs:
  highlighted:
    default: true
    required: false
    type: boolean
  switchCount1:
    required: false
    type: number
  switchCount2:
    required: false
    type: number
  switchCount3:
    required: false
    type: number
  switchName1:
    required: true
    type: string
  switchName2:
    required: true
    type: string
  switchName3:
    required: false
    type: string
  switchValue1:
    required: true
    type: string
  switchValue2:
    required: true
    type: string
  switchValue3:
    required: false
    type: string
# Use the view component to create the layout.
children:
  - type: component.view
    options:
      style:
        background:
          color: ="element"
          emphasis: extra-low
        flex:
          direction: row
          grow: 1
        margin:
          top: none
        padding: minimal
        radius: large
# Configure the first switch/toggle.
      children:
        - type: component.view
          when: =@ctx.inputs.switchName1 != null
          options:
            style:
              alignItems: center
              background:
                color: =@ctx.solution.state.switch = @ctx.inputs.switchValue1 ?
                  @ctx.inputs.highlighted = true ? "primary":"card"
              flex:
                basis: 1
                direction: row
                grow: 1
              gap: minimal
              justifyContent: center
              padding:
                horizontal: medium
                vertical: small
              radius: large
            children:
# Configure the first switch/toggle's name.            
              - type: component.text
                options:
                  align: center
                  color: |
                    =@ctx.solution.state.switch = @ctx.inputs.switchValue1 and
                    @ctx.inputs.highlighted = true ? "":"element"
                  value: =@ctx.inputs.switchName1
                
              - type: component.view
                when: =@ctx.inputs.switchCount1 != null
                options:
                  style:
                    alignItems: center
                    border:
                      color: =@ctx.solution.state.switch = @ctx.inputs.switchValue1 and
                        @ctx.inputs.highlighted = true ? "":"element"
                      emphasis: medium
                      style: solid
                    height: 18
                    justifyContent: center
                    radius: large
                    width: 18
                  children:
                    - type: component.text
                      options:
                        align: center
                        color: |
                          =@ctx.solution.state.switch = @ctx.inputs.switchValue1 and
                          @ctx.inputs.highlighted = true ? "":"element"
                        emphasis: medium
                        size: tiny
                        value: =@ctx.inputs.switchCount1
# Configure the onPress event to toggle between switches when pressed.                       
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.switch
                value: =@ctx.inputs.switchValue1
# Configure the second switch/toggle.                       
        - type: component.view
          when: =@ctx.inputs.switchName2 != null
          options:
            style:
              alignItems: center
              background:
                color: =@ctx.solution.state.switch = @ctx.inputs.switchValue2 ?
                  @ctx.inputs.highlighted = true ? "primary":"card"
              flex:
                basis: 1
                direction: row
                grow: 1
              gap: minimal
              justifyContent: center
              padding:
                horizontal: medium
                vertical: small
              radius: large
# Configure the second switch/toggle's name.
            children:
              - type: component.text
                options:
                  align: center
                  color: =@ctx.solution.state.switch = @ctx.inputs.switchValue2 and
                    @ctx.inputs.highlighted = true ? "":"element"
                  value: =@ctx.inputs.switchName2
                
              - type: component.view
                when: =@ctx.inputs.switchCount2 != null
                options:
                  style:
                    alignItems: center
                    border:
                      color: =@ctx.solution.state.switch = @ctx.inputs.switchValue2 and
                        @ctx.inputs.highlighted = true ? "":"element"
                      emphasis: medium
                      style: solid
                    height: 18
                    justifyContent: center
                    radius: large
                    width: 18

                  children:
                    - type: component.text
                      options:
                        align: center
                        color: =@ctx.solution.state.switch = @ctx.inputs.switchValue2 and
                          @ctx.inputs.highlighted = true ? "":"element"
                        emphasis: medium
                        size: tiny
                        value: =@ctx.inputs.switchCount2
# Configure the onPress event to toggle between switches when pressed.   
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.switch
                value: =@ctx.inputs.switchValue2
# Configure the third's switch/toggle.                       
        - type: component.view
          when: =@ctx.inputs.switchName3 != null
          options:
            style:
              alignItems: center
              background:
                color: =@ctx.solution.state.switch = @ctx.inputs.switchValue3 ?
                  @ctx.inputs.highlighted = true ? "primary":"card"
              flex:
                basis: 1
                direction: row
                grow: 1
              gap: minimal
              justifyContent: center
              padding:
                horizontal: medium
                vertical: small
              radius: large
# Configure the third switch/toggle's name.
            children:
              - type: component.text
                options:
                  align: center
                  color: =@ctx.solution.state.switch = @ctx.inputs.switchValue3 and
                    @ctx.inputs.highlighted = true ? "":"element"
                  value: =@ctx.inputs.switchName3
                
              - type: component.view
                when: =@ctx.inputs.switchCount3 != null
                options:
                  style:
                    alignItems: center
                    border:
                      color: =@ctx.solution.state.switch = @ctx.inputs.switchValue3 and
                        @ctx.inputs.highlighted = true ? "":"element"
                      emphasis: medium
                      style: solid
                    height: 18
                    justifyContent: center
                    radius: large
                    width: 18

                  children:
                    - type: component.text
                      options:
                        align: center
                        color: =@ctx.solution.state.switch = @ctx.inputs.switchValue3 and
                          @ctx.inputs.highlighted = true ? "":"element"
                        emphasis: medium
                        size: tiny
                        value: =@ctx.inputs.switchCount3
# Configure the onPress event to toggle between switches when pressed.                         
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.switch
                value: =@ctx.inputs.switchValue3
```

list-item-switch.jigx

```yaml
# components/list-item-switch.jigx
type: component.default
# Specify the inputs used in the component.
inputs: 
  switchName:
    required: true
    type: string  
  switchValue:
    required: true
    type: string
# Use the view component to create the layout.
children:
  - type: component.view
    options:
      style:
        background:
          color: =@ctx.solution.state.list-item-switch = @ctx.inputs.switchValue ?
            "primary":"element"
          emphasis: =@ctx.solution.state.list-item-switch = @ctx.inputs.switchValue ?
            "none":"extra-low"
        flex:
          direction: row
        margin:
          right: small
        padding:
          horizontal: medium
          vertical: small
        radius: large
# Configure the switch/toggle's name.        
      children:
        - type: component.text
          options:
            color: =@ctx.solution.state.list-item-switch = @ctx.inputs.switchValue ?
              "":"element"
            value: =@ctx.inputs.switchName
# Configure the onPress event to toggle between switches when pressed.             
      onPress:
        type: action.set-state
        options:
          state: =@ctx.solution.state.list-item-switch
          value: =@ctx.inputs.switchValue
```
:::
:::::

