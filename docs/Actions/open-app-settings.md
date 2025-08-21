# open-app-settings

Certain features, like location services, require user permissions to function properly. On both iOS and Android operating systems, users are prompted to grant these permissions the first time they are needed. However, if a user denies a permission request, especially on iOS, the app cannot prompt them again directly. For instance, if an iOS device user declines to grant location access when prompted, the system prevents the app from requesting that permission again. The only way to enable it afterward is for the user to manually go into their device’s settings and allow location access for the app.

The open-settings action makes this process easier and more intuitive. The action directs users to the app’s settings page, helping them quickly find and adjust permissions without manually navigating through their device settings.

## Configuration options

Some properties are common to all actions, see [Common action properties](open-app-settings.md) for a list and their configuration options.

<table><thead><tr><th width="149.59765625">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Provide the action button with a title, for example, Go to settings.</td></tr></tbody></table>

<table><thead><tr><th width="156.88671875">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Select an to display when the action is configured as the secondary button or in a <a href="../Components/jig-header.md">header action</a>.</td></tr><tr><td><code>isHidden</code></td><td><code>true</code> hides the action button, <code>false</code> shows the action button. Default setting is <code>false</code>.</td></tr><tr><td><code>style</code></td><td><p><code>isDanger</code> - Styles the action button in red or your brand's designated danger color.</p><ul><li><code>isDisabled</code> - Displays the action button as greyed out.</li><li><code>isPrimary</code> - Styles the action button in blue or your brand's designated primary color.</li><li><code>isSecondary</code> - Sets the action as a secondary button, accessible via the ellipsis. The <code>icon</code> property can be used when the action button is displayed as a secondary button.</li></ul></td></tr></tbody></table>

## Examples and code snippets

### Open-app settings

{% columns %}
{% column %}
This example shows how to set up the `open-app-settings` action for cases where the app doesn’t have the necessary permissions. Tapping the action button takes you to the device’s settings to grant the required permissions. Afterwards, you can return to the app and continue where you left off. The action is configured to appear when permissions are not granted and to hide once the necessary permissions are in place.
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-xQi39F4P1b8CRXDHmRtj\_-20250415-085249.gif" size="66" position="center" caption="Open app settings" alt="Open app settings" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-xQi39F4P1b8CRXDHmRtj\_-20250415-085249.gif" width="681" height="1377" darkWidth="681" darkHeight="1377"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="action-open-app-settings.jigx" %}
```yaml
title: Open app settings
description: Use the device's location tracking permissions to show the location or a message. 
type: jig.default

children:
  - type: component.location
    instanceId: geofencing
    when: =@ctx.system.locationPermissions.foreground.status = 'granted'
    options:
      viewPoint:
        address: =@ctx.datasources.locations[2].address
        zoomLevel: 12
        isFollowUserLocationEnabled: true
      markers:
        data: =@ctx.datasources.locations[2]
        item:
          type: component.marker-item
          options:
            radius:
              isEnabled: true
              value: 0.2
              unit: kilometers
              color: color12
            latitude: =@ctx.current.item.latitude
            longitude: =@ctx.current.item.longitude
            children:
              type: component.icon
              options:
                icon: =@ctx.current.item.icon
                
  - type: component.entity
    options:
      children: 
        - type: component.entity-field
          options:
            label: Permission Status
            value: =@ctx.system.locationPermissions.foreground.status 
        - type: component.entity-field
          options:
            label: Permission granted?
            value: =@ctx.system.locationPermissions.foreground.isGranted   
                       
placeholders:
  - title: You need to grant permissions in the device settings. 
    when: =@ctx.system.locationPermissions.foreground.isGranted = false
    icon: missing-data
# Add an action to open the device’s app settings,
# allowing the user to grant location permissions.
actions:
  - numberOfVisibleActions: 1
    children:
      - type: action.open-app-settings
        # Use the when property,
        # to execute the action if permissions are not granted.
        when: =@ctx.system.locationPermissions.foreground.isGranted = false
        options:
         # Hide the action when permissions are granted.
         isHidden: =@ctx.system.locationPermissions.foreground.isGranted = true
         title: Go to settings
```
{% endtab %}

{% tab title="locations" %}
```yaml
datasources:
  locations: 
    type: datasource.static
    options:
      data:
        - id: 1
          address: 768 5th Ave, New York, US 
          street: 768 5th Ave
          city: New York
          country: US
          latitude: 40.76482679513891
          longitude: -73.97432510322122 
          icon: style-two-pin-marker
        - id: 2
          address: 15 Harmony Estate Road, sunnydale, Cape Town, South Africa
          city: Cape Town
          country: South Africa  
          latitude: -34.11757706324835
          longitude: 18.387357196610385 
          icon: end-marker
        - id: 3
          address: Sun Valley Mall, Cnr Ou Kaaps Weg & Buller Louw Blvd, Sunnydale, Cape Town
          latitude: -34.12183827658212
          longitude: 18.38924840500718 
          icon: end-marker
```
{% endtab %}
{% endtabs %}
