---
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

# Aggregation

Use JSONata aggregation to return the results of values to find a maximum, minimum, or average value in an array.

## Configuration

<table><thead><tr><th width="131.09765625">Result</th><th>Expression</th></tr></thead><tbody><tr><td>Maximum</td><td><code>=$max(@ctx.datasources.mydata.array)</code></td></tr><tr><td>Minimum</td><td><code>=$min(@ctx.datasources.mydata.array)</code></td></tr><tr><td>Sum</td><td><code>=$sum(@ctx.datasources.mydata.array)</code></td></tr></tbody></table>

{% hint style="warning" %}
&#x20;Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
{% endhint %}

## Examples and code snippets

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/epx-aggregation.png" alt="Aggregated expression" width="188"><figcaption><p>Aggregated expression</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example static data is agregated in a `component.enity` to show the result in the entity field.

See the full example code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="expression.jigx" %}
```yaml
datasources:
  mydata: 
    type: datasource.static
    options:
      data:
        - name: Jane Stevens
          title: Doctor
          email: jane@first.com
          number: 0.64734
          number2: 12
          color: blue
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Max
            value: =$max(@ctx.datasources.mydata.array)
        - type: component.entity-field
          options:
            label: Min
            value: =$min(@ctx.datasources.mydata.array)
        - type: component.entity-field
          options:
            label: Sum
            value: =$sum(@ctx.datasources.mydata.array)
```
{% endcode %}
