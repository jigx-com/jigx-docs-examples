# jig-header

The `jig-header` component can be used in any type of jig. It serves as a container for specifying headers. It cannot be used without a component [image](./../Widgets/image.md), [location](./location.md), or [video-player](./video-player.md) inside the component.

:::hint{type="info"}
The images can be preloaded and cached using the asset folder's images file. The images will be displayed even when you are offline.  For more details, refer to [Assets](#).
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `children`         | Specifies which component will be used inside the jig-header. There are three options:<br />* [component.image](./image.md)
* [component.location](./location.md)
* [component.video player](./video-player.md)                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `height`           | Specifies the height of the header.<br />* `small`
* `medium`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `actions`          | Choose an action from the available list, such as `go-to` to open a different jig or `open-url` to navigate to a website. The selected action appears as a link in the top right corner of the header.<br />* Set the `icon` property in the action to display the action link as an icon instead of text.
* Styles of actions are inherited, for example, disabling the link.
* You can add multiple action links in the header, but ensure they accommodate the jig title and overall screen design.
* To prevent the jig `title` and header action links from overlapping while scrolling, use either one text action or up to three icon actions. |

:::hint{type="warning"}
Jigx does not recommend storing images in Dynamic Data (via any conversion), as the max file size per record is 350K.
:::

## Examples and code snippets

:::::ExpandableHeading
### Jig-header with image

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RQPQfkwE0vOo6no2yvRYW_header-image-smalliphone13blueportrait.png" size="76" position="center" caption="Header with image" alt="Header with image" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RQPQfkwE0vOo6no2yvRYW_header-image-smalliphone13blueportrait.png"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TtPV4N7FAxx1F2vm-lvSH_header-image-mediumiphone13blueportrait.png" size="74" position="center" caption="Header with image" alt="Header with image" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TtPV4N7FAxx1F2vm-lvSH_header-image-mediumiphone13blueportrait.png"}
:::
::::

This example shows a `component.jig-header` with property `children: component.image`and the difference between the set heights.

**Examples**:
See the code samples using static data in GitHub for [small](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-image/jig-header-image-small.jigx) and [medium](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-image/jig-header-image-medium.jigx) headers.

:::CodeblockTabs
small

```yaml
header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg
```

medium

```yaml
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg
```
:::
:::::

:::::ExpandableHeading
### Jig-header with location

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Location in header](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cQZEvoQcr1J_SDuWosHd7-20250221-091813.png "Location in header")
:::

:::VerticalSplitItem
This example shows a `component.jig-header` with property `children: component.location` and the difference between the set heights.
Refer to the [location](./location.md) component for additional location setup options.

**Examples**:
See the code samples using static data in GitHub for [small](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/jig-header/static-data/jig-header-location/jig-header-location-small.jigx) and [medium](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-location/jig-header-location-medium.jigx) headers.
:::
::::

:::CodeblockTabs
location-as-header(small)

```yaml
header: 
  type: component.jig-header
  options:
    height: small
    children:
      type: component.location
      options:
        viewPoint:
          # Center the address in the middle of the screen.
          centerPosition: middle
          # Sepcify the address using a datasource.
          address: =@ctx.datasources.sites[0].address
          # Zoom in for map clearly.
          zoomLevel: 8
        # Add endpoint marker icon for the address.  
        markers:
          data: =@ctx.datasources.sites[0].address
          item:
            type: component.marker-item
            options:
              address: =@ctx.datasources.sites[0].address
              children:
                type: component.icon
                options:
                  # Determine the color of the marker icon.
                  color: negative
                  # Define the icon in the datasource.
                  icon: =@ctx.datasources.sites[0].icon
```

location-as-header(medium)

```yaml
header: 
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.location
      options:
        viewPoint:
          # Center the address in the middle of the screen.
          centerPosition: middle
          # Sepcify the address using a datasource.
          address: =@ctx.datasources.sites[0].address
          # Zoom in for map clearly.
          zoomLevel: 8
        # Add endpoint marker icon for the address.  
        markers:
          data: =@ctx.datasources.sites[0].address
          item:
            type: component.marker-item
            options:
              address: =@ctx.datasources.sites[0].address
              children:
                type: component.icon
                options:
                  # Determine the color of the marker icon.
                  color: negative
                  # Define the icon in the datasource.
                  icon: =@ctx.datasources.sites[0].icon
```

datasource

```yaml
datasources:
  sites:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Empire State Building
          latitude: 40.748676182418976
          longitude: -73.98567513213604
          address: 20 W 34th St., New York, NY 10001, United States
          icon: landmark-empire-state
        - id: 2
          name: Great Lawn Softball Field 6
          latitude: 40.782091612607864 
          longitude: -73.9655512166898
          address: 86th St Transverse, New York, NY 10024, United States
          icon: stadium-1-building 
```
:::
:::::

:::::ExpandableHeading
### Jig-header with video-player

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/I2ErZFzeEDrRwupEWmysV_cc-header-small.PNG" size="76" position="center" caption="Small - header with video player" alt="Header with video player" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/I2ErZFzeEDrRwupEWmysV_cc-header-small.PNG"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/N468nPuSNoW9OEiZaf_EW_cc-header-medium.PNG" size="74" position="center" caption="Medium - header with video player" alt="Header with video player" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/N468nPuSNoW9OEiZaf_EW_cc-header-medium.PNG"}
:::
::::

This example shows a `component.jig-header` with property `children: component.video-player.` and the difference between the set heights.

**Examples**:
See the code samples using static data in GitHub for [small](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-video-player/jig-header-videoplayer-small.jigx) and [medium](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-video-player/jig-header-videoplayer-medium.jigx) headers.

:::CodeblockTabs
small

```yaml
header: 
  type: component.jig-header
  options:
    height: small
    children:
      type: component.video-player
      options:
        url: https://cdn.pixabay.com/video/2023/10/01/183108-870151713_small.mp4
        title: video-player
        autoplay: false
```

medium

```yaml
header: 
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.video-player
      options:
        url: https://cdn.pixabay.com/video/2023/10/01/183108-870151713_small.mp4
        title: video-player
        autoplay: false
```
:::
:::::

:::::ExpandableHeading
### Jig-header with an action (text link)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-2ffdFGQ8eLAPkrZ5vRK48-20250224-072301.png" size="70" position="center" caption="Jig header with an action" alt="Jig header with an action" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-2ffdFGQ8eLAPkrZ5vRK48-20250224-072301.png"}
:::

:::VerticalSplitItem
This example shows a `component.jig-header`  configured with an action. The action displays as a link in the top right corner of the header. Ensure the action is visible and not obscured by the header image or video. The `open-url` action is configured to open the Jigx website.
:::
::::

:::CodeblockTabs
small

```yaml
title: Jig- header with action
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1605712916066-e143c317df72?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fHByb2JsZW18ZW58MHx8MHx8fDA%3D
# Configure the action applicable to the header.
# The action displays as a link in the top right corner of the header.            
    actions:
      - type: action.go-to
        options:
          title: Ask a question
          linkTo: ai-chat

children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Helpful Resources
            children:
              - type: component.entity-field
                options:
                  label: Documentation
                  value: https://docs.jigx.com/
              - type: component.entity-field
                options:
                  label: Community
                  value: https://community.jigx.com/
              - type: component.entity-field
                options:
                  contentType: email
                  label: Support
                  value: support@jigx.com            
```
:::
:::::

:::::ExpandableHeading
### Jig-header with multiple actions (icons)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-m2qCNX2Ka63cThTwIfJDO-20250210-134415.png" size="70" position="center" caption="Jig header with icon actions" alt="Jig header with icon actions" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-m2qCNX2Ka63cThTwIfJDO-20250210-134415.png"}
:::

:::VerticalSplitItem
This example demonstrates a `component.jig-header` configured with three `open-url` actions, displayed as icons in the top right corner of the header. Styling is applied to two of the icons to ensure visibility. Make sure the actions are not obscured by the header image/video or the jig `title` when scrolling. The `open-url` actions open various Jigx websites.

***
:::
::::

:::CodeblockTabs
small

```yaml
title: Jig- header (icon actions)
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: 
            https://images.unsplash.com/photo-1475965894430-b05c9d13568a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTJ8fHdoaXRlJTIwcGF0dGVybmVkJTIwY29sb3IlMjBiYWNrZ3JvdW5kc3xlbnwwfHwwfHx8MA%3D%3D
# Configure multiple actions applicable to the header.
# Add icons for each action link. 
# Set the style for two of the action icons.
# The actions display the icons (not the text) in the top right corner of the header.          
     actions:
      - type: action.open-url
        options:
          icon: contact-us-customer-support-chat
          style:
          # Displays the icon in red or the brand's designated danger color.
            isDanger: true
          title: Ask a question
          url: https://jigx.com/
      - type: action.open-url
        options:
          # Icon displays in the primary color when no styling is configured.
          icon: document
          title: Documentation
          url: https://docs.jigx.com/
      - type: action.open-url
        options:
          style:
          # Displays the icon in yellow or the brand's designated secodary color.
            isSecondary: true
          icon: people-protester
          title: Community
          url: https://community.jigx.com/       
      
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Helpful Resources
            children:
              - type: component.entity-field
                options:
                  label: Documentation
                  value: https://docs.jigx.com/
              - type: component.entity-field
                options:
                  label: Community
                  value: https://community.jigx.com/
              - type: component.entity-field
                options:
                  contentType: email
                  label: Support
                  value: support@jigx.com            
```
:::
:::::

:::::ExpandableHeading
### Jig-header actions without header children

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
In this example, we use the `jig-header` action to create two actions with icons: one to open an `info-modal` and another to `go-to` a different jig.

The `jig-header` has no children (such as an image, location, or video player), which allows for greater flexibility in the header.
:::

:::VerticalSplitItem
![Jig-header action](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-es18hlzOsipHXjKwDCgMR-20250407-075200.png "Jig-header action")
:::
::::

:::CodeblockTabs
jig-header-action-without-children.jigx

```yaml
title: Header with no children
type: jig.default
# Add the header and only specify actions.
header:
  type: component.jig-header
  options:
    height: medium
    actions:
      # First action to go to a jig. The jig is opened as a modal. 
      - type: action.go-to
        options:
          title: Invoice
          icon: accounting-invoice
          linkTo: monthly-invoice
          isModal: true
      # Second action opens an info-modal showing an avatar.     
      - type: action.info-modal
        options:
          title: ""
          icon: person
          modal:
            title: This is you
            description: =@ctx.user.displayName
            buttonText: Close
            element: 
              type: avatar
              text: Your self
              uri: =@ctx.user.avatarUrl
            
children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Entity field
                  value: Text
```

monthly-invoice.jigx

```yaml
title: Monthly invoicing
description: Provide your details
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1450101499163-c8848c66ca85?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGludm9pY2luZ3xlbnwwfHwwfHx8MA%3D%3D    

children:
  - type: component.section
    options:
      title: Details
      children: 
        - type: component.form
          instanceId: inputValues
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  initialValue: =@ctx.user.displayName
                  label: First name
                  isRequired: false
              - type: component.email-field
                instanceId: email
                options:
                  initialValue: =@ctx.user.email
                  label: Email address
              - type: component.number-field
                instanceId: phoneNumber
                options:
                  initialValue: =@ctx.user.phone
                  label: Phone number

actions:
  - children:
      - type: action.action-list
        options:
          title: Send Invoice
          isSequential: true
          actions:
            - type: action.generate-pdf
              instanceId: generate-pdf-id
              options:
                # Provide the HTML for the PDF file.
                html: =@ctx.datasources.monthly-invoice-HTML.invoice-html
                fileName: invoice-1  
            - type: action.execute-entity
              options: 
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/documents
                method: create
                data:
                  fileName: invoice-1
                  date: =$now()
                  file: =@ctx.actions.generate-pdf-id.outputs.uri
                conversions:
                  - property: file
                    from: local-uri
                    to: data-uri      
            - type: action.share
              options:
                fileUri: =@ctx.actions.generate-pdf-id.outputs.uri
                message: Global Invoice 
                subject: Invoice for January
 
```

monthly-invoice-HTML.jigx

```yaml
type: datasource.static
options:
  data:     
    - id: 1
      invoice-html: |
       <!DOCTYPE html>
          <html lang="en">
          <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Invoice</title>
            <style>
              body {
                font-family: 'Arial', sans-serif;
                margin: 0;
                padding: 20px;
                background-color: #f6f6f6;
              }
              .invoice-box {
                max-width: 800px;
                margin: auto;
                padding: 30px;
                border: 1px solid #eee;
                box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
                background-color: #fff;
                color: #555;
              }
              .invoice-box table {
                width: 100%;
                line-height: 1.6;
                text-align: left;
                border-collapse: collapse;
              }
              .invoice-box table td {
                padding: 5px;
                vertical-align: top;
              }
              .invoice-box table tr td:nth-child(2) {
                text-align: right;
              }
              .invoice-box table tr.top table td {
                padding-bottom: 20px;
              }
              .invoice-box table tr.information table td {
                padding-bottom: 40px;
              }
              .invoice-box table tr.heading td {
                background: #eee;
                border-bottom: 1px solid #ddd;
                font-weight: bold;
              }
              .invoice-box table tr.details td {
                padding-bottom: 20px;
              }
              .invoice-box table tr.item td {
                border-bottom: 1px solid #eee;
              }
              .invoice-box table tr.item.last td {
                border-bottom: none;
              }
              .invoice-box table tr.total td:nth-child(2) {
                border-top: 2px solid #eee;
                font-weight: bold;
              }
              h2, h3 {
                margin: 0;
              }
            </style>
          </head>
          <body>
            <div class="invoice-box">
              <table cellpadding="0" cellspacing="0">
                <!-- Invoice Header -->
                <tr class="top">
                  <td colspan="2">
                    <table>
                      <tr>
                        <td class="title">
                          <h2>Company Name</h2>
                        </td>
                        <td>
                          Invoice #: 12345

                          Created: January 1, 2025

                          Due: January 31, 2025
                        </td>
                      </tr>
                    </table>
                  </td>
                </tr>
                <!-- Company & Customer Information -->
                <tr class="information">
                  <td colspan="2">
                    <table>
                      <tr>
                        <td>
                          Company Name, Inc.

                          12345 Street Address

                          City, State, Zip
                        </td>
                        <td>
                          Customer Name

                          Customer Company

                          67890 Customer Address
                        </td>
                      </tr>
                    </table>
                  </td>
                </tr>
                <!-- Payment Method Details -->
                <tr class="heading">
                  <td>Payment Method</td>
                  <td>Check #</td>
                </tr>
                <tr class="details">
                  <td>Check</td>
                  <td>1001</td>
                </tr>
                <!-- Itemized List of Services/Products -->
                <tr class="heading">
                  <td>Item</td>
                  <td>Price</td>
                </tr>
                <tr class="item">
                  <td>Website Design</td>
                  <td>$300.00</td>
                </tr>
                <tr class="item">
                  <td>Hosting (3 months)</td>
                  <td>$75.00</td>
                </tr>
                <tr class="item last">
                  <td>Domain Registration (1 year)</td>
                  <td>$10.00</td>
                </tr>
                <!-- Total -->
                <tr class="total">
                  <td></td>
                  <td>Total: $385.00</td>
                </tr>
              </table>
            </div>
          </body>
          </html>
```
:::
:::::

