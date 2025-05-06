---
title: go-back
slug: LX00-go-back
description: Learn how to use the go-back action in Jigx to enable users to easily navigate back to the previous page. This comprehensive document covers multiple setup options, including separate action, swipeable action, rightElement in the list, and associated acti
createdAt: Thu Jun 09 2022 18:22:53 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Nov 04 2024 09:47:02 GMT+0000 (Coordinated Universal Time)
---

This action is used to return to the previous page. Most jigs include this action automatically as an arrow to the left of the title of the jig. This action can be used in a list of actions, such as swipeable and rightElement, or used together with another action, where go-back is called after the main action and returns the user to the previous page.

## ****Configuration options****

A go-back action can be set up in various ways:

1. As a separate action or in the action list
2. As a swipeable action in the left or right direction
3. As rightElement in the list
4. As an associated action in the action list

:::hint{type="info"}
A go-back action associated with another action under onSuccess can only be used with dynamic data.
:::

## Examples and code snippets ****

:::::ExpandableHeading
### go-back as an action&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1BxcmGrBKayAJDjL1mdFT_qfq8vyqssxkg7hk1329ugo-backiphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1BxcmGrBKayAJDjL1mdFT_qfq8vyqssxkg7hk1329ugo-backiphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption="go-back as an action" alt="go-back as an action"}
:::

:::VerticalSplitItem
The simplest example of a go-back action is to use it as a separate action. When configured, a button will appear at the bottom which will return us to the previous page when pressed. In this case, the use of the function is unnecessary because as we can see in the screenshot there is an arrow to the left in the upper left corner. This means that this jig already has a go-back action automatically in it and the arrow has the same function as the "Go back" button below.

**Examples:**

See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-action/go-back-action.jigx" target="_blank">GitHub</a>.
See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-action/go-back-action-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
go-back-action.jigx

```yaml
actions:
  - children:
      - type: action.go-back
        options:
          title: Go back
```
:::
:::::

:::::ExpandableHeading
### go-back swipeable left/right

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wHC_QgeGKS4eLonetgUDH_c-t3oukoehdqalzuaazzcgo-back-swipeableiphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wHC_QgeGKS4eLonetgUDH_c-t3oukoehdqalzuaazzcgo-back-swipeableiphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption="swipeable go-back " alt="swipeable go-back "}
:::

:::VerticalSplitItem
This example uses the go-back action as a swipeable property. We can choose the swipe direction left or right. After pressing the button, we return to the previous page.

**Examples left:
**See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-swipeable/go-back-swipeable-left.jigx" target="_blank">GitHub</a>.&#x20;
See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-swipeable/go-back-left-dynamic.jigx" target="_blank">GitHub</a>.&#x20;

**Examples right:
**See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-swipeable/go-back-swipeable-right.jigx" target="_blank">GitHub</a>.&#x20;
See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-swipeable/go-back-right-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
left

```yaml
swipeable:
    left:
        - label: Go back
          color: primary
          onPress:
            type: action.go-back
            
```

right

```yaml
swipeable:
    right:
        - label: Go back
          color: primary
          onPress: 
            type: action.go-back
```
:::
:::::

:::::ExpandableHeading
### go-back rightElement

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/f59eQfajBmOoVwstlCTxe_8n2xgcq2o-rtnrp7hgdmwgo-back-rightelementiphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/f59eQfajBmOoVwstlCTxe_8n2xgcq2o-rtnrp7hgdmwgo-back-rightelementiphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption="rightElement go-back " alt="rightElement go-back "}
:::

:::VerticalSplitItem
In this example, we use the go-back action as the rightElement in the list-item component. There is a button for each item.

**Examples:
**See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-right-element/go-back-right-element.jigx" target="_blank">GitHub</a>.&#x20;
See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-right-element/go-back-right-element-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
goback-right-element

```yaml
rightElement: 
      element: button
      title: Go back
      onPress:
        type: action.go-back
```
:::
:::::

:::::ExpandableHeading
### go-back-on-success

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, we use the `action.go-back` with `onSuccess` to take you back to the main list after signing a form.

**Examples:
**See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-on-success/go-back-on-success.jigx" target="_blank">GitHub</a>.&#x20;

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IHyr3vBgqg8v34h9wMu2E_go-back-onsucces.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IHyr3vBgqg8v34h9wMu2E_go-back-onsucces.PNG" size="80" width="1240" height="2500" position="center" caption="go-back onSuccess" alt="go-back onSuccess"}
:::
::::

:::CodeblockTabs
go-back-on-success

```yaml
title: Signature
type: jig.default
description: In this example, the go-to action is associated with the
  submit-form action. After we enter the signature and press the "Sign" button,
  the submit-form action is performed and then the go-to action redirects us to
  the next page.
  
onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.send-signature-go-to.state.data

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.send-signature-go-to.state.data
    
actions:
  - children:
       - type: action.execute-entity
         options:
           title: Sign & go back to Actions
           provider: DATA_PROVIDER_DYNAMIC
           entity: default/form
           method: create
           data:
             signature: =@ctx.components.signature.state.value
           onSuccess: 
             type: action.go-back
   
children:
  - instanceId: send-signature-go-to
    type: component.form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - instanceId: signature
          type: component.signature-field
          options:
            label: Signature required         
```
:::
:::::

