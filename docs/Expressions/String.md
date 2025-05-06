---
title: String
slug: SHfU-string
description: Learn about JSONata string functions such as concatenation, length determination, substring extraction, case conversion, whitespace trimming, and more. Discover practical examples and code snippets to understand how to use these powerful string operations
createdAt: Thu Jul 27 2023 10:59:39 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jul 31 2023 09:15:04 GMT+0000 (Coordinated Universal Time)
---

In <a href="https://docs.jsonata.org/string-functions" target="_blank">JSONata String Functions,</a> you can concat two strings to display multiple data records in one row or write numbers as strings, or select only a few characters from the whole string, for example, to display a person's initials.

## String functions&#x20;

The string functions include:

- [$string()](https://docs.jsonata.org/string-functions#string)
- [$length()](https://docs.jsonata.org/string-functions#length)
- [$substring()](https://docs.jsonata.org/string-functions#substring)
- [$substringBefore()](https://docs.jsonata.org/string-functions#substringbefore)
- [$substringAfter()](https://docs.jsonata.org/string-functions#substringafter)
- [$uppercase()](https://docs.jsonata.org/string-functions#uppercase)
- [$lowercase()](https://docs.jsonata.org/string-functions#lowercase)
- [$trim()](https://docs.jsonata.org/string-functions#trim)
- [$pad()](https://docs.jsonata.org/string-functions#pad)
- [$contains()](https://docs.jsonata.org/string-functions#contains)
- [$split()](https://docs.jsonata.org/string-functions#split)
- [$join()](https://docs.jsonata.org/string-functions#join)
- [$match()](https://docs.jsonata.org/string-functions#match)
- [$replace()](https://docs.jsonata.org/string-functions#replace)
- [$eval()](https://docs.jsonata.org/string-functions#eval)
- [$base64encode()](https://docs.jsonata.org/string-functions#base64encode)
- [$base64decode()](https://docs.jsonata.org/string-functions#base64decode)
- [$encodeUrlComponent()](https://docs.jsonata.org/string-functions#encodeurlcomponent)
- [$encodeUrl()](https://docs.jsonata.org/string-functions#encodeurl)
- [$decodeUrlComponent()](https://docs.jsonata.org/string-functions#decodeurlcomponent)
- [$decodeUrl()](https://docs.jsonata.org/string-functions#decodeurl)

## Configuration

| **Result**                        | **Expression**                                                                                                                                             |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| String concat expression          | `=@ctx.datasources.mydata.name & ' ' & @ctx.datasources.mydata.title`                                                                                      |
| String length                     | `=$length(@ctx.datasources.mydata.name)`                                                                                                                   |
| Substring                         | `=$substring(@ctx.datasources.mydata.name, 3, 5)`                                                                                                          |
| Substring before                  | `=$substringBefore(@ctx.datasources.mydata.name, " ")`                                                                                                     |
| Substring after                   | `=$substringAfter(@ctx.datasources.mydata.name, " ")`                                                                                                      |
| Upper case                        | `=$uppercase(@ctx.datasources.mydata.name)`                                                                                                                |
| Lower case                        | `=$lowercase(@ctx.datasources.mydata.name)`                                                                                                                |
| Evaluate PathsData                | `=$eval(@ctx.current.item.pathsData)`                                                                                                                      |
| base64                            | `"data:image/png;base64," & @ctx.datasources.mydata.data`                                                                                                  |
| String to number                  | `($number(@ctx.datasources.tmra-graph.Total) >= 5)`<br />`($number(@ctx.datasources.tmra-graph.Total) < 8) ? true : false`                                 |
| Two-letter placeholder for avatar | `=$uppercase($substring($substringBefore(@ctx.current.item.firstName, " "), 0, 1) & $substring($substringAfter(@ctx.current.item.lastName, " ") , 0, 1) )` |

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets 

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![String expressions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0ZtwGqI1_Axa_fo3SqwC4_img6601iphone13blueportrait.png "String expressions")
:::

::::VerticalSplitItem
This example shows how you can use various string functions to return data.See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx" target="_blank">GitHub</a>.&#x20;

:::CodeblockTabs
expression.jigx

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
:::
::::
:::::

###

