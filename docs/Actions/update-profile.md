# update-profile

This action allows users to update specific information about themselves, which is displayed on the app's profile screen.

This action can be configured within a jig in various ways, such as:
&#x9; An action button
&#x9; A header action link or icon
&#x9; An event, e.g., `onPress`

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="136">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>instanceId</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide the action with an <code>instanceId</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>avatarUrl</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure the property with an expression, datasource, or input to update the user's avatar.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>displayName</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure the property with an expression, datasource, or input to update the user's preferred name, for example, Rob instead of Robert.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>firstName</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure the property with an expression, datasource, or input to update the user's last name (surname).</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>lastName</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure the property with an expression, datasource or input to update the user's name.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Defines the title for the action button, such as Update your details.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Update-profile button in a jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Update Profile details](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NhdCeFqRkSdYEjyKBdnIQ-20250514-093621.png "Update Profile details")
:::

:::VerticalSplitItem
This example demonstrates how a form captures basic personal information and updates the profile screen when the user taps the 'Update' button, which triggers the `action.update-profile`.
:::
::::

:::CodeblockTabs
actions-update-profile.jigx

```yaml
title: Update user profile
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2016/09/15/18/28/update-1672346_640.png
# Use a form to capture the user's profile details.
children:
  - type: component.form
    instanceId: user
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: user-avatar
          options:
            label: Photo
        - type: component.text-field
          instanceId: firstName
          options:
            label: First Name
        - type: component.text-field
          instanceId: LastName
          options:
            label: Last Name    
        - type: component.text-field
          instanceId: displayName
          options:
            label: App Name    
actions:
  - children:
       # Configure the action to save the details captured in the form.
      - type: action.update-profile
        options: 
          lastName: =@ctx.components.LastName.state.value
          firstName: =@ctx.components.firstName.state.value
          displayName: =@ctx.components.displayName.state.value
          avatarUrl: =@ctx.components.user-avatar.state.value
          style:
            # Style the button to use the secondary button color.
           isSecondary: true
          # Provide text that displays on the action button.
          title: Update
```
:::
:::::

:::::ExpandableHeading
### Update-profile in a jig-header link

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how a form captures basic personal information and updates the profile screen when the user taps the *Profile Update* link in the `jig-header`, which triggers the `action.update-profile`.
:::

:::VerticalSplitItem
![Update profile -header link](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-S3VYcMTayd_F6Z6AXR5aq-20250514-094006.png "Update profile - header link ")
:::
::::

:::CodeblockTabs
action-update-profile-header.jigx

```yaml
title: Update user profile
type: jig.default
# In the header add the action to to update the profile screen.
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2018/04/12/18/13/application-3314290_640.png
    actions:
      # Configure the action to save the details captured in the form.
      - type: action.update-profile
        options: 
          title: Profile update
          lastName: =@ctx.components.LastName.state.value
          firstName: =@ctx.components.firstName.state.value
          displayName: =@ctx.components.displayName.state.value
          avatarUrl: =@ctx.components.user-avatar.state.value

children:
  # Use a form to capture the user's profile details.
  - type: component.form
    instanceId: user
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: user-avatar
          options:
            label: Photo
        - type: component.text-field
          instanceId: firstName
          options:
            label: First Name
        - type: component.text-field
          instanceId: LastName
          options:
            label: Last Name    
        - type: component.text-field
          instanceId: displayName
          options:
            label: App Name    
```
:::
:::::

:::::ExpandableHeading
### Update-profile in a jig-header icon

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Update profile - header icon](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-6IbgXLdFBoLHrp0wab0U4-20250514-095340.png "Update profile - header icon")
:::

:::VerticalSplitItem
This example demonstrates how a form captures basic personal information and updates the profile screen when the user taps the *icon* in the `jig-header`, which triggers the `action.update-profile`.
:::
::::

:::CodeblockTabs
action-update-profile-header-icon.jigx

```yaml
title: Update user profile
type: jig.default
# In the header add the action to to update the profile screen.
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2018/04/12/18/13/application-3314290_640.png
   # Configure the action to save the details captured in the form.
    actions:
      - type: action.update-profile
        options: 
          # Add an icon to display in the header that the user can tap to 
          # execute the action.
          icon: upload-bottom
          title: Profile update
          lastName: =@ctx.components.LastName.state.value
          firstName: =@ctx.components.firstName.state.value
          displayName: =@ctx.components.displayName.state.value
          avatarUrl: =@ctx.components.user-avatar.state.value

children:
  # Use a form to capture the user's profile details.
  - type: component.form
    instanceId: user
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: user-avatar
          options:
            label: Photo
        - type: component.text-field
          instanceId: firstName
          options:
            label: First Name
        - type: component.text-field
          instanceId: LastName
          options:
            label: Last Name    
        - type: component.text-field
          instanceId: displayName
          options:
            label: App Name    
```
:::
:::::

:::::ExpandableHeading
### Update-profile with onPress event

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how to use the `onPress` event with `action.update-profile` in a `list-item` to update the first and last names. The names come from a datasource and the avatar from a `form` containing an `avatar` component.
:::

:::VerticalSplitItem
![Update profile - onPress](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-K-J4yCmos33-L-KO8H9cF-20250429-125242.png "Update profile - onPress event")
:::
::::

:::CodeblockTabs
action-update-profile-onpress.jigx

```yaml
title: Update user profile
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2018/04/12/18/13/application-3314289_640.png

children:
  - type: component.list-item
    options:
      title: Today's contractor on site
      subtitle: =(@ctx.datasources.contractors.firstName & ' ' & @ctx.datasources.contractors.lastName)
      rightElement: 
        element: button
        title: Update
        # Use the onPress event to update the profile details.
        # Configure the action to save the photo captured in the form.
        # The first and last names are updated from a datasource.
        onPress: 
          type: action.update-profile
          options:
            firstName: =@ctx.datasources.contractors.firstName
            lastName: =@ctx.datasources.contractors.lastName
            displayName: =@ctx.datasources.contractors.displayName
            avatarUrl: =@ctx.components.user-avatar.state.value
  # Use a form to capture the user's avatar.
  - type: component.form
    instanceId: user
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: user-avatar
          options:
            label: Photo
```

datasource

```yaml
datasources:
  contractors:
    type: datasource.static
    options:
      data:
        - id: 1
          lastName: Russel
          firstName: Robert
          displayName: Rob
```
:::
:::::

