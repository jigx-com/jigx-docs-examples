---
title: Jigx Variables
slug: y99t-organ
description: Learn about the variables available in expressions for manipulating data in a JigxApp. This comprehensive document covers organization, system, user, and solution variables, including configuration options and helpful examples. Explore code snippets and a
createdAt: Thu Jul 27 2023 13:17:38 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Mar 18 2025 18:38:17 GMT+0000 (Coordinated Universal Time)
---

Jigx has a set of variables that can be used in expressions to manipulate data specific to a  Jigx App, for example, determining the logged-in user, or the Jigx organization and solution.&#x20;

# Organization

The `organization` variable is used to get information about the actual organization in Jigx, such as your Jigxorganization's id.

## Configuration

| **Result** | **Expression**          |
| ---------- | ----------------------- |
| id         | `=@ctx.organization.id` |

## Examples and code snippets 

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/l9Evc2zPxdR6ZYdCJIOcm_img7983iphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/l9Evc2zPxdR6ZYdCJIOcm_img7983iphone13blueportrait.png" size="92" width="1570" height="2932" position="flex-end" caption="Organization expression" alt="Organization expression"}
:::

:::VerticalSplitItem
This example returns the organization's `id` . Each organization configured in [Organization Settings]() in Jigx Managementand will have a unique id.&#x20;
See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/organization.jigx" target="_blank">GitHub</a>.&#x20;

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Organization ID
            value: =@ctx.organization.id
```
:::
::::

# System

The system variable in an expression is used to get information about devices, for example, you can find information about the internet connection of the device, the language preference, the device's timezone and location details. System expressions are configured by `=@ctx.system.` followed by the specific variable name.&#x20;

## Configuration

The supported variables for the system variable are:

| **Variable**             | **Expression**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | **Results**                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| appVersion               | `=@ctx.system.appVersion`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | This variable returns the current version of the installed app, which is useful for troubleshooting, crash tracing, and debugging issues.&#xA;E.g. 1.110.7                                                                                                                                                                                                                                                                       |
| deviceType               | `=@ctx.system.deviceType`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | The variable returns the current user's device type, such as tablet or handset.                                                                                                                                                                                                                                                                                                                                                  |
| geocodes                 | `=@ctx.system.geocodes`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| isOffline                | `=@ctx.system.isOffline`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Boolean                                                                                                                                                                                                                                                                                                                                                                                                                          |
| isOnline                 | `=@ctx.system.isOnline`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Boolean                                                                                                                                                                                                                                                                                                                                                                                                                          |
| isPortrait               | `=@ctx.system.isPortrait`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | The variable is set with a boolean and is used to configure the behavior of components in either portrait or landscape mode.                                                                                                                                                                                                                                                                                                     |
| locale                   | `=@ctx.system.locale`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| location Permissions     | `=@ctx.system.locationPermisions`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `Status` can be:<br />* `granted` : granted: true
* `undetermined` : granted: false&#x20;
* `denied`: granted: false<br />`=@ctx.system.locationPermissions.foreground.status`<br />`isGranted` is determined by the device's location settings for the Jigx app: <br />* Always (`isGranted: true`)
* While using the app (`isGranted: true`)
* Never (`isGranted: false`)
* Ask Next time or when I share (`isGranted: false`) |
| timezone                 | `=@ctx.system.timezone.offset`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Get the information about the device's timezone, it can be:&#xA;-`name`: e.g. Europe/Prague&#xA;-`offset`: e.g. +200                                                                                                                                                                                                                                                                                                             |
| geolocation              | **Accuracy: &#xA;**`=@ctx.system.geolocation.coords.accuracy`**&#xA;Altitude:&#xA;**`=@ctx.system.geolocation.coords.altitude`&#xA;**Altitude Accuracy:** `=@ctx.system.geolocation.coords.altitudeAccuracy`&#xA;**Location - Heading:** `=@ctx.system.geolocation.coords.heading`&#xA;**Location - Latitude:&#xA;**`=@ctx.system.geolocation.coords.latitude`&#xA;**Location - Longitude:**&#xA;`=@ctx.system.geolocation.coords.longitude`&#xA;**Location - Speed:&#xA;**`=@ctx.system.geolocation.coords.speed`&#xA;**Location - Timestamp:&#xA;**`=@ctx.system.geolocation.timestamp`&#xA;**Location - Entire array (All details):**&#xA;`=$string(@ctx.system.geolocation)` |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| isLocationSharingEnabled | `=@ctx.system.isLocationSharingEnabled`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Boolean                                                                                                                                                                                                                                                                                                                                                                                                                          |
| solution                 | `=@ctx.solution.id`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | XXXXXXXX-XXX-XXXX-XXXX-XXXXXXXXXXXX                                                                                                                                                                                                                                                                                                                                                                                              |
| user                     | `=@ctx.user.email`&#xA;or&#xA;`=@ctx.user.id`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | username\@jigx.com&#xA;or&#xA;XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX                                                                                                                                                                                                                                                                                                                                                               |

## Examples and code snippets&#x20;

### System isOffline

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![System expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dozQmeZtycpfLoEgq34Zb_vexno05ey8qanp2ahvm8wimg1073iphone13blueportrait.png "System expression")
:::

::::VerticalSplitItem
With this expression, you can disable the action button to prevent it from being pressed if the device is offline.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx" target="_blank">GitHub</a>.&#x20;

:::CodeblockTabs
isOffline.jigx

```yaml
actions:
  - children:
      - type: action.go-to
        options:
          style:
            isDisabled: =@ctx.system.isOffline = true
          title: Go to action
          linkTo: advanced-expressions
```
:::




::::
:::::

### System timezone

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
&#x20;This example uses `system.timezone` to get the information about the device's timezone, it can be the `name` of the timezone or the `offset`. Use it further to convert date/time using [Date & Time](<./Date _ Time.md>) expressions into the format that you require.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx" target="_blank">GitHub</a>.

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Timezone name
            value: =@ctx.system.timezone.name
        - type: component.entity-field
          options:
            label: Timezone offset
            value: =@ctx.system.timezone.offset
```
:::

:::VerticalSplitItem


![System timezone expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/oANyCp8ANnxLlVQO8SP9t_br9tnyrzt6xxavl6azvoeimg1075iphone13blueportrait.png "System timezone expression")
:::
::::

### System geolocation

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![system geolocation expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Zw09RzF0UJDUm3XaEwrcM_img7975iphone13blueportrait.png "system geolocation expression")


:::

:::VerticalSplitItem
This example shows how you can use `system.geolocation` to get the device's location (details).

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/geolocation.jigx" target="_blank">GitHub</a>.

```yaml
children: 
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: System Location - Accuracy
            value: =@ctx.system.geolocation.coords.accuracy
        - type: component.entity-field
          options:
            label: System Location - Altitude
            value: =@ctx.system.geolocation.coords.altitude
        - type: component.entity-field
          options:
            label: System Location - Altitude Accuracy
            value: =@ctx.system.geolocation.coords.altitudeAccuracy
        - type: component.entity-field
          options:
            label: System Location - Heading
            value: =@ctx.system.geolocation.coords.heading
        - type: component.entity-field
          options:
            label: System Location - Latitude
            value: =@ctx.system.geolocation.coords.latitude
        - type: component.entity-field
          options:
            label: System Location - Longitude
            value: =@ctx.system.geolocation.coords.longitude
        - type: component.entity-field
          options:
            label: System Location - Speed
            value: =@ctx.system.geolocation.coords.speed
        - type: component.entity-field
          options:
            label: System Location - Timestamp
            value: =@ctx.system.geolocation.timestamp
            contentType: time
        - type: component.entity-field
          options:
            label: System Location - Entire array (All details)
            value: =$string(@ctx.system.geolocation)

```
:::
::::

### System locationPermissions

Location tracking is a powerful feature in mobile apps that enables various functionalities, such as navigation, personalized recommendations, and location-based notifications. However, using location data requires explicit permission from users to ensure privacy and compliance with platform guidelines.

This example, uses the device's *privacy and security settings* to display a location or deny access to a location. Change your device's settings for the Jigx App to see the returned permissions.&#x20;

The following `statuses` are returned depending on the device's settings:

- `undetermined`&#x20;
- `granted`&#x20;
- `denied`&#x20;

Evaluating whether or not permission has been granted using `isGranted` returns a boolean.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Jd_CvMmj_mJUaj5oebWRD-20250317-153841.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Jd_CvMmj_mJUaj5oebWRD-20250317-153841.png" size="98" width="3738" height="2466" position="center" caption="System Location Permissions" alt="System Location Permissions"}

:::CodeblockTabs
```yaml
title: Location permissions
description: Use the device's location tracking permissions to show the location or a message. 
type: jig.default

children:
  - type: component.location
    when: =@ctx.system.locationPermissions.foreground.status = 'granted'
    # status: undetermined = isGranted:false
    # status: granted = isGranted: true
    # status: denied = isGranted:false
    options:
      viewPoint:
        address: =@ctx.datasources.locations[2].address
        zoomLevel: 12
      markers:
        data: =@ctx.datasources.locations[2]
        item:
          type: component.marker-item
          options:
          # Set a small radius around the location address in kilometers. 
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
  # Retrieves the location permission settings configured for Jigx apps on the device.          
  - type: component.entity
    options:
      children: 
        - type: component.entity-field
          options:
            label: Permission Status
            value: =@ctx.system.locationPermissions.foreground.status
  - type: component.entity
    options:
      children: 
       # Check whether the Jigx app has been granted location permissions on the device.  
        - type: component.entity-field
          options:
            label: Permission granted?
            value: =@ctx.system.locationPermissions.foreground.isGranted   
# If the permissions are not granted then show a placeholder message.                          
placeholders:
  - title: You need to grant permissions in the device settings.
    when: =@ctx.system.locationPermissions.foreground.isGranted = false
    icon: missing-data
```

locations (datasource)

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
        # Change the address, latitude & longitude to be closer to your location.
        # The address shown below was for demonstration purposes.  
        - id: 3
          address: Sun Valley Mall, Cnr Ou Kaaps Weg & Buller Louw Blvd, Sunnydale, Cape Town
          latitude: -34.12183827658212
          longitude: 18.38924840500718 
          icon: music-genre-dumbbell
```
:::

### System appVersion & deviceType

Device information is important to identify the types of devices and the app version users   are using. This is useful for troubleshooting issues and diagnosing app crashes. The details can be retrieved in multiple ways when using the system variable, such as on the app screen or when connected to Jigx dev tools in Jigx Builder.  &#x20;

![Jigx dev tools for debugging](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-G4rE3IMKVCIOs3HqHfnwf-20250225-112949.png "Jigx dev tools for debugging")

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: AppVersion
            value: =@ctx.system.appVersion
        - type: component.entity-field
          options:
            label: Device Type
            value: =@ctx.system.deviceType 
```

### System isLocationSharingEnabled

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
See the example using dynamic data in GitHub. &#x20;

```yaml
  onFinish: 
            type: action.confirm
            options:
              isConfirmedAutomatically: false
              onConfirmed: 
                type: action.go-back
              modal:
                title: Enjoy your pizza
      # Add the ability to stop sharing your location 
      - type: action.stop-location-sharing
        when: =@ctx.system.isLocationSharingEnabled
        options:
          title: Stop sharing
```
:::

:::VerticalSplitItem
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/6PYMLSP1mvgXAyOVdRTl3_systemexpress.png)
:::
::::

# User

## Examples and code snippets&#x20;

The *user* is used to get information about the logged-in user, for example, name, and email.

## Configuration

| **Result** | **Expression**           |
| ---------- | ------------------------ |
| Name       | `=@ctx.user.displayName` |
| Email      | `=@ctx.user.email`       |
| id         | `=@ctx.user.id`          |

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![User expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YjBuEhcG9PqMOYLrSR02f_img7979iphone13blueportrait.png "User expression")
:::

::::VerticalSplitItem
See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/user.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
user.jigx

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: User Display Name
            value: =@ctx.user.displayName
        - type: component.entity-field
          options:
            label: User Email
            value: =@ctx.user.email
        - type: component.entity-field
          options:
            label: User Id
            value: =@ctx.user.id
```
:::
::::
:::::

# Solution

The `solution` variable is used to get information about the specific Jigx solution, for example, name, and id. [Custom variables]() can be set in [Solution Settings]() in Jigx Management, and the variable value referenced in the solution expression.

## Configuration

| **Result**     | **Expression**                                |
| -------------- | --------------------------------------------- |
| name           | `=@ctx.solution.name`                         |
| id             | `=@ctx.solution.id`                           |
| variable value | `=@ctx.solution.settings.custom.variableName` |

## Examples and code snippets&#x20;

### Solution Id and name

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Solution expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/oViCGP9PqleD7r5MC51mk_img7981iphone13blueportrait.png "Solution expression")
:::

:::VerticalSplitItem
This example shows how to get the solution's id and name using the `solution` variable.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/solution.jigx" target="_blank">Github</a>.&#x20;

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Solution ID
            value: =@ctx.solution.id
        - type: component.entity-field
          options:
            label: Solution Name
            value: =@ctx.solution.name
```
:::
::::

### Solution settings - custom variable

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
![Setting Custom Variables](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-xXC42Y_pvmCKo34wfapvo-20240819-091011.png "Setting Custom Variables")
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-L6LdkmoDZq3iZw0CsGaXk-20240819-130652.PNG" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-L6LdkmoDZq3iZw0CsGaXk-20240819-130652.PNG" size="86" width="1240" height="2500" position="center" caption="Showing variable value" alt="Showing variable value"}
:::
::::

:::CodeblockTabs
YAML

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            rightIcon: cursor-click-computers
            label: Click to view the report in SharePoint
# Reference the custom variable set in Management in the expression            
            value: =@ctx.solution.settings.custom.SharePoint_URL
```
:::

