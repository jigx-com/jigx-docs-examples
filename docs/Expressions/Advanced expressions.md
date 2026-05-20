# Advanced expressions

Use [Advanced Expressions](<Advanced expressions.md>) to filter an array of records to display specific data and perform expression transformations over the data.

## Examples and code snippets

## Create a filtered list from an array of records

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/exp- advancedFilter.png" alt="Result with Advanced Expressions" width="188"><figcaption><p>Result with Advanced Expressions</p></figcaption></figure>
{% endcolumn %}

{% column %}
We will display a list of people from the array of records, then filter them and display those that have entered a name. We will display their initials as a left avatar and add a label to each list item to display whether they are registered.

See the full example in [GitHub.](https://github.com/jigx-com/jigx-samples/blob/main/samples/jigx-samples/jigs/guide-advanced-expressions/static-data/advanced-expressions-list.jigx)
{% endcolumn %}
{% endcolumns %}

{% code title="advanced-expression.jigx" %}
```yaml
title: List with advanced Expressions
type: jig.list

datasources:
  people:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: Mark
          lastname: Dobrew
          email: mark@gmail.com
          mobile: 783432565
          registered: false
        - id: 2
          firstname: Astra
          lastname: Courts
          email: astra@gmail.com
          mobile: 437874221
          registered: false
        - id: 3
          firstname: Jane
          lastname: Doe
          email: jane@gmail.com
          mobile: 783432531
          registered: true
        - id: 4
          firstname: ''
          lastname: ''
          email: steve@gmail.com
          mobile: 783432531
          registered: true

data: =@ctx.datasources.people[firstname != '' and lastname != '']
item:
  type: component.list-item
  options:
    title: "=@ctx.current.item.firstname 
            & ' ' & 
            @ctx.current.item.lastname"
    subtitle: ='Phone:' & @ctx.current.item.mobile
    description: ='Email:' & @ctx.current.item.email
    style:
      isHighlighted: "=@ctx.current.item.registered = true 
                      ? true:false"
    label:
      title: "=@ctx.current.item.registered = true 
              ? 'Registered':'Not registered'"
      color:
        - when: =@ctx.current.item.registered = true 
          color: color2
        - when: =@ctx.current.item.registered = false
          color: color4
    leftElement: 
      type: avatar
      text: "=$substring(@ctx.current.item.firstname,0,1) 
            & $substring(@ctx.current.item.lastname,0,1)"
```
{% endcode %}

## Define functions to run the expressions

As part of advanced expressions, you can define functions that will run the expressions. It can be a function for date transformations, maths calculations, or any string transformations. By using functions you will have cleaner code that is easier to read.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/exp-advancedFunction.png" alt="Divided by 10" width="188"><figcaption><p>Divided by 10</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example shows a simple function that will divide the number from the datasource.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-advanced-expressions/static-data/advanced-expressions-list.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="advanced-expression.jigx" %}
```yaml
datasources:
  number-data:
    type: datasource.static
    options:
      data:
        - id: 1
          number: 2500
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Expression to get result divided by 10
            value: =($b := function($l, $w){ $l / $w }; $b(@ctx.datasources.number-data.number,10);)
```
{% endcode %}
