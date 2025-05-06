---
title: set-state
slug: XgCi-set-state
description: Learn how to use the "set-state" action in UI components with this comprehensive document. Explore multiple ways to set up this action, including onFocus, onRefresh, onPress, and onChange events. Find examples and code snippets for each setup, enabling yo
createdAt: Tue Jun 14 2022 13:37:28 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Oct 01 2024 13:19:01 GMT+0000 (Coordinated Universal Time)
---

The `set-state` action sets the global state (also called the solution state). Multiple components and jigs can access the state's value across the solution. Effectively managing the global state ensures that all parts of the app that depend on this data are updated consistently. To understand how to use states, see [State]().

## ****Configuration options****

A `set-state` action can be set up in various ways:

1. As `onFocus` action that will be executed.
2. As `onRefresh` action that will be executed.
3. As the main action on the jig, and when you press the action, the `set-state` action will be executed.
4. The `onPress` and `onChange` actions will be executed when you trigger these events.

## Examples and code snippets ****

::::ExpandableHeading
### set-state as onFocus/onRefresh

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/biw9t9RyNz-0XOfnu92pv_set-state-onfocus.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/biw9t9RyNz-0XOfnu92pv_set-state-onfocus.PNG" size="80" width="2536" height="2499" position="center" caption="Count triggers with set-sate" alt="Count triggers with set-sate"}

Set state action is used when the onFocus/onRefresh event is triggered and a count is shown of the number of triggers.

See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/set-state/static-data/set-state-focus-refresh.jigx" target="_blank">GitHub</a>.&#x20;

:::CodeblockTabs
onFocus.jigx

```yaml
onFocus: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.onFocus-key
    value: =@ctx.solution.state.on-focus-key +1 
```

onRefresh.jigx

```yaml
onRefresh: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.onRefresh-key
    value: =@ctx.solution.state.on-refresh-key +1
```
:::
::::

::::ExpandableHeading
### set-state as action

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_gb30xllbsbqiIK8YENCT_set-state-action.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_gb30xllbsbqiIK8YENCT_set-state-action.PNG" size="80" width="2497" height="2511" position="center" caption="Set-state action" alt="Set-state action"}

Set-state action is used as the primary action on the jig, to set the value of the action-key to +1.

See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/set-state/static-data/set-state-action.jigx" target="_blank">GitHub</a>.&#x20;

:::CodeblockTabs
action.jigx

```yaml
actions:
  - children:
      - type: action.set-state
        options:
          title: Add 1 to your action-key
          state: =@ctx.solution.state.action-key
          value: =@ctx.solution.state.action-key +1
```
:::
::::

::::ExpandableHeading
### set-state as onPress/onChange

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qSwlxC1hjffY06BLuvK7u_set-state-onpress.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qSwlxC1hjffY06BLuvK7u_set-state-onpress.PNG" size="78" width="2518" height="2513" position="center" caption="Set-state onPress/onChange" alt="Set-state onPress/onChange"}

Set-state action used on the list as onPress/onChange action, to set the value of the key to +1.

See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/set-state/static-data/set-state-onpress-onchange.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
onPress.jigx

```yaml
onPress: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.onPress-key
    value: =@ctx.solution.state.on-press-key +1
```

onChange.jigx

```yaml
onChange: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.onChange-key
    value: =@ctx.solution.state.on-change-key +1
```
:::
::::

