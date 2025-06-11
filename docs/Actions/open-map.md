# open-map

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The open map action lets you tap the on-screen button to open your device's default map app (e.g., Google Maps, Apple Maps, or Waze) with the provided destination address. If multiple map apps are available, they will be listed for you to select one.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ceR_gXAWqyOYxwwBly0Kx-20250217-110927.gif" size="66" position="center" caption="Open map action" alt="Open map action" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ceR_gXAWqyOYxwwBly0Kx-20250217-110927.gif"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Provide the action with a title, for example, Navigate.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `address`          | Address of location - geocode string address to location.&#xA;Valid formats are: &#xA;- **address string - city, street**, e.g.&#xA; \`address: 20 W 34th St., New York, NY 10001, USA<br />`or in an expression calling a datasource `=@ctx.datasources.address&#xA;- **latitude and longitude**, e.g.&#xA;address: 40.759412, -73.912306\` &#xA;- DMS format&#xA;**- latitude and longitude**, e.g.&#xA;address: &#xA;     latitude: 40.74860&#xA;     longitude: "-73.98566" |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon](#) to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                                                       |
| `isHidden`        | `true` hides the action button, `false` shows the action button. Default setting is `false`.                                                                                                                                                                                                                                                                                                                                       |
| `styles`          | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Examples and code snippets

### Open map action button

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ceR_gXAWqyOYxwwBly0Kx-20250217-110927.gif" size="66" position="center" caption="Open an address on a map" alt="Open an address on a map" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ceR_gXAWqyOYxwwBly0Kx-20250217-110927.gif"}
:::

:::VerticalSplitItem
In this example, a button at the bottom of the screen uses the `action.open-map` to open a modal listing the available map apps on the device. Select your preferred app to navigate to the specified address.
:::
::::

```yaml
title: New York
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: >
            https://images.unsplash.com/photo-1485871981521-5b1fd3805eee
            ?w=800&auto=format&fit=crop&q=60
            &ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8bmV3JTIweW9ya3xlbnwwfHwwfHx8MA%3D%3D

children:
  - type: component.entity-field
  options:
    isMultiline: true
    label: ' '
    value: >
      New York City comprises 5 boroughs sitting where the Hudson River meets the Atlantic Ocean.
      At its core is Manhattan, a densely populated borough that’s among the world’s major commercial,
      financial, and cultural centers.
      Its iconic sites include skyscrapers such as the Empire State Building and sprawling Central Park.
      Broadway theater is staged in neon-lit Times Square.

actions:
  - children:
      # Add the action to open the modal to select the map app on the device,
      # with an address to navigate to. 
      - type: action.open-map
        options:
          title: Go to New York
          address: New York, US
```

### Open map from a list (onPress)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example includes a list of people and places in New York. Tapping the `rightElement` button opens a modal, displaying available map apps on the device. Select your preferred app to navigate to the specified `address`. The addresses are defined in a datasource in various formats, including text strings, latitude, and longitude.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-BWuMO4jXKq6t1f05HH6E6-20250217-115630.gif" size="66" position="center" caption="Open an address from a list" alt="Open an address from a list" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-BWuMO4jXKq6t1f05HH6E6-20250217-115630.gif"}
:::
::::

:::CodeblockTabs
open-map.jigx

```yaml
title: Open map
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1485871981521-5b1fd3805eee?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8bmV3JTIweW9ya3xlbnwwfHwwfHx8MA%3D%3D

children:
  - type: component.list
    options:
      data: =@ctx.datasources.adresses
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          description: =$string(@ctx.current.item.address)
          title: =@ctx.current.item.name
          leftElement: 
            element: icon
            icon: =@ctx.current.item.icon
          # Add a button on the right that can be tapped to open the modal with map options.  
          rightElement: 
            element: button
            title: Navigate
            # Use the onPress event to trigger the action.
            onPress:
              # Configure the action with an address derived from a datasource or static value.
              type: action.open-map
              options:
                address: =@ctx.current.item.address
```

datasource

```yaml
datasources:
  adresses:
    type: datasource.static
    options:
      data:
        - id: 1
          name: John Smith
          address: New York, US
          icon: home-apps-logo
        - id: 2
          name: Empire State Building
          address:
            latitude: 40.74860
            longitude: "-73.98566"
          icon: landmark-empire-state
        - id: 3
          name: The lighthouse
          address: "40.74789, -74.01113"
          icon: lighthouse-bird
```
:::

### Open the map from a secondary action button

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-I5St-RlrY0rIm7zN2AEvP-20250217-120353.gif" size="66" width="1080" height="2167" position="center" caption="Open - map as secondary action" alt="Open - map as secondary action" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-I5St-RlrY0rIm7zN2AEvP-20250217-120353.gif"}
:::

:::VerticalSplitItem
This example describes Central Park in New York. Tapping the ellipsis opens the secondary action button, which is configured with an `icon` displayed to the left of the `title`. When tapped, a modal opens, listing available map apps on the device. Select your preferred app to navigate to the specified `address`, defined by latitude and longitude.
:::
::::

:::CodeblockTabs
open-map-secondary.jigx

```yaml
title: Central Park NY
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: >
            https://images.unsplash.com/photo-1631729779674-1f369e1116b4
            ?w=800&auto=format&fit=crop&q=60
            &ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8Y2VudHJhbCUyMHBhcmt8ZW58MHx8MHx8fDA%3D

children:
  - type: component.entity
    options:
      children:
      - type: component.entity-field
        options:
          isMultiline: true
          label: ' '
          value: >
            A green oasis amidst the towering skyscrapers, 
            Central Park spans 843 acres. 
            This park is a microcosm of New York City itself.
actions:
  - children:
     # Primary action button
      - type: action.go-to
        options:  
          title: Book trip
          linkTo: booking
      # Secondary action button, use the ellipsis to see the button on the screen.
      # The action.open-map opens the modal to select a map app on the device.   
      - type: action.open-map
        options:
          style:
            isSecondary: true
          # Add an icon that displays in the left of the title.  
          icon: end-marker
          # Give the action button a name.
          title: Navigate
          # Specify the address for the action button.
          address: 40.7827902614508, -73.96559413203381
children:
  - type: component.entity
    header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1631729779674-1f369e1116b4?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8Y2VudHJhbCUyMHBhcmt8ZW58MHx8MHx8fDA%3D

       options:
      children:
      - type: component.entity-field
        options:
          isMultiline: true
          label: ' '
          value: A green oasis amidst the towering skyscrapers, Central Park spans 843 acres. This park is a microcosm of New York City itself. 
        
actions:
  - children:
     # Primary action button
      - type: action.go-to
        options:  
          title: Book trip
          linkTo: booking
      # Secondary action button, use the ellipsis to see the button on the screen.
      # The action.open-map opens the modal to select a map app on the device.   
      - type: action.open-map
        options:
          style:
            isSecondary: true
          # Add an icon that displays in the left of the title.  
          icon: end-marker
          # Give the action button a name.
          title: Navigate
          # Specify the address for the action button.
          address: 40.7827902614508, -73.96559413203381
```
:::

### Jig header with open-map action icon

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-aOQBSERQ1zpZdhMkFOba3-20250217-132934.gif" size="66" position="center" caption="Action in jig header" alt="Action in jig header" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-aOQBSERQ1zpZdhMkFOba3-20250217-132934.gif"}
:::

:::VerticalSplitItem
In this example, the `action.open-map` is configured in the `jig.header` action to open a modal listing the available map apps on the device. Select your preferred app to navigate to the specified address. The action is configured with an icon rather than a button.
:::
::::

:::CodeblockTabs
open-map-header.jigx

```yaml
title: New York Financial District
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: >
            https://images.unsplash.com/photo-1532952626554-d0cace1cd3fc
            ?w=900&auto=format&fit=crop&q=60
            &ixlib=rb-4.0.3
            &ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8bmV3JTIweW9yayUyMGZpbmFuY2lhbCUyMGRpc3RyaWN0fGVufDB8fDB8fHww
    actions:
      # Configure a component action on the header to open the modal.
      - type: action.open-map
        options:
          title: Financial District
          # Add an icon that displays in the right of the header. 
          icon: maps-pin
          style:
            # Style the icon.  
            isDanger: true
          # Specify the address for the action icon.  
          address: 1 Wall St, New York, NY 10005, United States
children:
  - type: component.entity
    options:
      children:
      - type: component.entity-field
        options:
          isMultiline: true
          label: ' '
          value: >
            This is the city's buzzing financial heart, home to Wall Street and 
            glittering skyscrapers. Sidewalks bustle during the week and, after work, 
            young professionals fill the restaurants and bars of the South Street Seaport 
            and pedestrian-only Stone Street.
```
:::

