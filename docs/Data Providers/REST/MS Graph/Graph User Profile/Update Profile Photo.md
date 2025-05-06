---
title: Update Profile Photo
slug: rw3S-update-profile-photo
description: Learn how to update your profile photo in Microsoft Graph using an image picker on a Jig and a Jigx REST function. Our document provides step-by-step instructions and includes links to the Graph documentation and Graph explorer for more information. We al
createdAt: Sat Nov 26 2022 06:49:22 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 13:40:09 GMT+0000 (Coordinated Universal Time)
---

## Scenario

Update a user's profile photo in Microsoft Graph using the `media-field` component in a jig to select the photo. A Jigx REST function is used in the `execute-entity` action to make the update.

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
**Resource links:**&#x20;

- <a href="https://learn.microsoft.com/en-us/graph/api/profilephoto-update?view=graph-rest-1.0&tabs=http" target="_blank">Update profilePhoto Graph</a> documentation&#x20;
- <a href="https://developer.microsoft.com/en-us/graph/graph-explorer" target="_blank">Graph explorer</a>
- [Configuring OAuth for MS Graph]()&#x20;

**Required OAuth scope **(least to most privilege)**:**

User.ReadWrite
User.ReadWrite.All
:::

:::VerticalSplitItem
![Update profile photo](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/QYTX-A2BExnkFNhSPRmVx_graph-uploadpic.png "Update profile photo")
:::
::::

## Examples and code snippets

:::hint{type="success"}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator" target="_blank">GitHub</a>.
:::

## General

:::CodeblockTabs
index.jigx

```yaml
name: ms-graph-demonstrator
title: MS Graph Demonstrator
description: A sample solution that uses the Microsoft Graph API. You can deploy and use this solution without any additional configuration.
category: business

tabs:
  home:
    jigId: view-user-jigx
    icon: home-apps-logo
 
onFocus: 
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: user-profile
              function: get-user-profile
              functionParameters:
                accessToken: microsoft.OAuth
            - entity: profile-picture
              function: get-profile-picture
              functionParameters:
                accessToken: microsoft.OAuth 
                userId: =@ctx.user.email   
```
:::

## Functions

MS Graph User function in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/functions/User/update-profile-picture.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
update-profile-picture.jigx

```yaml
provider: DATA_PROVIDER_REST
method: PATCH
url: https://graph.microsoft.com/v1.0/me/photo/$value
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth # Use manage.jigx.com to define credentials for your solution
  Content-Type:
    location: header
    required: true
    type: string
    value: image/jpeg # set the content type of the body
  file:
    location: body
    required: true
    type: image
conversions:
  - property: file
    from: local-uri
    to: buffer

```
:::

## Jigs

MS Graph User jig in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/user/update-profile-picture.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
update-profile-picture.jigx

```yaml
title: Update Profile Picture
description: Update a user's Microsoft Graph profile photo
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://support.content.office.net/en-us/media/f1c4b693-4670-4e7a-8102-bbf1749e83fe.jpg

children:
  - type: component.form
    instanceId: pictureForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.media-field
          instanceId: profilePicture
          options:
            label: New Profile Picture
            mediaType: image
            isMultiple: false
            imageQuality: 80 # optimized photo size with minimal quality loss
            
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Submit Photo
          provider: DATA_PROVIDER_REST
          entity: profile-picture
          function: update-profile-picture
          functionParameters:
            accessToken: microsoft.OAuth
            Content-Type: image/jpeg
            file: =@ctx.components.profilePicture.state.value 
          method: functionCall
          onSuccess: 
            type: action.go-back

```
:::

## See Also

- [Get User Profile & Photo](<./Get User Profile _ Photo.md>)

