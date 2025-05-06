---
title: Get User Profile & Photo
slug: Vusj-get-user-profile
description: Learn how to retrieve a user's profile in Microsoft Graph using Jigx function and display it on a jig entity control. This document includes code snippets, Graph documentation links, and Graph explorer references. Explore the detailed Jigx code for settin
createdAt: Fri Nov 25 2022 19:06:31 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 13:35:58 GMT+0000 (Coordinated Universal Time)
---

## Scenario

Gets a user's profile and photo in Microsoft Graph using Jigx functions, and displays the profile and photo on a jig using the `image` and `entity` component.

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
**Resource links:**&#x20;

1. <a href="https://learn.microsoft.com/en-us/graph/api/resources/profilephoto?view=graph-rest-1.0" target="_blank">Profile Photo Graph</a> documentation
2. <a href="https://learn.microsoft.com/en-us/graph/api/user-get?view=graph-rest-1.0&tabs=http" target="_blank">Graph Get a User</a> documentation
3. <a href="https://developer.microsoft.com/en-us/graph/graph-explorer" target="_blank">Graph explorer</a>&#x20;
4. [Configuring OAuth for MS Graph]()&#x20;

**Required OAuth scope **(least to most privilege)**:**

User.Read
User.ReadWrite
User.ReadBasic.All
User.Read.All
User.ReadWrite.All
Directory.Read.All
Directory.ReadWrite.All
:::

:::VerticalSplitItem
![User Profile](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dntkn6sc5sSZFqfHF7IGH_graph-user-profile.png "User Profile")
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
            - entity: user-emails
              function: get-user-emails-addresses
              functionParameters:
                accessToken: microsoft.OAuth                   

```
:::

## Functions

MS Graph User functions in <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator/functions/User" target="_blank">GitHub</a>.

:::CodeblockTabs
get-user-profile.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://graph.microsoft.com/v1.0/me
useLocalCall: true
outputTransform: $
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth #Use manage.jigx.com to define credentials for your solution
    
```

get-profile-picture.jigx

```yaml
provider: DATA_PROVIDER_REST
method: GET
format: pdf #pdf indicates a generic binary type
url: https://graph.microsoft.com/v1.0/me/photo/$value
outputTransform: $.{"data":$.data,"userId":$.inputs.userId.value} #add the email input to the output to identify image later in select

parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: microsoft.OAuth #Use manage.jigx.com to define credentials for your solution
  userId:
    type: string
    location: path
    required: true
conversions:
  - property: data
    from: base64
    to: local-uri
```
:::

## Jigs

MS Graph User jig in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/user/view-user-jigx.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
view-user-jigx.jigx

```yaml
title: View User Profile
description: Displays a user's profile information from Microsoft Graph
type: jig.default
icon: person

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://support.content.office.net/en-us/media/f1c4b693-4670-4e7a-8102-bbf1749e83fe.jpg
      
onRefresh: 
  type: action.sync-entities
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
      - entity: user-emails
        function: get-user-emails-addresses
        functionParameters:
          accessToken: microsoft.OAuth
      
datasources:
  userProfile: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: user-profile
      query: |
        SELECT id, 
        '$.displayName', 
        '$.givenName', 
        '$.jobTitle', 
        '$.mail',
        '$.mobilePhone',
        '$.officeLocation',
        '$.surname',
        '$.userPrincipalName',
        '$.businessPhones',
        '$.id' 
        FROM [user-profile]
      isDocument: true
      
  profilePhoto:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: profile-picture
      query: SELECT id, '$.userId', '$.data' FROM [profile-picture]
      isDocument: true
      
  userEmails:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: user-emails
      query: SELECT id, '$.address', '$.type', '$.allowedAudiences' FROM [user-emails]

children:
  - type: component.image
    options:
      source:
        uri: =@ctx.datasources.profilePhoto.data         
      height: 200
      resizeMode: contain
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.userProfile.mail
            contentType: email
        - type: component.entity-field
          options:
            label: User Principal Name
            value: =@ctx.datasources.userProfile.userPrincipalName
        - type: component.entity-field
          options:
            label: Display Name
            value: =@ctx.datasources.userProfile.displayName
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Given Name
                  value: =@ctx.datasources.userProfile.givenName
              - type: component.entity-field
                options:
                  label: Surname
                  value: =@ctx.datasources.userProfile.surname
        - type: component.field-row
          options:
            children:
            - type: component.entity-field
              options:
                label: Job Title
                value: =@ctx.datasources.userProfile.jobTitle
            - type: component.entity-field
              options:
                label: Mobile Phone
                value: =@ctx.datasources.userProfile.mobilePhone
        - type: component.entity-field
          options:
            label: Office Location
            value: =@ctx.datasources.userProfile.officeLocation
  - type: component.section
    options:
      title: Email Addresses
      children:
        - type: component.list
          options:
            data: =@ctx.datasources.userEmails
            maximumItemsToRender: 8
            item: 
              type: component.list-item
              options:
                divider: solid
                leftElement: 
                  element: icon
                  icon: email
                title: =@ctx.current.item.address
                subtitle: |
                  ="Type: " & @ctx.current.item.type
                description: |
                  ="Allowed Audiences: " & @ctx.current.item.allowedAudiences               

actions:
  - children:
      - type: action.go-to
        options:
          title: Update Profile Picture
          linkTo: update-profile-picture
            
widgets:
  "2x4": 
    type: widget.group
    options:
      children:
        - type: widget.avatar
          options:
            text: "Your Profile"
            uri: =@ctx.datasources.profilePhoto.data            
            bottom:
              type: component.titles
              options:
                align: center
                title: =@ctx.datasources.userProfile.displayName
                subtitle: =@ctx.datasources.userProfile.jobTitle
                
  "2x2": 
    type: widget.image
    options:
      isContentOverlaid: true
      source:
        uri: =@ctx.datasources.profilePhoto.data
      bottom: 
        type: component.titles
        options:
          title: =@ctx.datasources.userProfile.displayName
          subtitle: =@ctx.datasources.userProfile.jobTitle
        
```
:::

## See Also

- [Update Profile Photo](<./Update Profile Photo.md>)

