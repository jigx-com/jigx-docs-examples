# Arrays

Handling arrays when saving data to SQL and Dynamic Data require JSONATA expressions to return the data as an array rather than a string.

The operators used for handling arrays are:

* [array functions - count](https://docs.jsonata.org/array-functions)
* [string function - split](https://docs.jsonata.org/string-functions#split)
* [string function- eval](https://docs.jsonata.org/string-functions#eval)

## Dynamic Data Configuration

Usually, data in Dynamic Data is saved as an array, for example, `['value1', 'value2'],` but when Dynamic Data returns the data, it is stringified as `"['value1', 'value2']"`. If the data is used in components, for example, to show an `intialValue`, it is not seen as an array but rather as a string. Use the `=$eval` before the expression to return the data in an array.

**Example**

`=$eval(@ctx.datasources.profile.food)`

{% code title="dropdown-dd" %}
```yaml
children:
  - type: component.form
    instanceId: food-selection
    options:
      children:
        - type: component.dropdown
          instanceId: meals
          options:
            label: meal options
            data: =@ctx.datasources.food
      # use eval to return an array on food selected in the dropdown      
            initialValue: =$eval(@ctx.datasources.food.name)
              
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.name
```
{% endcode %}

## SQL Configuration

Data is sent as an array, for example, \['value1', 'value2'], SQL then saves the data as; VARCHAR(MAX), for example, `'value1, value2'`. If the data is used in components, for example, to show an `intialValue`, it is not seen as an array but rather as a string. Use the `=$split` before the expression to return the data in an array.

**Example**

`=$split(@ctx.datasources.profile.food, ',')`

{% code title="dropdown-sql" %}
```yaml
children:
  - type: component.form
    instanceId: food-selection
    options:
      children:
        - type: component.dropdown
          instanceId: meals
          options:
            label: meal options
            data: =@ctx.datasources.food
            initialValue: =$split(@ctx.datasources.profile.food, ',')
              
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.name
```
{% endcode %}

There could be a scenario where there is only one string inside an array. Use the `=$.count` to determine if there is only one string in the array or more. If there are more than one, include `$.split` in the expression.

**Example**

`=$count($split(@ctx.datasource.profile.food, ',')) = 1 ? @ctx.datasources.profile.food:$count($split(@ctx.datasources.profile.food, ',')) >1 ? $split(@ctx.datqasources.food, ','):null`

{% code title="dropdown-sql-count" %}
```yaml
children:
  - type: component.form
    instanceId: food-selection
    options:
      children:
        - type: component.dropdown
          instanceId: meals
          options:
            label: meal options
            data: =@ctx.datasources.food
# Count to see if there is only 1 string or more           
            initialValue: =$count($split(@ctx.datasource.profile.food, ',')) = 1 ? @ctx.datasources.profile.food:$count($split(@ctx.datasources.profile.food, ',')) >1 ? $split(@ctx.datqasources.food, ','):null
              
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.name
```
{% endcode %}

## Create a filtered list from an array of records

{% columns %}
{% column %}
&#x20;![Result with Advanced Expressions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LGvYapk-Ctp7XNjyF1AhK_ldcfoljjvzbydshpyny6img1005iphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
We will display a list of people from the array of records, then filter them and display those that have entered a name. We will display their initials as a left avatar and add a label to each list item to display whether they are registered.

Filter an array of records to display specific data and perform expression transformations over the data.

See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/samples/jigx-samples/jigs/guide-advanced-expressions/static-data/advanced-expressions-list.jigx).
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
