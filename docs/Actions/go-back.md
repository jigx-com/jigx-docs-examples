---
title: go-back
slug: LX00-go-back
createdAt: Thu Jun 09 2022 18:22:53 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Nov 04 2024 09:47:02 GMT+0000 (Coordinated Universal Time)
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# go-back

This action is used to return to the previous page. Most jigs include this action automatically as an arrow to the left of the title of the jig. This action can be used in a list of actions, such as swipeable and rightElement, or used together with another action, where go-back is called after the main action and returns the user to the previous page.

## Configuration options

A go-back action can be set up in various ways:

1. As a separate action or in the action list
2. As a swipeable action in the left or right direction
3. As rightElement in the list
4. As an associated action in the action list

{% hint style="info" %}
A go-back action associated with another action under onSuccess can only be used with dynamic data.
{% endhint %}

## Examples and code snippets

### go-back as an action

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-goback1.png" alt="go-back as an action" width="188"><figcaption><p>go-back as an action</p></figcaption></figure>
{% endcolumn %}

{% column %}
The simplest example of a go-back action is to use it as a separate action. When configured, a button will appear at the bottom which will return us to the previous page when pressed. In this case, the use of the function is unnecessary because as we can see in the screenshot there is an arrow to the left in the upper left corner. This means that this jig already has a go-back action automatically in it and the arrow has the same function as the "Go back" button below.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-action/go-back-action.jigx).\
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-action/go-back-action-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="go-back-action.jigx" %}
```yaml
actions:
  - children:
      - type: action.go-back
        options:
          title: Go back
```
{% endcode %}

### go-back swipeable left/right

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-goback2.png" alt="swipeable go-back" width="188"><figcaption><p>swipeable go-back</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example uses the go-back action as a swipeable property. We can choose the swipe direction left or right. After pressing the button, we return to the previous page.

**Examples left:** See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-swipeable/go-back-swipeable-left.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-swipeable/go-back-left-dynamic.jigx).

**Examples right:** See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-swipeable/go-back-swipeable-right.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-swipeable/go-back-right-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="left" %}
```yaml
swipeable:
    left:
        - label: Go back
          color: primary
          onPress:
            type: action.go-back
            
```
{% endtab %}

{% tab title="right" %}
```yaml
swipeable:
    right:
        - label: Go back
          color: primary
          onPress: 
            type: action.go-back
```
{% endtab %}
{% endtabs %}

### go-back rightElement

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/ac-goback3.png" alt="rightElement go-back" width="188"><figcaption><p>rightElement go-back</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example, we use the go-back action as the rightElement in the list-item component. There is a button for each item.

**Examples:**\
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-right-element/go-back-right-element.jigx).\
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/dynamic-data/go-back-right-element/go-back-right-element-dynamic.jigx)
{% endcolumn %}
{% endcolumns %}

{% code title="goback-right-element" %}
```yaml
rightElement: 
      element: button
      title: Go back
      onPress:
        type: action.go-back
```
{% endcode %}

### go-back-on-success

{% columns %}
{% column %}
In this example, we use the `action.go-back` with `onSuccess` to take you back to the main list after signing a form.

**Examples:**\
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/go-back/static-data/go-back-on-success/go-back-on-success.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/ac-goback4.png" alt="go-back onSuccess" width="188"><figcaption><p>go-back onSuccess</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% code title="go-back-on-success" %}
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
{% endcode %}
