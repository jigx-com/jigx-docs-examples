# info-modal

The info-modal is a pop-up window that provides additional information or context without navigating away from the current screen. It is used to display additional information and offer guidance or instructions. The modal appears as a temporary overlay on top of the current screen, dimming the background to focus your attention on the modal content. The Info-modal includes interactive elements like buttons, images, icons, or links.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GT3z8bVI4Thn1WDWMkgPB\_cc-infom-intro.png" size="86" position="center" caption="Info-modal" alt="Info-modal" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GT3z8bVI4Thn1WDWMkgPB\_cc-infom-intro.png" width="800" height="538" darkWidth="800" darkHeight="538"}

### Configuration options

Some properties are common to all components, see [Common component properties](info-modal.md) for a list and their configuration options.

<table><thead><tr><th width="166.40234375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>modal</code></td><td>Modal contains the properties that will determine the button and content in the modal.</td></tr><tr><td><code>instanceId</code></td><td>The unique identifier for the info-modal that can be referenced in other jigs.</td></tr><tr><td><code>title</code></td><td>Provide a short title for display at the top of the info-modal. You can use text, an expression or a datasource to set the title.</td></tr></tbody></table>

<table><thead><tr><th width="163.86328125">Other options</th><th></th></tr></thead><tbody><tr><td><code>buttonText</code></td><td>Give the button a label by providing short text. The button displays as a link. If an action like <code>onConfirm</code> is configured the button displays as a button.</td></tr><tr><td><code>description</code></td><td>Provide the text description or instructions for the user to follow. This creates the content in the info-modal. You can use text, an expression or a datasource. This can have multiple lines.</td></tr><tr><td><code>element</code></td><td>The following elements can be added to the modal: - <code>type</code> - Specify either an <code>icon</code>, <code>image</code>, <code>avatar</code>. - When <code>image</code> is specified a <code>uri</code> is required. - Use <code>color</code> to change the <code>icon</code> color, available colors are positive, negative, primary, warning. The default color is primary if no color is specificed. - When using an <code>avatar</code> you can specifiy <code>text</code> or use a <code>uri</code> to show in the avatar.</td></tr><tr><td><code>icon</code></td><td>Add an icon to the info-modal, for example a dollar icon. The icon apprears on the center of the modal. A list of icons are available. See for more information. This property relates to the action button at the bottom of the screen.</td></tr><tr><td><code>isHidden</code></td><td>When set to <code>true</code> the info-modal (button at the bottom of the screen) is hidden on a jig.</td></tr></tbody></table>

<table><thead><tr><th width="159.22265625">Actions</th><th></th></tr></thead><tbody><tr><td><code>onConfirmed</code></td><td><p>The action is triggered when the button is pressed. Use IntelliSense to see the list of available actions. Action to execute when the info-modal button is pressed.</p><ul><li>If the action is not defined, the info-modal will be closed.</li><li>If defined, the info-modal closes after the action is executed.</li><li>The button will have primary action style.</li></ul></td></tr></tbody></table>

### Considerations

* The info-modal only has one action (button).
* If the action on the button is not defined, the info-modal closes automatically and no action is performed.
* Expressions can be used in the info-modal properties to provide the required values.
* The info-modal can be used in the `onFocus`, `onRefresh`, and `onPress` events.
* The info-modal is available in the default, composite, list and document jigs.
* An info-modal action can be used in an action-list.
* A jig can have multiple info-modals configured.
* In the info-modal the `buttonText` displays as a link, if the `onConfirmed` event is added the link visually changes to a button.
* Consider the [confirm](confirm.md) action, which also provides a modal with two buttons, allowing you to cancel or proceed.

### Examples and code snippets

#### info-modal with avatar

{% columns %}
{% column %}
&#x20;In this example, the info-modal is configured on an action. When the button is pressed the info-modal opens and displays an avatar. The avatar `uri` property is used to set the avatar image. The `buttonText` is configured to close the info-modal.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-avatar.jigx).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VJwrxIQhnivZs1hnS-Glo\_cc-infom-avatar.PNG" size="70" position="center" caption="Info-modal with avatar" alt="Info-modal with avatar" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VJwrxIQhnivZs1hnS-Glo\_cc-infom-avatar.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}
{% endcolumns %}

{% code title="info-modal-avatar.jigx" %}
```yaml
title: info-modal - avatar
description: Tap the button to view the info-modal
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1557683316-973673baf926?q=80&w=1129&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Name
            value: Jane Smith
              
actions:
  - children:
      - type: action.info-modal
        options:
          title: avatar
          modal:
            title: Avatar
            buttonText: Close
            description: This info-modal contains an avatar with avatar image and text
            element: 
              type: avatar
              text: AV
              uri: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
```
{% endcode %}

#### info-modal with icon

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nHMaSdrD4gXN3E5WClJKO\_cc-infom-icon.PNG" size="70" position="center" caption="Info-modal with icon" alt="Info-modal with icon" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nHMaSdrD4gXN3E5WClJKO\_cc-infom-icon.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}&#x20;
{% endcolumn %}

{% column %}
In this example, the info-modal is configured on an action. When the button is pressed the info-modal opens and displays a location icon. The `color` property is set to use the primary color. The `buttonText` is configured to close the info-modal.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-icon.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="info-modal-icon.jigx" %}
```yaml
title: info-modal with icon
description: Tap the button to view the info-modal
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1619468129361-605ebea04b44?q=80&w=1171&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D


children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Address
            value: 24 West Street, Houston, Texas
              
actions:
  - children:
      - type: action.info-modal
        options:
          title: icon
          modal:
            title: Location
            buttonText: Close
            description: This info-modal contains a location icon with color
            element: 
              type: icon
              icon: maps-pin
              color: primary
```
{% endcode %}

#### info-modal with image

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7FLQDKXDKA4e1UCDKLEcx\_cc-infom-image.PNG" size="70" position="center" caption="Info-modal with an image" alt="Info-modal with an image" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7FLQDKXDKA4e1UCDKLEcx\_cc-infom-image.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}

{% column %}
Tapping on the action button opens the info-modal showing an image of Thialand. The image property uses `resizeMode` ensuring it is contained in the modal. The `buttonText` allows you to close the modal.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-image.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="info-modal-image.jigx" %}
```yaml
title: info-modal with image
description: Tap the button to view the info-modal
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1508615121316-fe792af62a63?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Holiday destination
            value: Thailand
              
actions:
  - children:
      - type: action.info-modal
        options:
          title: Image
          modal:
            title: Thailand
            buttonText: Close
            description: Welcome to your holiday destination!
            element: 
              type: image
              resizeMode: contain
              uri: https://images.unsplash.com/photo-1502085671122-2d218cd434e6?q=80&w=1226&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
```
{% endcode %}

#### info-modal in calendar jig

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/42pa6T1c-ZmK3uaq-Fb-Y\_cc-infom-calendar.PNG" size="90" position="center" caption="Info-modal in a calendar jig" alt="Info-modal in a calendar jig" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/42pa6T1c-ZmK3uaq-Fb-Y\_cc-infom-calendar.PNG" width="800" height="389" darkWidth="800" darkHeight="389"}

In this example the info-modal is used four places in the jig:

1. In the `onFocus` event to show what type of calendar it is. The info-modal uses the `element` type `image`. The `buttonText` closes the info-modal.
2. In the `onRefresh` event to notify the user that the calendar is refreshing. The info-modal uses the `title`, and the `buttonText` closes the info-modal.
3. In the `action` to allow the info-modal to inform users that events are subject to change, the `element` uses type `icon` with a `color: negative`.
4. In the `onPress` event to show informaton about the event that has been pressed. The info-modal's `description` property provides a text message to users, the `avatar: uri` provides an image and the `buttonText` allows you close the info-modal.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-calendar.jigx).

{% tabs %}
{% tab title="info-modal-calendar.jigx" %}
```yaml
title: Info Modal in a Calendar
type: jig.calendar
icon: calendar

onFocus: 
  type: action.info-modal
  options:
    modal:
      element: 
        type: image
        uri: https://i.ytimg.com/vi/aU5emeJgi88/maxresdefault.jpg
      title: Global team calendar
      buttonText: View 
    
onRefresh: 
  type: action.info-modal
  options:
    modal:
      title: Calendar is refreshing
      buttonText: Close
            
actions:
  - children:
      - type: action.info-modal
        options:
          title: Events Warning
          modal:
            title: Events listed here are subject to change
            description: Events listed here rely on the input from others and may not have been updated reliably. We are notto be held liable for any changes or inconvenience caused.  
            buttonText: OK
            element: 
              type: icon
              icon: calendar
              color: negative
               
data: =@ctx.datasources.story
item:
  type: component.event
  options:
    title: =@ctx.current.item.title
    description: =@ctx.current.item.description
    from: =@ctx.current.item.from
    to: =@ctx.current.item.to
    onPress: 
      type: action.info-modal
      options:
          modal:
            title: Events and times can change 
            description: Events listed here rely on the input from others and may not have been updated reliably.   
            buttonText: OK
            element: 
              type: avatar
              text: CD
              uri: https://cdn1.iconfinder.com/data/icons/managers-15/488/Untitled-5-512.png
```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  story:
    type: datasource.static
    options:
      data:
        - description: Updated the team on your progress for the week
          from: =$fromMillis($toMillis($now()) + 3600000)
          location: Main Boardroom
          title: Team weekly sync
          to: =$fromMillis($toMillis($now()) + 3600000 + 1800000)
          active: false
        - description: Updated the team on your progress for the week
          from: $fromMillis($toMillis($now()) + 7200000)
          location: break area
          title: Social meal
          to: $fromMillis($toMillis($now()) + 7200000 + 3600000)
          active: false
```
{% endtab %}
{% endtabs %}

#### info-modal in default jig

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/T\_RsT3Q\_vvFf2sJUSbFr4\_cc-infom-default.PNG" size="70" position="center" caption="Info-modal on a default jig" alt="Info-modal on a default jig" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/T\_RsT3Q\_vvFf2sJUSbFr4\_cc-infom-default.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}

{% column %}
This example shows the info-modal when the Submit action button is pressed. The `icon` element property is used with `color: warning`. The description property provides the text content, and the `buttonText` is used for the text on the button. An `onConfirm` event is used to add a `go-back` action to the button. Notice how the button has visually changed from a link to a button. You can add an `action-list` to the `onConfirm` and add an `execute-entity` to submit the data from the form to the data store.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-default.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="info-modal-default.jigx" %}
```yaml
title: Info modal on a default jig
type: jig.default

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.default-form.state.data
    
actions:
  - children: 
      - type: action.info-modal
        options:
          title: Sumbit
          modal:
            title: Verification
            buttonText: Submit
            description: Once you submit this form, your details are verifed with a third-party. A progress mail is sent within a week of submision.
            element: 
              type: icon
              icon: double-exclamation-mark-1-formatting
              color: warning
          onConfirmed: 
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/employees
              method: create
              data:
                employee-photo: =@ctx.components.employee-photo.state.value
                employee-first-name: =@ctx.components.employee-first-name.state.value
                employee-surname: =@ctx.components.employee-surname.state.value
                employee-date-of-birth: =@ctx.components.employee-date-of-birth.state.value
                employee-email: =@ctx.components.employee-email.state.value
                employee-phone-number: =@ctx.components.employee-phone-number.state.value
                employee-position: =@ctx.components.employee-position.state.value
                employee-startWork: =@ctx.components.employee-startWork.state.value
          
children:
  - type: component.form
    instanceId: default-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: employee-photo
          options:
            initialValue: =@ctx.datasources.employee-detail-dynamic[0].photo
            label: Photo
        - type: component.section
          options:
            title: Personal information
            children:
              - type: component.text-field
                instanceId: employee-first-name
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].firstname
                  label: First name
              - type: component.text-field
                instanceId: employee-surname
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].lastname
                  label: Surname
              - type: component.date-picker
                instanceId: employee-date-of-birth
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].birthdate
                  label: Date of birth
              - type: component.email-field
                instanceId: employee-email
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].email
                  label: Email
                  icon: email
              - type: component.number-field
                instanceId: employee-phone-number
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].phone
                  label: Phone number
                  icon: phone
        - type: component.section
          options:
            title: Business information
            children:
              - type: component.text-field
                instanceId: employee-position
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].position
                  label: Position
              - type: component.date-picker
                instanceId: employee-startWork
                options:
                  initialValue: =@ctx.datasources.employee-detail-dynamic[0].employee-startWork
                  label: Date of starting work
```
{% endtab %}

{% tab title="employee-detail-dynamic.jigx" %}
```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - entity: default/employees
  query: |
    SELECT 
      id, 
      '$.firstname', 
      '$.lastname', 
      '$.photo', 
      '$.birthdate', 
      '$.gender', 
      '$.email', 
      '$.phone', 
      '$.street', 
      '$.city', 
      '$.state', 
      '$.country', 
      '$.category', 
      '$.modify',
      '$.position',
      '$.employee-startWork' 
    FROM [default/employees] 
    WHERE '$.category' = "employee-detail"
```
{% endtab %}
{% endtabs %}

#### info-modal in list jig

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gCf59HwaD\_adrk5tU5b\_z\_cc-infom-list2.PNG" size="80" position="center" caption="Info-modal in a list jig" alt="Info-modal in a list jig" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gCf59HwaD\_adrk5tU5b\_z\_cc-infom-list2.PNG" width="800" height="538" darkWidth="800" darkHeight="538"}

In this example the info-modal is used three places in the jig:

1. In the `onRefresh` event to notify the user that the list is refreshing. The info-modal use the `title`, `description` and `buttonText` to closes the info-modal. An `element` type `icon` with `color: warning` shows an icon in the center of the info-modal.
2. In the `action` to allow the info-modal to show a message regarding sales information with an element type of `image`, the `buttonText` allows you to go back to the list.
3. In a `swipeable: left` event to show the customer's details. The info-modal's `description` property provides a text message to users, the `avatar: uri` provides an `avatar` with `text` and the `buttonText` allows you close the info-modal. The `description` containing the info-modal content uses an expression to add content from a datasource.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-list.jigx).

{% tabs %}
{% tab title="info-modal-list.jigx" %}
```yaml
title: Info Modal in a list jig
type: jig.list

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1557683316-973673baf926?q=80&w=1129&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
      
onRefresh: 
  type: action.info-modal
  options:
    modal:
      title: Refreshing
      buttonText: Close
      description: Refreshing the customer list
      element: 
        type: icon
        icon: hourglass
        color: warning

data: =@ctx.datasources.components
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.reason
    color:
      - when: =(@ctx.current.item.result= 'Success' ? true :false)
        color: color2
    progress: =@ctx.current.item.progress
    leftElement: 
      element: checkbox
      value: =(@ctx.current.item.status= 'Finished' ? true :false)
    style:
      isError: =(@ctx.current.item.result= 'Unsuccess' ? true :false)
      isStrikeThrough: =(@ctx.current.item.status= 'Finished' ? true :false)
    rightElement: 
      element: value      
      text: ="$ " & @ctx.current.item.value
    
    swipeable:
      left:
        - label: Details
          icon: people-man-8
          color: primary
          onPress: 
            type: action.info-modal
            options:
              modal:
                title: Customer Details
                buttonText: Close
                description: =(@ctx.current.item.name & '\n' & @ctx.current.item.subtitle & '\n' & '\n$' & @ctx.current.item.value)
                element:
                  type: avatar
                  text: =@ctx.current.item.avatar-text
                  
actions:
  - children:
      - type: action.info-modal
        options:
          title: Sales information
          icon: chart
          modal:
            title: Sales information 
            description: Customer and sales information is subject to change frequently  
            buttonText: Go back
```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  components:
    type: datasource.static
    options:
      data:        
      - name: Belantti
        subtitle: APAC
        label-color: color4
        avatar-text: B
        avatar-uri: https://robohash.org/aloha
        progress: 0.54
        value: 115000
        status: Progress
        result: 
        reason:  
        badge: off             
      - name: Ten Tulip
        subtitle: APAC
        highlight: false
        label-color: color7
        avatar-text: TT
        avatar-uri: 
        progress: 0.6
        value: 107000
        status: Progress  
        result:  
        reason: 
        badge: off  
      - name: Ellesti
        subtitle: LATAM
        label-color: color3
        avatar-text: E
        avatar-uri: https://robohash.org/jigx
        progress: 1
        value: 120000
        status: Finished
        result: Success
        reason:   
        badge: on
      - name: Giga Stride
        subtitle: North America
        label-color: color8
        avatar-text: GS
        avatar-uri: 
        progress: 0.21
        value: 102500  
        status: Progress   
        result: 
        reason:   
        badge: off
      - name: Foot Locker
        subtitle: North America
        label-color: color11
        avatar-text: FL
        avatar-uri: 
        progress: 0.47
        value: 42000
        status: Finished   
        result: Unsuccess
        reason: Stopped Because Of High Price 
        badge: off 
      - name: Ovuga
        subtitle: EMEA
        label-color: color9
        avatar-text: O
        avatar-uri: 
        progress: 0.45
        value: 98000   
        status: Progress  
        result: 
        reason:   
        badge: off
      - name: Boostgo
        subtitle: North America
        label-color: color10
        avatar-text: B
        avatar-uri: 
        progress: 0.8
        value: 56000   
        status: Progress   
        result: 
        reason:   
        badge: off
      - name: Sonic Automotive
        subtitle: EMEA
        label-color: color13
        avatar-text: SA
        avatar-uri: 
        progress: 0.22
        value: 37000   
        status: Progress
        result: 
        reason: 
        badge: off
      - name: Mega Mile
        subtitle: EMEA
        label-color: color5
        avatar-text: MM
        avatar-uri: https://robohash.org/Mega
        progress: 0.78
        value: 154000
        status: Finished
        result: Unsuccess  
        reason: Stopped Because Of High Price
        badge: on   
      - name: Jacobs Engineering Group
        subtitle: EMEA
        label-color: color12
        avatar-text: JE
        avatar-uri: 
        progress: 1
        value: 38500
        status: Finished 
        result: Success  
        reason:   
        badge: off
```
{% endtab %}
{% endtabs %}

#### info-modal in onPress action on a widget

![Info-modal on widget](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x16UEinXJlMDbA6LAMVXp_cc-infom-widget.png)

In this example the info-modal is added to the `onPress` event of the widgets.

1. First widget uses an `icon` with `color`, `title`, `buttonText`, `description` and `onConfirm` event to navigate to another jig.
2. Second widget uses avatar,`title`, `buttonText`, `description` and and `onConfirm` event to navigate to another jig.
3. Third widget uses an `image`, `title`, `buttonText` and `onConfirmed` event to open a url.
4. The fourth widget uses a `title`, `buttonText` and `description`. The `buttonText` closes the modal.

**Example:** See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/info-modal/info-modal-widget.jigx).

{% tabs %}
{% tab title="info-modal-widget.jigx" %}
```yaml
# Main wellness week landing screen configuration.
title: Wellness Week
type: jig.default

children:
  # Hero image section - calming/wellness themed background.
  - type: component.image
    options:
      # Fixed height for hero image.
      height: 300  
      # Scale image to cover entire area.                  
      resizeMode: cover              
      source:
        uri: https://images.unsplash.com/photo-1524901548305-08eeddc35080?w=700&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Nnx8Y2FsbXxlbnwwfHwwfHx8MA%3D%3D

  # Grid layout containing 4 interactive widgets
  - type: component.grid
    options:
      children:
        # Widget 1: Yoga/Wellness Week Information
        - type: component.grid-item
          options:
            # Single grid cell size
            size: 1x1                
            children:
              type: component.jig-widget
              options:
                jigId: info-modal-placeholder
                icon: yoga           
                onPress:
                  type: action.info-modal
                  options:
                    modal:
                      element:
                        type: icon
                        icon: yoga
                        color: warning    
                      title: Wellness Week
                      buttonText: Join
                      description: Center your wellbeing and come join is for a week of yoga
                    # Action when user taps the join button.
                    onConfirmed:
                      type: action.go-to
                      options:
                        linkTo: info-modal-placeholder

        # Widget 2: Venue Information
        - type: component.grid-item
          options:
            size: 1x1
            children:
              type: component.jig-widget
              options:
                jigId: info-modal-placeholder
                icon: people-man-1-geometric    
                onPress:
                  type: action.info-modal
                  options:
                    modal:
                      element:
                        type: avatar
                        text: JS      
                      title: Venue
                      buttonText: Directions
                      description: Wellness week will take place at Jodi's studio in Western Avenue, Seattle
                    # Action when user taps the venue button.
                    onConfirmed:
                      type: action.go-to
                      options:
                        linkTo: info-modal-placeholder

        # Widget 3: Healthy Products Shop
        - type: component.grid-item
          options:
            size: 1x1
            children:
              type: component.jig-widget
              options:
                jigId: info-modal-placeholder
                icon: shop          
                onPress:
                  type: action.info-modal
                  options:
                    modal:
                      element:
                        type: image
                        # Fit image within bounds
                        resizeMode: contain    
                        uri: https://images.unsplash.com/31/RpgvvtYAQeqAIs1knERU_vegetables.jpg?q=80&w=1175&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
                      title: Healthy Products
                      buttonText: Shop
                      description: Enhance your lifestyle with our premium selection of healthy products, now available at our store
                    # Action opens external shopping website
                    onConfirmed:
                      type: action.open-url
                      options:
                        url: https://thrivemarket.com/?utm_source=google&utm_medium=cpc&utm_campaign=Non-Brand_SEM_Diet_Healthy&utm_content=151719993106&utm_term=healthy%20food&device=c&ccode=acq60fogwp&ccode_force=1&gad_source=1&gclid=Cj0KCQjwpNuyBhCuARIsANJqL9ODbLM28MMxGvxJ9gK9ohdecVeLkrldAriwFwYg91JDLUEBMfwvK74aAsv6EALw_wcB

        # Widget 4: About Us Information
        - type: component.grid-item
          options:
            size: 1x1
            children:
              type: component.jig-widget
              options:
                jigId: info-modal-placeholder
                icon: content-browser-edit  
                onPress:
                  type: action.info-modal
                  options:
                    modal:
                      title: About us
                      buttonText: Go Back    
                      description: At our wellness center, we are dedicated to nurturing your mind, body, and spirit through holistic and personalized care
```
{% endtab %}

{% tab title="info-modal-placeholder.jigx" %}
```yaml
title: ' '

type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1622737133809-d95047b9e673?q=80&w=2532&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
          
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Placeholder
```
{% endtab %}
{% endtabs %}
