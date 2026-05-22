# onAppActivated

Use the  `onAppActivated` event to execute actions when the app returns to the foreground from `background` or `inactive`. This event is useful for refreshing data or updating state after the user comes back to the app.&#x20;

### When it runs

* `onAppActivated` runs only when the app changes from `background` or `inactive` to `active`.
* It does not run on cold start. It also does not run during normal jig navigation.
* Use `onFocus` for screen-to-screen navigation. Use `onLoad` for cold start setup.
* When quickly switching the app in and out of the background repeatedly, Jigx won't kick off a separate data sync process each time, it waits for any currently running sync to finish before starting a new one, so you never end up with multiple syncs running simultaneously and stepping on each other.
* The datastore becomes active before `onAppActivated` runs.
* If both solution-level and jig-level handlers are configured, the solution handler settles first. The jig handler runs after that.
* In [jig.tabs](<../../docs/Jig Types/jig_tabs.md>), only the active tab's jig runs `onAppActivated`. Inactive tabs are skipped.

### Where to use it

You can configure `onAppActivated` at:

* solution level in `index.jigx`
* jig level in any jig

### Configuration options

`onAppActivated` accepts a single action configuration. To execute multiple actions use the `action.action-list` .

### Examples

#### Solution-level example

Use a solution-level configuration when the action should run once after the app becomes active.

```yaml
onAppActivated:
  type: action.set-solution-state
  options:
    changes:
      last-activated: =$now()
```

#### Jig-level example

Use a jig-level configuration when the active jig should refresh its own data.

```yaml
onAppActivated:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_LOCAL
    entity: my-entity
    function: functions/refresh
```

### Considerations

* Use `onAppActivated` when the app returns from the background.
* Use `onFocus` when a solution or jig becomes the active screen.
* Use `onLoad` for setup that must run on first launch.
