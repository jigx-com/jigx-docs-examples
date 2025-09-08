---
title: Predicate Queries
slug: ELoX-pre
createdAt: Thu Jul 27 2023 13:16:54 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jul 31 2023 09:13:59 GMT+0000 (Coordinated Universal Time)
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

# Predicate Queries

Use [JSONata Predicate Queries](https://docs.jsonata.org/predicate) at any location path; the selected items can be filtered using a predicate - **\<expr>** where expr evaluates to a Boolean value. With that, you can select values from the array based on the specific type set as the predicate expression.

## Configuration

<table><thead><tr><th width="284.3515625">Result</th><th>Expression</th></tr></thead><tbody><tr><td>Evaluate if true and show the name</td><td><code>=@ctx.datasources.mydata[title='Nurse' and color='blue'].name</code></td></tr></tbody></table>

{% hint style="warning" %}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
{% endhint %}

## Examples and code snippets

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/exp-predicate.png" alt="Predicate queries" width="188"><figcaption><p>Predicate queries</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example the expression is used to show the name of the nurse whose color is blue.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).
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
        - name: Arthur Marks
          title: Nurse
          email: arthur@first.com
          number: 0.98
          number2: 10
          color: red
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]
        - name: Merley Shanks
          title: Nurse
          email: merley@first.com
          number: 0.43
          number2: 9
          color: blue
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Predicate expression
            value: =@ctx.datasources.mydata[title='Nurse' and color='blue'].name
```
{% endcode %}
