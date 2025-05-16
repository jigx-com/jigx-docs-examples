# location

The location component enables users to display a location on a map within a jig. It can be configured to appear in different formats, including the standard component layout, the jig header, or fullscreen mode. Additionally, display options can be set up to show the current location with markers or paths.

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Options**                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `address`                     | The actual address of the location.&#xA;Valid formats are: &#xA;- **address string - city, street**, e.g.&#xA; `address: 20 W 34th St., New York, NY 10001, USA`&#xA;or in an expression calling a datasource `=@ctx.datasources.address.street & ',' & @ctx.datasources.address.city & ',' & @ctx.datasources.address.country`&#xA;- **latitude and longitude**, e.g. &#xA;`address: 40.759412, -73.912306`                                                                                                                                                                                                                      |
| `is AnimationDisabled`        | `true` or `false` to determine if map animation is disabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `isFollowUserLocationEnabled` | When enabled, the `viewPoint` will be centred on the user’s real-time location.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `markers`                     | Multiple markers can be configured to display on the map. There is a 10K limit for markers showing on the map.&#xA;For example:&#xA;`-type: component.location
    options:
      markers:
        data:
        -latitude: 40.759412
         longitude: -73.912306
        -latitude: 40.745368
         longitude: -74.057189
        -latitude: 40.76479429122513
         longitude: -73.97429291692742 `<br />You can use an expression to provide the latitude and longitude points from a datasource, for example:&#xA;`markers:
   data: \|       =@ctx.datasources.jobs.{"lng": $number($.lng), "lat": $number($.lat)}` |
| `marker-item`                 | `anchorTo:` - Anchor the marker to a specific point, either `bottom-center` or `center`<br />`radius` - Display a circle around the marker. In the radius you can configure the `color`, `unit` (Default is kilometres)<br />`icon` - Choose an icon for the markers. You can style the icon `color`, `emphasis`, `type`, `shape` and `size`.                                                                                                                                                                                                                                                                                     |
| `paths`                       | Create one path from many points. The first point is the start destination, and the last is the end destination. There is a 10K limit for paths showing on the map.&#xA;for example:&#xA;` -type: component.location
    options:
      paths:
        data:
        -latitude: 40.759412
         longitude: -73.912306
        -latitude: 40.803495
         longitude: -73.950694
      address: =@ctx.datasources.location[0].address`                                                                                                                                                                                        |
| `viewPoint`                   | Controls the visible area of the map, defining what the user sees. It allows control over position, zoom and orientation.&#xA;Options include:&#xA;`centerPosition:` `middle` or `top`                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `zoomLevel`                   | Defines the initial zoom level of the map. Zooming in enlarges the view, revealing finer details, improving readability, and enhancing location precision.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

| **Action**                                             |                                                                                                                                                                                                                                  |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [open-map](./../Actions/open-map.md)                   | The `action.open-map` lets you open your device's default map app (e.g., Google Maps, Apple Maps, or Waze) with the provided destination address. If multiple map apps are available, they will be listed for you to select one. |
| [open-app-settings](./../Actions/open-app-settings.md) | The `action.open-app-settings` can be configured to show when location tracking permission is not granted. Tapping the action opens the device’s settings screen.                                                                |

| **State Configuration**  | **Key**  | **Notes**                               |
| ------------------------ | -------- | --------------------------------------- |
| `=@ctx.component.state.` | location | State is the variable of the component. |

| **System variable Configuration**            | **Key**              | **Notes**                                                                                                                                                          |
| -------------------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `=@ctx.system.locationPermisions.foreground` | isGranted&#xA;status | Determines the status of the permissions and evaluates if permissions are granted. See [System locationPermissions](<./../Expressions/Jigx Variables.md>) example. |
| `=@ctx.system.geolocation.`                  | coords&#xA;timestamp | See [System geolocation](<./../Expressions/Jigx Variables.md>) example.                                                                                            |

## Considerations

- Test the layout of the location component when combining it with other components, as it can cause spacing issues.
- To display a location as a full screen, use the [jig.fullscreen](<./../Jig Types/jig_fullscreen.md>) type with the `component.location`. See the <a href="https://docs.jigx.com/examples/location#autxL" target="_blank">Fullscreen location</a> example down below.

## Examples and code snippets

:::::ExpandableHeading
### Location using address

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-UFZdb7OyH1n4qiLOUrfKR-20250221-065903.png" size="80" position="center" caption="Location from address" alt="Location from address" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-UFZdb7OyH1n4qiLOUrfKR-20250221-065903.png"}
:::

:::VerticalSplitItem
An interactive map displaying the location using the address.

**Examples**:
See the example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-with-address.jigx).
See the example using dynamic data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/dynamic-data/location-with-address-dynamic.jigx).

**Datasource**:
See the full datasource for static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-with-address.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/location.jigx).
:::
::::

:::CodeblockTabs
location (static)

```yaml
- type: component.location
      options:
        viewPoint:
          centerPosition: middle 
          address: 768 5th Ave, New York, US
          zoomLevel: 14 
        # Add a pin to the exact address.  
        markers:
          data: =@ctx.datasources.address
          item:
            type: component.marker-item
            options:
              address: =@ctx.datasources.address.street
              children:
                type: component.icon
                options:
                  color: negative
                  icon: pin-1-map
```

location (dynamic)

```yaml
- type: component.location
      options:
        viewPoint:
          centerPosition: middle 
          address: =@ctx.datasources.location.address-us
          zoomLevel: 14 
        # Add a pin to the exact address.  
        markers:
          data: =@ctx.datasources.location.address-us
          item:
            type: component.marker-item
            options:
              address: =@ctx.datasources.location.address-us
              children:
                type: component.icon
                options:
                  color: negative
                  icon: pin-1-map
```

datasources (dynamic)

```yaml
datasources:
  location:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/location
      query: |
        SELECT
          '$.id',
          '$.address',
          '$.address-us',
          '$.category',  
          '$.lat',
          '$.lng'
        FROM [default/location] WHERE '$.category' = "location"
```

datasources (static)

```yaml
datasources:
  address: 
    type: datasource.static
    options:
      data:
        - street: 768 5th Ave
          city: New York
          country: US
```
:::
:::::

:::::ExpandableHeading
### Location using latitude and longitude

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SNmxyLzQ0Z2t6OnyCEYDv-20250221-075843.png" size="80" position="center" caption="Address - Latitude & Longitude" alt="Address - Latitude & Longitude" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SNmxyLzQ0Z2t6OnyCEYDv-20250221-075843.png"}
:::

:::VerticalSplitItem
In this example a location is shown using the `latitude` and `longitude` coordinates in the address property.
:::
::::

:::CodeblockTabs
location-lat-lng.jigx

```yaml
children:
    - type: component.location
          options:
            viewPoint:
              # Center the address in the middle of the screen.
              centerPosition: middle
              # Specify the address using latitude and longitude.
              latitude: =@ctx.datasources.appointments[0].latitude
              longitude: =@ctx.datasources.appointments[0].longitude
            # Add endpoint marker icon for the address.  
            markers:
              data: =@ctx.datasources.appointments[0]
              item:
                type: component.marker-item
                options:
                  latitude: =@ctx.current.item.latitude
                  longitude: =@ctx.current.item.longitude
                  children:
                    type: component.icon
                    options:
                      color: negative
                      icon: pin-1-map      
```

datasource

```yaml
datasources:
  appointments:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Empire State Building
          latitude: 40.748676182418976
          longitude: -73.98567513213604
          address: 20 W 34th St., New York, NY 10001, United States
          icon: home
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
### Location with multiple markers

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_G08LkK_JYJE7lY18vhAQ-20250221-073344.png" size="80" position="center" caption="Multiple markers" alt="Multiple markers" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_G08LkK_JYJE7lY18vhAQ-20250221-073344.png"}
:::

:::VerticalSplitItem
An interactive map displaying multiple points.

**Examples**:
See the example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-multiple-markers.jigx).

**Datasources**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-multiple-markers.jigx).
:::
::::

:::CodeblockTabs
location-multiple-markers (static)

```yaml
children:
  - type: component.location
    options:
      viewPoint:
        address: |
          =@ctx.datasources.address.street 
          & ',' & @ctx.datasources.address.city
          & ',' & @ctx.datasources.address.country
      # Use a datasource to define the multiple markers.    
      markers:
        data: =@ctx.datasources.points
```

datasources (static)

```yaml
datasources:
 # First datasource with address.
  address: 
    type: datasource.static
    options:
      data:
        - id: 1
          street: 768 5th Ave
          city: New York
          country: US
  # Second datasource for points in latitude and longitude.
  points:
    type: datasource.static
    options:
      data:
        - latitude: 40.759412
          longitude: -73.912306
        - latitude: 40.745368
          longitude: -74.057189
        - latitude: 40.76479429122513
          longitude: -73.97429291692742    
```
:::
:::::

:::::ExpandableHeading
### Location displaying paths

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-HyprtOZYo43vA857u8iYz-20250221-074256.png" size="80" position="center" caption="Location paths" alt="Location paths" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-HyprtOZYo43vA857u8iYz-20250221-074256.png"}
:::

:::VerticalSplitItem
An interactive map displaying a path with three points, a starting point, middle and end point, with a marker-item at each point.

**Examples**:
See the example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-path.jigx).

**Datasources**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/static-data/location-path.jigx).
:::
::::

:::CodeblockTabs
location-path (static-no -animation)

```yaml
- type: component.location
          options:
            viewPoint:
              # Starting address specified.
              centerPosition: middle
              latitude: 40.759412
              longitude: -73.912306
              isAnimationEnabled: false
              zoomLevel: 9
            # Add icon markers for the addresses.
            markers:
              data: =@ctx.datasources.points
              item:
                type: component.marker-item
                options:
                  latitude: =@ctx.current.item.latitude
                  longitude: =@ctx.current.item.longitude
                  children:
                    type: component.icon
                    options: 
                      icon: end-marker  
            # Paths defined in a datasource in latitude and longitude.                 
            paths:
              data: =@ctx.datasources.points            
```

location-path (static- with-animation)

```yaml
children:
   - type: component.location
          options:
            markers:
              data: =@ctx.datasources.points
              item:
                type: component.marker-item
                options:
                  latitude: =@ctx.current.item.latitude
                  longitude: =@ctx.current.item.longitude
                  children:
                    type: component.icon
                    options: 
                      icon: end-marker        
            paths:
              data: =@ctx.datasources.points 
            viewPoint:
              centerPosition: middle
              latitude: 40.759412
              longitude: -73.912306
              isAnimationEnabled: true
              zoomLevel: 9
```

datasources (static)

```yaml
datasources:
   coordinates:
      type: datasource.static
      options:
        data:
          - id: 1
            latitude: 40.769702
            longitude: -74.038241
          - id: 2
            latitude: 40.759412
            longitude: -73.912306
          - id: 3
            latitude: 40.803495
            longitude: -73.950694
```
:::
:::::

:::::ExpandableHeading
### Location radius

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how to add a circular `radius` around the specified location. Determine whether it is in `kilometers` or `miles` and set its size (`value`). Then, select the `color` of the radius.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cDA1fuYtVPJqgPh81VW6l-20250226-085626.png" size="66" position="center" caption="Location with a radius" alt="Location with a radius" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cDA1fuYtVPJqgPh81VW6l-20250226-085626.png"}
:::
::::

:::CodeblockTabs
location-radius.jigx

```yaml
title: Location with radius
type: jig.default

children:
  - type: component.location
    options:
      viewPoint:
        # Starting address specified.
        centerPosition: middle
        latitude: 40.759412
        longitude: -73.912306 
        address: =@ctx.datasources.points
      # Add the marker point that the radius will use as the center point.  
      markers:
        data: =@ctx.datasources.points
        item:
          type: component.marker-item
          options:
            latitude: =@ctx.current.item.latitude
            longitude: =@ctx.current.item.longitude
            # Specify the radius units, size (value) and color.
            radius:
              isEnabled: true
              # The value determines the radius circle, e.g. 4km.
              value: 4
              unit: kilometers
              color: color4
            children:
              type: component.icon
              options:
                icon: end-marker      
```

datasource

```yaml
datasources:
  points:
    type: datasource.static
    options:
      data:
        - latitude: 40.759412
          longitude: -73.912306
```
:::
:::::

::::::ExpandableHeading
### &#x20;Location full screen

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
In this example the `component.location` is used in the `jig.fullscreen` ensuring the map covers the entire jig.

**Examples**:
See the example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/location/dynamic-data/location-fullscreen-dynamic.jigx).

**Datasource**:
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/location.jigx).

:::hint{type="success"}
Using the code below requires data in the database, the *jigx.sample* solution has the data provided for location. You can use the location.csv file in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/csv/location.csv" target="_blank">GitHub</a> and upload it via the [Data](#) configuration in Jigx Management.
:::
::::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-RV6o93L_kcfzE1pfggkwo-20250221-082705.png" size="68" position="center" caption="Fullscreen location" alt="Fullscreen location" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-RV6o93L_kcfzE1pfggkwo-20250221-082705.png"}
:::
:::::

:::CodeblockTabs
location-fullscreen.jigx

```yaml
title: Location fullscreen
type: jig.full-screen

component: 
  type: component.location
  options:
    viewPoint:
      # Center the address in the middle of the screen.
      centerPosition: middle
      # Specify the address using latitude and longitude.
      address: =@ctx.datasources.address[0].street
      # Zoom in to enlarge the view, reveal finer details, improving readability, 
      # and enhance location precision.
      zoomLevel: 14
    # Add endpoint marker icon for the address.   
    markers:
      data: =@ctx.datasources.address[0].street
      item:
        type: component.marker-item
        options:
          address: =@ctx.datasources.address[0].street
          children:
            type: component.icon
            options:
              # Determine the size of the marker icon.
              size: large
              icon: end-marker
```

datasources

```yaml
datasources:
  address: 
    type: datasource.static
    options:
      data:
        - id: 1
          street: 768 5th Ave
          city: New York
          country: US
        - id: 2
          street: 137 W 111th St
          city: New York
          country: US  
```
:::
::::::

:::::ExpandableHeading
### Location as a header

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cQZEvoQcr1J_SDuWosHd7-20250221-091813.png" size="98" position="center" caption="Location in header" alt="Location in header" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cQZEvoQcr1J_SDuWosHd7-20250221-091813.png"}
:::

:::VerticalSplitItem
The location component can be used as a `small` or `medium` size header in a jig. In the screenshot the difference between the set heights is shown.

**Examples:**
See the code samples using static data in GitHub for [small](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-location/jig-header-location-small.jigx) and [medium](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/jig-header/static-data/jig-header-location/jig-header-location-medium.jigx) headers.
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

## See also

- [State](#)

