---
title: Get User Profile & Photo
slug: Vusj-get-user-profile
createdAt: Fri Nov 25 2022 19:06:31 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 13:35:58 GMT+0000 (Coordinated Universal Time)
---

# Get User Profile & Photo

{% columns %}
{% column width="50%" %}
### Scenario

Gets a user's profile and photo in Microsoft Graph using Jigx functions, and displays the profile and photo on a jig using the `image` and `entity` component.

**Resource links:**

1. [Profile Photo Graph](https://learn.microsoft.com/en-us/graph/api/resources/profilephoto?view=graph-rest-1.0) documentation
2. [Graph Get a User](https://learn.microsoft.com/en-us/graph/api/user-get?view=graph-rest-1.0\&tabs=http) documentation
3. [Graph explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
4. [Configuring OAuth for MS Graph](https://docs.jigx.com/configuring-oauth-for-ms-graph)

**Required OAuth scope** (least to most privilege):\
User.Read User.ReadWrite User.ReadBasic.All User.Read.All User.ReadWrite.All Directory.Read.All Directory.ReadWrite.All
{% endcolumn %}

{% column width="50%" %}
<img src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dntkn6sc5sSZFqfHF7IGH_graph-user-profile.png" alt="User Profile" data-size="original">


{% endcolumn %}
{% endcolumns %}

### Examples and code snippets

{% hint style="success" %}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator).
{% endhint %}

### General

{% tabs %}
{% tab title="index.jigx" %}
```yaml
name: ms-graph-demonstrator
title: MS Graph Demonstrator
description: A solution using Microsoft Graph APIs .
category: business

onLoad:
  type: action.execute-action
  options:
    action: full-sync

onRefresh:
  type: action.execute-action
  options:
    action: full-sync

expressions:
  today: =$substring($now(), 0, 10)
  todayStart: =$toMillis($today)
  weekdayStr: =$floor($todayStart/86400000)
  weekdayNum: =($weekdayStr + 4) % 7
  startOfWeek: =$todayStart - ($weekdayNum * 86400000)
  thisWeek: =$startOfWeek + 604800000
  next7: =$number($todayStart) + 604800000

tabs:
  home:
    jigId: home
    icon: home
```
{% endtab %}

{% tab title="home.jigx" %}
```yaml
mtitle: Home
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: 2x2
      children:
        type: component.jig-widget
        options:
          jigId: view-user-jigx
          widgetId: profileImage
  - type: component.grid-item
    options:
      size: 2x2
      children:
        type: component.jig-widget
        options:
          jigId: calendar-summary
          widgetId: nextDays
  - type: component.grid-item
    when: =$boolean(@ctx.datasources.next-meeting.locationAddress)
    options:
      size: 4x2
      children:
        type: component.jig-widget
        options:
          jigId: next-meeting
          widgetId: meeting-location
  - type: component.grid-item
    options:
      size: 2x2
      children:
        type: component.jig-widget
        options:
          jigId: list-email-messages
  - type: component.grid-item
    options:
      size: 2x2
      children:
        type: component.jig-widget
        options:
          jigId: list-task-lists
          widgetId: taskList
  - type: component.grid-item
    options:
      size: 4x2
      children:
        type: component.jig-widget
        options:
          jigId: items-trending
          widgetId: trending
```
{% endtab %}
{% endtabs %}

### Functions

MS Graph User functions in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator/functions/User).

{% tabs %}
{% tab title="get-user-profile.jigx" %}
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
    # Use manage.jigx.com to define credentials for your solution.
    value: microsoft.OAuth 

```
{% endtab %}

{% tab title="get-profile-picture.jigx" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
# pdf indicates a generic binary type.
format: pdf 
url: https://graph.microsoft.com/v1.0/me/photo/$value
# Add the email input to the output to identify image later in select
outputTransform: $.{"data":$.data,"userId":$.inputs.userId.value} 

parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution
    value: microsoft.OAuth 
  userId:
    type: string
    location: path
    required: true
conversions:
  - property: data
    from: base64
    to: local-uri
```
{% endtab %}
{% endtabs %}

### Jigs

MS Graph User jig in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-MS-Graph-demonstrator/jigs/user/view-user-jigx.jigx).

{% code title="view-user-jigx.jigx" %}
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
        parameters:
          accessToken: microsoft.OAuth
      - entity: profile-picture
        function: get-profile-picture
        parameters:
          accessToken: microsoft.OAuth
          userId: =@ctx.user.email
      - entity: user-emails
        function: get-user-emails-addresses
        parameters:
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
  profileAvatar:
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

  profileImage:
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
{% endcode %}

### See Also

* [Update Profile Photo](<Update Profile Photo.md>)
