# String

In [JSONata String Functions](https://docs.jsonata.org/string-functions), you can concat two strings to display multiple data records in one row, or write numbers as strings, or select only a few characters from the whole string, for example, to display a person's initials.

## String functions

The string functions include:

* [$string()](https://docs.jsonata.org/string-functions#string)
* [$length()](https://docs.jsonata.org/string-functions#length)
* [$substring()](https://docs.jsonata.org/string-functions#substring)
* [$substringBefore()](https://docs.jsonata.org/string-functions#substringbefore)
* [$substringAfter()](https://docs.jsonata.org/string-functions#substringafter)
* [$uppercase()](https://docs.jsonata.org/string-functions#uppercase)
* [$lowercase()](https://docs.jsonata.org/string-functions#lowercase)
* [$trim()](https://docs.jsonata.org/string-functions#trim)
* [$pad()](https://docs.jsonata.org/string-functions#pad)
* [$contains()](https://docs.jsonata.org/string-functions#contains)
* [$split()](https://docs.jsonata.org/string-functions#split)
* [$join()](https://docs.jsonata.org/string-functions#join)
* [$match()](https://docs.jsonata.org/string-functions#match)
* [$replace()](https://docs.jsonata.org/string-functions#replace)
* [$eval()](https://docs.jsonata.org/string-functions#eval)
* [$base64encode()](https://docs.jsonata.org/string-functions#base64encode)
* [$base64decode()](https://docs.jsonata.org/string-functions#base64decode)
* [$encodeUrlComponent()](https://docs.jsonata.org/string-functions#encodeurlcomponent)
* [$encodeUrl()](https://docs.jsonata.org/string-functions#encodeurl)
* [$decodeUrlComponent()](https://docs.jsonata.org/string-functions#decodeurlcomponent)
* [$decodeUrl()](https://docs.jsonata.org/string-functions#decodeurl)

## Configuration

<table><thead><tr><th width="218.5390625">Result</th><th>Expression</th></tr></thead><tbody><tr><td>String concat expression</td><td><code>=@ctx.datasources.mydata.name &#x26; ' ' &#x26; @ctx.datasources.mydata.title</code></td></tr><tr><td>String length</td><td><code>=$length(@ctx.datasources.mydata.name)</code></td></tr><tr><td>Substring</td><td><code>=$substring(@ctx.datasources.mydata.name, 3, 5)</code></td></tr><tr><td>Substring before</td><td><code>=$substringBefore(@ctx.datasources.mydata.name, " ")</code></td></tr><tr><td>Substring after</td><td><code>=$substringAfter(@ctx.datasources.mydata.name, " ")</code></td></tr><tr><td>Upper case</td><td><code>=$uppercase(@ctx.datasources.mydata.name)</code></td></tr><tr><td>Lower case</td><td><code>=$lowercase(@ctx.datasources.mydata.name)</code></td></tr><tr><td>Evaluate PathsData</td><td><code>=$eval(@ctx.current.item.pathsData)</code></td></tr><tr><td>base64</td><td><code>"data:image/png;base64," &#x26; @ctx.datasources.mydata.data</code></td></tr><tr><td>String to number</td><td><code>($number(@ctx.datasources.tmra-graph.Total) >= 5)</code> <code>($number(@ctx.datasources.tmra-graph.Total) &#x3C; 8) ? true : false</code></td></tr><tr><td>Two-letter placeholder for avatar</td><td><code>=$uppercase($substring($substringBefore(@ctx.current.item.firstName, " "), 0, 1) &#x26; $substring($substringAfter(@ctx.current.item.lastName, " ") , 0, 1) )</code></td></tr></tbody></table>

{% hint style="warning" %}
&#x20;Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
{% endhint %}

## Examples and code snippets

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/exp-string.png" alt="String expressions" width="188"><figcaption><p>String expressions</p></figcaption></figure>
{% endcolumn %}

{% column %}
&#x20;This example shows how you can use various string functions to return data.See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).
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

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: String concat expression
            value: =@ctx.datasources.mydata.name & ' ' & @ctx.datasources.mydata.title
        - type: component.entity-field
          options:
            label: String length
            value: =$length(@ctx.datasources.mydata.name)
        - type: component.entity-field
          options:
            label: Substring
            value: =$substring(@ctx.datasources.mydata.name, 3, 5)
        - type: component.entity-field
          options:
            label: Substring before
            value: =$substringBefore(@ctx.datasources.mydata.name, " ")
        - type: component.entity-field
          options:
            label: Substring after
            value: =$substringAfter(@ctx.datasources.mydata.name, " ")
        - type: component.entity-field
          options:
            label: Upper case
            value: =$uppercase(@ctx.datasources.mydata.name)
        - type: component.entity-field
          options:
            label: Lower case
            value: =$lowercase(@ctx.datasources.mydata.name)
```
{% endcode %}
