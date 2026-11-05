# interactive image field

The [interactive-image](../../../docs/Components/interactive-image/interactive-image.md) component can be used as a form field by setting `presentation: field`. In `field` mode, the interactive image behaves like any other form field, such as a `dropdown` or `signature` field. It has a `label`, a `value`, `validation`, and `onChange`. The selected points are submitted with the form.

In a form, the `field` renders as a collapsed row that shows a floating label, a summary of how many points are selected, and a read-only preview of the image. Tapping the row opens a full-height picker where the user selects points on the image. The picker shows the image with the group cards beneath it, and a pinned **Cancel** / **Confirm** footer:

* **Confirm** commits the selection to the field's value and triggers `onChange` once for the whole picker session.
* **Cancel**, tapping the backdrop, or swiping the picker down discards the changes and restores the selection from when the picker was opened.

The points on the image are configured with [interactive-image-item](../../../docs/Components/interactive-image/interactive-image-item.md), in the same way as the inline interactive image.

{% hint style="info" %}
The default `presentation` is `inline`, so existing interactive images are not affected. An inline interactive image placed inside a form is not part of the form: its selection is not included in the submitted form data, it does not block form submission, and its `onChange` is not triggered.
{% endhint %}

## Configuration options

Some properties are common to all components. See [Common component properties](<../../../docs/Components/Common component properties.md>) for the properties and their configuration options.

### Core structure

<table><thead><tr><th width="175.6328125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>presentation</code></td><td>Set to <code>field</code> to use the interactive image as a form field. The default is <code>inline</code>, which displays the image directly on the screen and does not take part in the form.</td></tr><tr><td><code>instanceId</code></td><td>The unique identifier of the field. The <code>instanceId</code> is used as the key for the field's value in the form data when the form is submitted, for example, <code>{"damaged-parts": ["1","3"]}</code>.</td></tr><tr><td><code>label</code></td><td>The <code>label</code> displayed on the field row. The <code>label</code> floats above the selection summary once points are selected.</td></tr><tr><td><code>source</code></td><td>The image to display, specified as a <code>uri</code>.</td></tr><tr><td><code>data</code></td><td>The datasource that provides the points displayed on the image, for example, <code>=@ctx.datasources.vehicle-parts</code>.</td></tr><tr><td><code>item</code></td><td>The <a href="../../../docs/Components/interactive-image/interactive-image-item.md">interactive-image-item</a> that configures each point, including its <code>id</code>, <code>title</code>, and <code>percentageCoordinates</code>. The item's <code>id</code> is the value stored in the field when the point is selected.</td></tr></tbody></table>

### Other options

<table><thead><tr><th width="175.83203125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>groups</code></td><td>Create groups to categorize the selected points, for example, Damaged or Scratched. Each group has an <code>id</code>, <code>title</code>, optional <code>color</code>, and optional <code>maximumPoints</code> that limits how many points can be added to the group. The groups display as cards in the picker, and each selected point displays as a removable tag on its group's card. If no groups are configured, the picker shows all selected points in a single Selected card.</td></tr><tr><td><code>helperText</code></td><td>Text displayed under the field to guide the user, for example, Tap to mark the damaged parts.</td></tr><tr><td><code>errorText</code></td><td>Text displayed under the field when the field is invalid.</td></tr><tr><td><code>initialValue</code></td><td>The point id(s) selected when the field loads. Use an array of ids when <code>isMultiple</code> is <code>true</code>, for example, <code>['3','1']</code>, and a single id when <code>isMultiple</code> is <code>false</code>, for example, <code>'2'</code>. Seeding the field with <code>initialValue</code> does not mark the form as dirty.</td></tr><tr><td><code>isHidden</code></td><td>Hides the field when set to <code>true</code>. Use an expression to show or hide the field dynamically.</td></tr><tr><td><code>isMultiple</code></td><td>Set to <code>false</code> to allow only one point to be selected. Selecting a new point replaces the previously selected point, and the field's value is a single id instead of an array. The default is <code>true</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> to make the field required. An asterisk displays next to the label until a point is selected, and the form cannot be submitted without a selection.</td></tr><tr><td><code>pointColor</code></td><td>The color of the points on the image that are available for selection.</td></tr><tr><td><code>style</code></td><td><code>isDisabled</code> - disables the field so that the picker cannot be opened and the selection cannot be changed.</td></tr><tr><td><code>value</code></td><td>Sets the field's value, using the point id(s) in the same format as <code>initialValue</code>.</td></tr></tbody></table>

{% hint style="info" %}
`imageHeight` has no effect when `presentation` is set to `field`, as the row keeps the standard height of a form field. On an inline interactive image, `imageHeight` caps the height of the image. If `imageHeight` is not set on an inline image, the image fills the width of its container.
{% endhint %}

### Actions

<table><thead><tr><th width="143.46484375">Action</th><th>Description</th></tr></thead><tbody><tr><td><code>onChange</code></td><td>The action is triggered when the selection changes. When the user selects points in the picker, the action is triggered once, when the user presses Confirm, not for each point pressed. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr><tr><td><code>onBlur</code></td><td>The action is triggered when the field loses focus. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

### State Configuration

<table><thead><tr><th width="240.62890625">State</th><th width="190.08984375">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td><code>value</code><br><code>selected</code></td><td><code>value</code> - the id(s) of the selected points, for example, <code>["1","3"]</code>, or <code>"3"</code> when <code>isMultiple</code> is <code>false</code>.<br><code>selected</code> - the datasource records of the selected points, for example, <code>=@ctx.components.damaged-parts.state.selected.title</code> returns <code>["Hood","Trunk"]</code>.</td></tr><tr><td><code>=@ctx.components.form-id.state.</code></td><td><code>data</code><br><code>isValid</code><br><code>isDirty</code></td><td>The form state includes the interactive image field's value in <code>data</code>, keyed by the field's <code>instanceId</code>.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td><code>activeItemId now</code></td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

### Points selected on load

A point is selected when the field loads if its id is in `initialValue`, or if the interactive-image-item sets `style.isActive` to `true` for that point. Points made active through `style.isActive` are written into the field's value on load, so the field's value includes both. For example, with `initialValue: ['3','1']` and `isActive` set for point `4`, the field's value is `["1","3","4"]`.

{% hint style="warning" %}
Points activated through the item's `style.isActive` are written into the value when the field loads, so the form is dirty from the start. Use `initialValue` if the form must stay untouched until the user makes a selection.
{% endhint %}

## Examples and code snippets

### Vehicle damage inspection example

The example shows a vehicle inspection form where the inspector taps the **Damaged parts** field and marks the damaged parts on the image of the vehicle. The field is required, so the form cannot be submitted until at least one part is selected. The `groups` property is used to differentiate between scratched and dented parts. On submit, the ids of the selected parts are saved with the inspection.

{% tabs %}
{% tab title="vehicle-inspection (dynamic)" %}
```yaml
title: Vehicle inspection
type: jig.default

actions:
  - children:
      - type: action.submit-form
        options:
          title: Submit inspection
          formId: inspection-form
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/vehicle-inspections
          method: save

datasources:
  vehicle-parts:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/vehicle-parts
      query: |
        SELECT
          id,
          '$.title',
          json_extract(data, '$.x') as x,
          json_extract(data, '$.y') as y
        FROM [default/vehicle-parts]

children:
  - type: component.form
    instanceId: inspection-form
    options:
      children:
        - type: component.text-field
          instanceId: registration
          options:
            label: Registration number
            isRequired: true
        - type: component.interactive-image
          instanceId: damaged-parts
          options:
            # Render the image as a form field that opens a picker.
            presentation: field
            label: Damaged parts
            helperText: Tap to mark the damaged parts on the vehicle.
            isRequired: true
            source:
              uri: https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a?w=800&q=80
            data: =@ctx.datasources.vehicle-parts
            pointColor: color10
            groups:
              - id: scratched
                title: Scratched
                color: color2
              - id: dented
                title: Dented
                color: color14
            item:
              type: component.interactive-image-item
              options:
                # The id is stored in the field's value when the point is selected.
                id: =@ctx.current.item.id
                title: =@ctx.current.item.title
                percentageCoordinates:
                  x: =@ctx.current.item.x
                  y: =@ctx.current.item.y
        - type: component.text-field
          instanceId: notes
          options:
            label: Notes
            isMultiline: true
```
{% endtab %}

{% tab title="vehicle-inspection (static)" %}
```yaml
title: Vehicle inspection
type: jig.default

actions:
  - children:
      - type: action.submit-form
        options:
          title: Submit inspection
          formId: inspection-form
          provider: DATA_PROVIDER_LOCAL
          entity: vehicle-inspections
          method: save

datasources:
  vehicle-parts:
    type: datasource.static
    options:
      data:
        - id: '1'
          title: Hood
          x: 25
          y: 30
        - id: '2'
          title: Door
          x: 50
          y: 55
        - id: '3'
          title: Trunk
          x: 75
          y: 30
        - id: '4'
          title: Roof
          x: 50
          y: 20

children:
  - type: component.form
    instanceId: inspection-form
    options:
      children:
        - type: component.interactive-image
          instanceId: damaged-parts
          options:
            presentation: field
            label: Damaged parts
            helperText: Tap to mark the damaged parts on the vehicle.
            isRequired: true
            source:
              uri: https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a?w=800&q=80
            data: =@ctx.datasources.vehicle-parts
            pointColor: color10
            groups:
              - id: scratched
                title: Scratched
                color: color2
              - id: dented
                title: Dented
                color: color14
            item:
              type: component.interactive-image-item
              options:
                id: =@ctx.current.item.id
                title: =@ctx.current.item.title
                percentageCoordinates:
                  x: =@ctx.current.item.x
                  y: =@ctx.current.item.y
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  vehicle-parts:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/vehicle-parts
      query: |
        SELECT
          id,
          '$.title',
          json_extract(data, '$.x') as x,
          json_extract(data, '$.y') as y
        FROM [default/vehicle-parts]
```
{% endtab %}

{% tab title="form data (submitted)" %}
```json
{
  "registration": "CA 123-456",
  "damaged-parts": ["1", "3"],
  "notes": "Scratches on the hood, dent on the trunk lid."
}
```
{% endtab %}
{% endtabs %}

### Single selection example

The example shows a field where only one part can be selected. `isMultiple` is set to `false`, so selecting a new point replaces the previous point, and the field's value is a single id instead of an array. The `Primary damage` group is limited to one point with `maximumPoints`. The field loads with the Door (`'2'`) selected using `initialValue`, and the form stays untouched until the user changes the selection.

{% tabs %}
{% tab title="interactive-image-field-single" %}
```yaml
children:
  - type: component.form
    instanceId: inspection-form
    options:
      children:
        - type: component.interactive-image
          instanceId: primary-damage
          options:
            presentation: field
            label: Primary damage
            isRequired: true
            # Only one point can be selected; the value is a single id.
            isMultiple: false
            initialValue: '2'
            source:
              uri: https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a?w=800&q=80
            data: =@ctx.datasources.vehicle-parts
            groups:
              - id: primary
                title: Primary damage
                maximumPoints: 1
            item:
              type: component.interactive-image-item
              options:
                id: =@ctx.current.item.id
                title: =@ctx.current.item.title
                percentageCoordinates:
                  x: =@ctx.current.item.x
                  y: =@ctx.current.item.y
```
{% endtab %}

{% tab title="form data (submitted)" %}
```json
{
  "primary-damage": "3"
}
```
{% endtab %}
{% endtabs %}

### Pre-selected points with conditional visibility example

The example shows a follow-up inspection where parts recorded in the previous inspection are pre-selected. `initialValue` selects the Hood and Trunk, and the item's `style.isActive` selects the Roof (`'4'`), so the field's value on load is `["1","3","4"]`. The field is shown only when the inspector indicates that the vehicle is damaged, and is disabled once the inspection is signed off. Each confirmed change in the picker increments a counter in solution state using `onChange`.

{% tabs %}
{% tab title="interactive-image-field-seeded" %}
```yaml
children:
  - type: component.form
    instanceId: inspection-form
    options:
      children:
        - type: component.checkbox
          instanceId: has-damage
          options:
            label: Vehicle has damage
        - type: component.interactive-image
          instanceId: damaged-parts
          options:
            presentation: field
            label: Damaged parts
            # Seed the field with the parts from the previous inspection.
            initialValue:
              - '3'
              - '1'
            isHidden: =@ctx.components.has-damage.state.value != true
            style:
              isDisabled: =@ctx.solution.state.inspection-signed-off = true
            groups:
              - id: damaged
                title: Damaged
            source:
              uri: https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a?w=800&q=80
            data: =@ctx.datasources.vehicle-parts
            onChange:
              type: action.set-state
              options:
                state: =@ctx.solution.state.damage-changes
                value: =@ctx.solution.state.damage-changes + 1
            item:
              type: component.interactive-image-item
              options:
                id: =@ctx.current.item.id
                title: =@ctx.current.item.title
                # Active points are added to the field's value on load.
                style:
                  isActive: =@ctx.current.item.id = '4'
                percentageCoordinates:
                  x: =@ctx.current.item.x
                  y: =@ctx.current.item.y
```
{% endtab %}

{% tab title="index.jigx (state)" %}
```yaml
state:
  damage-changes:
    type: number
    initialValue: 0
  inspection-signed-off:
    type: boolean
    initialValue: false
```
{% endtab %}
{% endtabs %}

## See also

* [State](https://docs.jigx.com/building-apps-with-jigx/logic/state)
