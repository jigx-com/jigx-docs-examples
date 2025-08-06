# Jigx Variables

Jigx has a set of variables that can be used in expressions to manipulate data specific to a  Jigx App, for example, determining the logged-in user, or the Jigx organization and solution.

# Organization

The `organization` variable is used to get information about the actual organization in Jigx, such as your Jigx organization's id.

## Configuration

| **Result** | **Expression**          |
| ---------- | ----------------------- |
| id         | `=@ctx.organization.id` |

## Examples and code snippets

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/l9Evc2zPxdR6ZYdCJIOcm_img7983iphone13blueportrait.png" size="92" position="flex-end" caption="Organization expression" alt="Organization expression" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/l9Evc2zPxdR6ZYdCJIOcm_img7983iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example returns the organization's `id` . Each organization configured in [Organization Settings]() in Jigx Managementand will have a unique id.
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/organization.jigx).

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

The system variable in an expression is used to get information about devices, for example, you can find information about the internet connection of the device, the language preference, the device's timezone and location details. System expressions are configured by `=@ctx.system.` followed by the specific variable name.

## Configuration

The supported variables for the system variable are:

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="140,270">
  <tr>
    <td selected="false" align="left">
      <p><strong>Variable</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Expression</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Results</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>appVersion</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.appVersion</code></p>
    </td>
    <td selected="false" align="left">
      <p>This variable returns the current version of the installed app, which is useful for troubleshooting, crash tracing, and debugging issues.
      E.g. 1.110.7</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>deviceType</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.deviceType</code></p>
    </td>
    <td selected="false" align="left">
      <p>The variable returns the current user's device type, such as tablet or handset.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>geocodes</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.geocodes</code></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>isOffline</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.isOffline</code></p>
    </td>
    <td selected="false" align="left">
      <p>Boolean</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>isOnline</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.isOnline</code></p>
    </td>
    <td selected="false" align="left">
      <p>Boolean</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>isPortrait</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.isPortrait</code></p>
    </td>
    <td selected="false" align="left">
      <p>The variable is set with a boolean and is used to configure the behavior of components in either portrait or landscape mode.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>locale</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.locale</code></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>user</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.user.email</code>
      or
      <code>=@ctx.user.id</code></p>
    </td>
    <td selected="false" align="left">
      <p>or
      XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>isLocationSharingEnabled</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.isLocationSharingEnabled</code></p>
    </td>
    <td selected="false" align="left">
      <p>Boolean</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>solution</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.id</code></p>
    </td>
    <td selected="false" align="left">
      <p>XXXXXXXX-XXX-XXXX-XXXX-XXXXXXXXXXXX</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>timezone</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.system.timezone.offset</code></p>
    </td>
    <td selected="false" align="left">
      <p>Get the information about the device's timezone, it can be:
      -<code>name</code>: e.g. Europe/Prague
      -<code>offset</code>: e.g. +200</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>geolocation</p>
    </td>
    <td selected="false" align="left">
    </td>
    <td selected="false" align="left">
      <p>**Accuracy:
      <strong><code>=@ctx.system.geolocation.coords.accuracy</code></strong>
      Altitude:
      **<code>=@ctx.system.geolocation.coords.altitude</code>
      <strong>Altitude Accuracy:</strong> <code>=@ctx.system.geolocation.coords.altitudeAccuracy</code>
      <strong>Location - Heading:</strong> <code>=@ctx.system.geolocation.coords.heading</code>
      **Location - Latitude:
      **<code>=@ctx.system.geolocation.coords.latitude</code>
      <strong>Location - Longitude:</strong>
      <code>=@ctx.system.geolocation.coords.longitude</code>
      **Location - Speed:
      **<code>=@ctx.system.geolocation.coords.speed</code>
      **Location - Timestamp:
      **<code>=@ctx.system.geolocation.timestamp</code>
      <strong>Location - Entire array (All details):</strong>
      <code>=$string(@ctx.system.geolocation)</code></p>
    </td>
  </tr>
</table>

## Examples and code snippets

### System isOffline

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![System expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dozQmeZtycpfLoEgq34Zb_vexno05ey8qanp2ahvm8wimg1073iphone13blueportrait.png "System expression")
:::

::::VerticalSplitItem
With this expression, you can disable the action button to prevent it from being pressed if the device is offline.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx)

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
This example uses `system.timezone` to get the information about the device's timezone, it can be the `name` of the timezone or the `offset`. Use it further to convert date/time using [Date & Time](<./Date _ Time.md>) expressions into the format that you require.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).

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

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/geolocation.jigx).
:::
::::

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

### System appVersion & deviceType

Device information is important to identify the types of devices and the app version users are using. This is useful for troubleshooting issues and diagnosing app crashes. The details can be retrieved in multiple ways when using the system variable, such as on the app screen or when connected to Jigx dev tools in Jigx Builder.

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
See the example using dynamic data in GitHub.

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

## Examples and code snippets

The *user* is used to get information about the logged-in user, for example, name, and email.

## Configuration

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="126">
  <tr>
    <td selected="false" align="left">
      <p><strong>Result</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Expression</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Name</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.user.displayName</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Email</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.user.email</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>id</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.user.id</code></p>
    </td>
  </tr>
</table>

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![User expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YjBuEhcG9PqMOYLrSR02f_img7979iphone13blueportrait.png "User expression")
:::

::::VerticalSplitItem
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/user.jigx).

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

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Result</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Expression</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>name</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.name</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>id</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.id</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>variable value</p>
    </td>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.settings.custom.variableName</code></p>
    </td>
  </tr>
</table>

## Examples and code snippets

### Solution Id and name

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Solution expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/oViCGP9PqleD7r5MC51mk_img7981iphone13blueportrait.png "Solution expression")
:::

:::VerticalSplitItem
This example shows how to get the solution's id and name using the `solution` variable.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/solution.jigx)

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
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-L6LdkmoDZq3iZw0CsGaXk-20240819-130652.PNG" size="86" position="center" caption="Showing variable value" alt="Showing variable value" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-L6LdkmoDZq3iZw0CsGaXk-20240819-130652.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"}
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

