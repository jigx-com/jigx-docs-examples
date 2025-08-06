# open-url

This action opens a web page depending on the provided URL or [deep links](https://docs.jigx.com/deep-links) to an external app. open-url can be used in a list of actions, such as `swipeable` and `rightElement`, or with another action; after the main action is executed, open-url is called and opens the configured URL.

## Configuration options

An open-url action can be set up in various ways:

1. As a separate action or in the action list.
2. As a `swipeable` action in the left or right direction.
3. As `rightElement` in the list.
4. As an associated action in the action list.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="94">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a title for opening the URL, you can use expressions in the title field.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>url</code></p>
    </td>
    <td selected="false" align="left">
      <p>Specify the URL you want opened. The following formats are supported: </p>
      <p>https://</p>
      <p><a href="">www</a>.
      sitename.com
      external app link (See the deep link to an external app example)</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### open-url as an action

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/T3ZC0Rad-LbIo-TwkAz0n_gtzweo29zg0gybp4gfc9paiphone13blueportrait.png" size="80" position="center" caption="Open URL" alt="Open URL" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/T3ZC0Rad-LbIo-TwkAz0n_gtzweo29zg0gybp4gfc9paiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
The simplest example of using an open-url action is to use it as a separate action. Thanks to this, a button will appear at the bottom, which, when pressed, will open the specific URL that we set up.

**Example:**
See the full example in \<[GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/open-url/open-url-action.jigx).
:::
::::

```yaml
actions:
  - children:
      - type: action.open-url
        options:
          title: Jigx Documentation
          url: https://docs.jigx.com/examples/open-url
```
:::::

:::::ExpandableHeading
### open-url swipeable left/right

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/85MfW1I1rRzJZ2nViXGqn_lwkiwhqm9jefwzaddms2sopen-url-swipeableiphone13blueportrait.png" size="78" position="center" caption="Swipe to open URL" alt="Swipe to open URL " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/85MfW1I1rRzJZ2nViXGqn_lwkiwhqm9jefwzaddms2sopen-url-swipeableiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example uses the open-url action as a swipeable property. We can choose the swipe direction left or right. After pressing the button, it will open the specific url that we set up.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/open-url/open-url-swipeable.jigx).
:::
::::

```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.lastname
    subtitle: =@ctx.current.item.firstname
    leftElement: 
      element: avatar
      text: " "
      uri: =@ctx.current.item.img
    swipeable:
      left:
        - label: Open Url 
          onPress:
            type: action.open-url
            options:
              url: https://docs.jigx.com/examples/open-url
      right:
        - label: Open Url 
          onPress: 
            type: action.open-url
            options:
              url: https://docs.jigx.com/examples/open-url
```
:::::

:::::ExpandableHeading
### open-url rightElement

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GYadDhjMgTy2NrPEZyzmh_udarll0iezuhktkkwiufopen-url-rightiphone13blueportrait.png" size="80" position="center" caption="Button to open URL" alt="Button to open URL" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GYadDhjMgTy2NrPEZyzmh_udarll0iezuhktkkwiufopen-url-rightiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
In this example, we use the open-url action as the rightElement in the list-item component. There is a button for each item.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/open-url/open-url-right-element.jigx).
:::
::::

```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.lastname
    subtitle: =@ctx.current.item.firstname
    leftElement: 
      element: avatar
      text: " "
      uri: =@ctx.current.item.img
    rightElement: 
      element: button
      title: Open
      onPress:
        type: action.open-url
        options:
          url: https://docs.jigx.com/examples/open-url
```
:::::

:::::ExpandableHeading
### open-url onSuccess

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/w6iMDziHnqSet6KtsHYWi_scmmooymdeswthvqltsmbopen-url-onsuccessiphone13blueportrait.png" size="80" position="center" caption="Open URL onSuccess" alt="Open URL onSuccess" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/w6iMDziHnqSet6KtsHYWi_scmmooymdeswthvqltsmbopen-url-onsuccessiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
In this example, the open-url action is associated with the submit-form action. After we enter the signature and press the "Sign" button, the submit-form action is performed and the specific url will be opened.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/open-url/open-url-on-success.jigx).
:::
::::

:::CodeblockTabs
open-url-on-success.jigx

```yaml
actions:
  - children:
      - type: action.action-list
        options:
          title: Sign and go to documentation
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/form
                method: create
                data:
                  signature: =@ctx.components.signature.state.value
                onSuccess: 
                  title: Succesfully signed
                  actions:
                    - type: action.open-url
                      options:
                        title: Open the documentation
                        url: https://docs.jigx.com/examples
            - type: action.go-back
```
:::
:::::

:::::ExpandableHeading
### Use open-url to deep link to an external app

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
In this example, the `action.open-url` is used with a deep link that opens the Google Maps app to a specific location. There are two code examples, one for iOS and the other for Andriod.
:::

:::VerticalSplitItem
![Open Google Maps](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-4baP6op8VhWdNkzk2mhU_cc-appdeeplink.PNG "Open Google Maps")
:::
::::

:::CodeblockTabs
iOS-open-url

```yaml
title: Zoos in the USA
type: jig.default

actions:
  - children:
      - type: action.open-url #iOS
        options:
          title: Directions
          # Add the external app's iOS deep link in the url    
          url: comgooglemaps://?center=32.7347483943,-117.150943196&zoom=14
    
children:
  - type: component.image
    options:
      source:
        uri: https://c8.alamy.com/comp/2GFT773/san-diego-california-25-aug-2021-san-diego-zoo-main-entrance-in-balboa-park-2GFT773.jpg
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: San Diego Zoo
            value: The San Diego Zoo is 100 acres in size. It is well known for its lush, naturalistic habitats and unique animal encounters and is home to more than 3,700 rare and endangered animals representing approximately 660 species and subspecies and a prominent botanical collection with more than 700,000 plants.
```

Android-open-url

```yaml
title: Zoos in the USA
type: jig.default

actions:
  - children:  
      - type: action.open-url #android
        options:
          title: Directions
          # Add the external app's Android deep link in the url
          url: google.navigation:q=2920+Zoo+Dr,San+Diego,CA+92101,United+States
      
children:
  - type: component.image
    options:
      source:
        uri: https://c8.alamy.com/comp/2GFT773/san-diego-california-25-aug-2021-san-diego-zoo-main-entrance-in-balboa-park-2GFT773.jpg
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: San Diego Zoo
            value: |
             The San Diego Zoo is 100 acres in size.
             It is well known for its lush, naturalistic habitats and unique animal encounters
             and is home to more than 3,700 rare and endangered animals representing approximately
             660 species and subspecies and a prominent botanical collection with more than 700,000 plants.
```
:::
:::::

