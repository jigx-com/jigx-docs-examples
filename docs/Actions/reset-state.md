---
title: reset-state
slug: EQV7-reset-state
createdAt: Mon Jun 13 2022 13:39:09 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Sep 30 2024 12:19:59 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to effectively use the reset-state action in Jig files with this
  comprehensive document. Discover multiple approaches to set up this action,
  such as utilizing onFocus, onRefresh, onPress, or
---

# reset-state

`Reset-state` action is typically used to reset the state of the key inside the jig file and can be used further to reset the state of UI components and forms. To understand how to use states, see [State](https://docs.jigx.com/state).

### Configuration options

There are multiple ways to set up a reset-state action within a jig:

1. As `onFocus` action that will be executed.
2. As `onRefresh` action that will be executed.
3. As the main action on the jig, and when you press the action, the `reset-state` action will be executed.
4. The `onPress` and `onChange` actions will be executed when you trigger the `onPress` or `onChange` event.

### Examples and code snippets

::::ExpandableHeading

#### reset-state onFocus/onRefresh

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/me\_Ah8R\_TyYAScqJsBsn6\_reset-state-onfocus.PNG" size="80" position="center" caption="Reset-state onFocus/onRefresh" alt="Reset-state onFocus/onRefresh"}

1. Reset-state action is used when the onFocus/onRefresh event is triggered to reset the component's state or key.
2. You can specify instanceId, this will be the name of the UI component.
3. And you need to specify the key, which will be the value of the UI component or the name of the key that you want to reset.

**Example:** See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/reset-state/static-data/reset-state-focus-load-refresh.jigx).

:::CodeblockTabs onFocus.jigx

```yaml
onFocus:
  type: action.reset-state
  options:
    state: =@ctx.solution.state.onFocus-key
```

onRefresh.jigx

```yaml
onRefresh:
  type: action.reset-state
  options:
    state: =@ctx.solution.state.onRefresh-key
```

::: ::::

::::ExpandableHeading

#### reset-state as action

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/c43Ii0P7\_-wNzHN8VeReE\_reset-state-action.PNG" size="80" position="center" caption="Reset-state action" alt="Reset-state action"}

1. Reset-state action is used as the primary action on the jig, to reset-state of the component in the jig and its value.
2. You can specify **instanceId**, this will be the name of the UI component
3. And you need to specify the **key**, which will be the value of the UI component that you want to reset

**Example:**

See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/reset-state/static-data/reset-state-action-form.jigx).

:::CodeblockTabs action.jigx

```yaml
actions:
  - children:
      - type: action.reset-state
        options:
          title: Reset state of the form
          state: =@ctx.components.form.state.data
```

::: ::::

::::ExpandableHeading

#### reset-state onPress/onChange

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vrFGC9hXE3ufLaIzJ2c-m\_reset-state-onpress.PNG" size="80" position="center" caption="Reset-state onPress/onChange" alt="Reset-state onPress/onChange"}

1. Reset-state action used on the list as **onPress** or **onChange** action, to reset-state of the component.
2. You can specify instanceId, this will be the name of the UI component.
3. And you need to specify the **state**, which will be the value of the UI component that you want to reset

**Example:**

See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/reset-state/static-data/reset-state-onpress-onchange.jigx).

:::CodeblockTabs onPress.jigx

```yaml
onPress:
  type: action.reset-state
  options:
    state: =@ctx.solution.state.onPress-key
```

onChange.jigx

```yaml
onChange:
  type: action.reset-state
  options:
    state: =@ctx.solution.state.onChange-key
```

::: ::::
