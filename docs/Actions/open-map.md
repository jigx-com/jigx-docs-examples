# open-map

{% columns %}
{% column %}
The open map action lets you tap the on-screen button to open your device's default map app (e.g., Google Maps, Apple Maps, or Waze) with the provided destination address. If multiple map apps are available, they will be listed for you to select one.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/ac-open-map-intro.gif" alt="Open map action" width="188"><figcaption><p>Open map action</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Configuration options

Some properties are common to all components, see [Common component properties](open-map.md) for a list and their configuration options.

<table><thead><tr><th width="151.94140625">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Provide the action with a title, for example, Navigate.</td></tr><tr><td><code>address</code></td><td><p>Address of location - geocode string address to location. Valid formats are:</p><ul><li><strong>address string - city, street</strong>, e.g. `address: 20 W 34th St., New York, NY 10001, USA or in an expression calling a datasource <code>=@ctx.datasources.address</code></li><li><strong>latitude and longitude</strong>, e.g. address: 40.759412, -73.912306`</li><li>DMS format</li><li><strong>latitude and longitude</strong>, e.g. address: latitude: 40.74860 longitude: "-73.98566"</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="160.21484375">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Select an to display when the action is configured as the secondary button or in a <a href="../Components/jig-header.md">header action</a>.</td></tr><tr><td><code>isHidden</code></td><td><code>true</code> hides the action button, <code>false</code> shows the action button. Default setting is <code>false</code>.</td></tr><tr><td><code>styles</code></td><td><p><code>isDanger</code> - Styles the action button in red or your brand's designated danger color.</p><ul><li><code>isDisabled</code> - Displays the action button as greyed out.</li><li><code>isPrimary</code> - Styles the action button in blue or your brand's designated primary color.</li><li><code>isSecondary</code> - Sets the action as a secondary button, accessible via the ellipsis. The <code>icon</code> property can be used when the action button is displayed as a secondary button.</li></ul></td></tr></tbody></table>

## Examples and code snippets

### Open map action button

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-open-map-intro.gif" alt="Open an address on a map" width="188"><figcaption><p>Open an address on a map</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example, a button at the bottom of the screen uses the `action.open-map` to open a modal listing the available map apps on the device. Select your preferred app to navigate to the specified address.

**Example:** See the full code example in GitHub.
{% endcolumn %}
{% endcolumns %}

{% code title="open-map-action" %}
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
  - type: component.entity
    options:
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
{% endcode %}

### Open map from a list (onPress)

{% columns %}
{% column %}
This example includes a list of people and places in New York. Tapping the `rightElement` button opens a modal, displaying available map apps on the device. Select your preferred app to navigate to the specified `address`. The addresses are defined in a datasource in various formats, including text strings, latitude, and longitude.

**Example:** See the full code example in GitHub.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/ac-open-map-list.gif" alt="Open a map from a list" width="188"><figcaption><p>Open a map from a list</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="open-map-onpress.jigx" %}
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
          # Add a button on the right that can be tapped to open the modal with
          # map options.  
          rightElement: 
            element: button
            title: Navigate
            # Use the onPress event to trigger the action.
            onPress:
              # Configure the action with an address derived from a datasource 
              # or static value.
              type: action.open-map
              options:
                address: =@ctx.current.item.address
```
{% endtab %}

{% tab title="datasource" %}
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
{% endtab %}
{% endtabs %}

### Open the map from a secondary action button

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-open-map-secondary.gif" alt="Open - map as secondary action" width="188"><figcaption><p>Open - map as secondary action</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example describes Central Park in New York. Tapping the ellipsis opens the secondary action button, which is configured with an `icon` displayed to the left of the `title`. When tapped, a modal opens, listing available map apps on the device. Select your preferred app to navigate to the specified `address`, defined by latitude and longitude.

**Example:** See the full code example in GitHub.
{% endcolumn %}
{% endcolumns %}

{% code title="open-map-secondary.jigx" %}
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
          uri: https://images.unsplash.com/photo-1631729779674-1f369e1116b4?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8Y2VudHJhbCUyMHBhcmt8ZW58MHx8MHx8fDA%3D
      
children:
  - type: component.entity
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
{% endcode %}

### Jig header with open-map action icon

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-open-map-header.gif" alt="Action in jig header" width="188"><figcaption><p>Action in jig header</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example, the `action.open-map` is configured in the `jig.header` action to open a modal listing the available map apps on the device. Select your preferred app to navigate to the specified address. The action is configured with an icon rather than a button.

**Example:** See the full code example in GitHub.
{% endcolumn %}
{% endcolumns %}

{% code title="open-map-header.jigx" %}
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
{% endcode %}
