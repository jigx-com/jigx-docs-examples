# Functional Programming

You can use [JSONata Functional programming](https://docs.jsonata.org/programming) to compare values or display data based on certain conditions. You can quickly make any logical statements, and based on the result, you can perform different actions.

## Configuration

<table><thead><tr><th width="251.87109375">Result</th><th>Expression</th></tr></thead><tbody><tr><td>Determine if the value is bigger or smaller than a certain number</td><td><code>"=@ctx.datasources.mydata.number2 > 10 ? 'Number is bigger':'Number is lower'"</code></td></tr><tr><td>Variables</td><td><code>="&#x3C;div style='font-size: 40px'>Welcome on board &#x3C;b>" &#x26; @ctx.datasources.html.name &#x26; "&#x3C;/b> - " &#x26; @ctx.datasources.html.email &#x26; "&#x3C;/div></code></td></tr></tbody></table>

{% hint style="warning" %}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
{% endhint %}

## Examples and code snippets

### Compare values

{% columns %}
{% column %}
&#x20;![Functional expressions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0uqaFEwFcsgWqmsxHy1uN_mk6aixjb8o06to7dpzsifimg0979iphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
In this example we determine if the value for `entity.field` is bigger or smaller that 10.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx)
{% endcolumn %}
{% endcolumns %}

{% code title=" expression.jigx" %}
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
            label: Functional expression
            value: "=@ctx.datasources.mydata.number2 > 10 
                    ? 'Number is bigger':'Number is lower'"
```
{% endcode %}

### Variables in content

{% columns %}
{% column %}
&#x20;![Content](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VAw06TIFPwJhNmAezMiwA_contentiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
This example shows how to write variables in HTML content.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/variablesInContent.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="variablesInContent.jigx" %}
```yaml
source:
  documentType: HTML
  content: |
    ="<div style='font-size: 40px'>Welcome on board 
    <b>" & @ctx.datasources.html.name & "</b>
     - " & @ctx.datasources.html.email &
    "</div>
    <br>
    <img src='https://chart.googleapis.com/chart?cht=qr&chl=id"&@ctx.datasources.html.itemId&"&chs=380x380&choe=UTF-8&chld=L|2' alt='qr code'>
    <a href='https://www.qr-code-generator.com' border='0' style='cursor:default'  rel='nofollow'></a>
    <br>"  & @ctx.datasources.html.itemId
```
{% endcode %}

### Multiple select in a dropdown

{% columns %}
{% column %}
&#x20;![Multiple selector expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/q9ObXqaGM9y4_deRVoVdX_multipleselectiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
In this example, we use the notation in which we select the instanceId of our component from the components, and extract the selected from the state of the component, then choose the required value. For example id, name,...

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/multipleSelect.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% code title=" multipleSelect.jigx" %}
```yaml
children:
  - type: component.form
    instanceId: selected-people-form
    options:
      children:
        - type: component.dropdown
          instanceId: selected-people-dropdown
          options:
            label: Select people
            data: =@ctx.datasources.employees-static
            isMultiple: true
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
                value: =@ctx.current.item.id
                leftElement: 
                  element: avatar
                  text: =$substring(@ctx.current.item.firstname, 0, 1) & $substring(@ctx.current.item.lastname, 0, 1)
                  uri: =@ctx.current.item.img
```
{% endcode %}
