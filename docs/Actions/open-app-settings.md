---
title: open-app-settings
slug: ojEV-p
createdAt: Thu Jan 09 2025 07:33:40 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 07:25:59 GMT+0000 (Coordinated Universal Time)
---

Certain features, like location services, require user permissions to function properly. On both iOS and Android operating systems, users are prompted to grant these permissions the first time they are needed. However, if a user denies a permission request, especially on iOS, the app cannot prompt them again directly. For instance, if an iOS device user declines to grant location access when prompted, the system prevents the app from requesting that permission again. The only way to enable it afterward is for the user to manually go into their device’s settings and allow location access for the app.

The open-settings action makes this process easier and more intuitive. The action directs users to the app’s settings page, helping them quickly find and adjust permissions without manually navigating through their device settings.

## Configuration options

Some properties are common to all actions, see [Common action properties](docId\:xwLai--R7dO1e7HzPY8xT)  for a list and their configuration options.

| **Core structure** |                                                                  |
| ------------------ | -------------------------------------------------------------------- |
| `title`            | Provide the action button with a title, for example, Go to settings. |

| **Other options** |                                                                                           |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon]() to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).     |
| `isHidden`        | `true` hides the action button, `false` shows the action button. Default setting is `false`.     |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Examples and code snippets ****

:::::ExpandableHeading
### Open-app settings

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows how to set up the `open-app-settings` action for cases where the app doesn’t have the necessary permissions. Tapping the action button takes you to the device’s settings to grant the required permissions. Afterwards, you can return to the app and continue where you left off. The action is configured to appear when permissions are not granted and to hide once the necessary permissions are in place.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-xQi39F4P1b8CRXDHmRtj_-20250415-085249.gif" size="66" position="center" caption="Open app settings" alt="Open app settings"}
:::
::::
:::::

:::CodeblockTabs
action-open-app-settings.jigx

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

locations

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
:::

