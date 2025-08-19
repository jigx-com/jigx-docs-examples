---
title: stage
slug: Cw5F-stage
createdAt: Thu Jun 09 2022 19:58:34 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Apr 24 2025 07:14:20 GMT+0000 (Coordinated Universal Time)
---

# stage

In this component, you add left and right elements, typically showing a start-and-end concept, such as flight schedules.

### Configuration options

Some properties are common to all components, see [Common component properties](docId:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

<table><thead><tr><th width="164.26171875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>left</code></td><td>Add content to the <code>left</code> element as text, or use an expression.</td></tr><tr><td><code>right</code></td><td>Add content to the <code>right</code> element as text, or use an expression.</td></tr><tr><td><code>title</code></td><td>Add <code>titles</code> for the text on the <code>left</code> and <code>right</code> elements.</td></tr></tbody></table>

<table><thead><tr><th width="167.36328125">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Add an icon to show in the <code>centerElement</code>. A list of icons is available. See <a href="https://docs.jigx.com/jigx-icons">Jigx icons</a> for more information.</td></tr><tr><td><code>style</code></td><td><code>isWaitingSync</code> - Will display a "Waiting sync" indicator (cloud with a line through it), a visual indicator showing that data has not been synced to the cloud yet.</td></tr><tr><td><code>subtitle</code></td><td>Add a <code>subtitle</code> to either the left or right element as text, or use an expression.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="166.58984375">Actions</th><th></th></tr></thead><tbody><tr><td><code>onPress</code></td><td>The action is triggered while pressing on the content in the stage. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

### Consideration

* `component.stage` can only be used in the `component.expander` or a [list](../list/stage.md).

### Examples and code snippets

#### Stage in expander

{% columns %}
{% column %}
![Stage in expander](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQUOSOOooTNZSRT6fBCoU_dqf676mvwvyz4w1feir5qstageiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/static-data/stage.jigx). \
See the full example using dynamic data [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/dynamic-data/stage-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="stage (static)" %}
```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.stage
          options:
            right:
              title: Boston
              subtitle: 11:30
            left:
              title: New York
              subtitle: 12:30
```
{% endtab %}

{% tab title="stage (dynamic)" %}
```yaml
title: Stage
type: jig.default

children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.stage
          options:
            right:
              title: =@ctx.datasources.trip-dynamic[3].from
              subtitle: =@ctx.datasources.trip-dynamic[3].board
            left:
              title: =@ctx.datasources.trip-dynamic[3].to
              subtitle: =@ctx.datasources.trip-dynamic[3].disembark
      children:
        - type: component.entity
          options:
            children:
              - type: component.entity-field
                options:
                  label: tbd
                  value: tbd
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  trip-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/flight-schedule
      query: |
        SELECT 
          id, 
          '$.airline', 
          '$.board', 
          '$.disembark', 
          '$.date', 
          '$.flight', 
          '$.from', 
          '$.fromabrv', 
          '$.gate', 
          '$.name', 
          '$.seat', 
          '$.to', 
          '$.toabrv' 
        FROM [default/flight-schedule]
```
{% endtab %}
{% endtabs %}

#### Stage in list

{% columns %}
{% column %}
&#x20;![Stage in list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8oR-ecX43O27thnShsgId_mlmkhpfrzwatv8spkkz7vstageiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/static-data/stage-list.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/dynamic-data/stage-list-dynamic.jigx).

**Datasources:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/trip-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/trip-dynamic.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="stage-list (static)" %}
```yaml
title: Trip in list
type: jig.list

data: =@ctx.datasources.trip-static
item:
  type: component.stage
  options:
    right:
      title: =@ctx.current.item.to
      subtitle: =@ctx.current.item.time-to
    left:
      title: =@ctx.current.item.from
      subtitle: =@ctx.current.item.time-from
```
{% endtab %}

{% tab title="stage-list (dynamic)" %}
```yaml
title: Stage in list
type: jig.list

data: =@ctx.datasources.trip-dynamic
item:
  type: component.stage
  options:
    right:
      title: =@ctx.current.item.from
      subtitle: =@ctx.current.item.board
    left:
      title: =@ctx.current.item.to
      subtitle: =@ctx.current.item.disembark
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  trip-static:
    type: datasource.static
    options:
      data:
        - id: 1
          from: Boston
          time-from: 11:30
          to: New York
          time-to: 12:30
        - id: 1
          from: Las Vegas
          time-from: 09:45
          to: London
          time-to: 19:00
        - id: 1
          from: Paris
          time-from: 13:15
          to: Prague
          time-to: 17:30
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  trip-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/flight-schedule
      query: |
        SELECT 
          id, 
          '$.airline', 
          '$.board', 
          '$.disembark', 
          '$.date', 
          '$.flight', 
          '$.from', 
          '$.fromabrv', 
          '$.gate', 
          '$.name', 
          '$.seat', 
          '$.to', 
          '$.toabrv' 
        FROM [default/flight-schedule]
```
{% endtab %}
{% endtabs %}
