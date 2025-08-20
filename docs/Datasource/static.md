# static

Static lists are typically used when data needs to be accessed but hardly ever manipulated, handled, or updated. Within Jigx , we have ensured that static data is easily specified but also accessed with the same ease. Static data can be configured as a direct data source on a jig or as a global datasource that can be accessed or referenced across various jigs or components.

## Configuration options

When setting up a `static datasource` component within a Jig you have the option to use them in various ways:

1. As a locally configured data source within a jig for locally stored data to be available
2. As a global data source that allows easy access and reusability to the data across various jigs and components

{% hint style="info" %}
You also have the option to set up static data directly in the relevant fields. This scenario is however not discussed here as this section focuses only on the application of the static data component itself. Please refer to the guide on working with [Static Data](static.md) for more information on the alternative application.
{% endhint %}

## Examples and code snippets

View common uses for the static datasource below and how you can configure the same in your solution (links to examples are available in the relevant examples).

We've gone ahead and expanded the first one for you. Feel free to view any others you'd like to inspect.

#### Static datasource configured locally on a jig

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/Static-list.png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
Below is an example of static data that has been configured locally.

**Examples**: See the full example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/static-data/simple-list-sd-local.jigx%22)&#x20;
{% endcolumn %}
{% endcolumns %}

{% code title="static-data-local-jig" %}
```yaml
datasources:
  repair_services_static:
    type: datasource.static
    options:
      data:
        - id: 1
          description: Installation or repairs for doors. Doors to be provided by client
          hourlyRate: 70
          illustration: http://clipart-library.com/data_images/436224.png
          image: https://images.unsplash.com/photo-1500281781950-6cd80847ebcd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1469&q=80
          materials: false
          service: Door Installation/Repair
          time: 60       
        - id: 3
          description: Installation or repairs of tiled surfaces. Tiles have to be provided by client
          hourlyRate: 110
          illustration: http://clipart-library.com/images/kcKnbzbXi.jpg
          image: https://images.unsplash.com/photo-1523413184730-e85dbbd04aba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80
          materials: false
          service: Tile Installation/Repair
          time: 120
        - id: 5
          description: Repairs to bathroom rails, toilets, etc
          hourlyRate: 90
          illustration: http://clipart-library.com/new_gallery/53-530190_black-and-white-toilet-png.png
          image: https://images.unsplash.com/photo-1585313647787-7a061b5a85a6?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1423&q=80
          materials: true
          service: Bathroom Repairs
          time: 60
        - id: 6
          description: Painting as required. Paint and tools not provided 
          hourlyRate: 70
          illustration: http://clipart-library.com/img/853166.jpg
          image: https://images.unsplash.com/photo-1562259949-e8e7689d7828?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1431&q=80
          materials: false
          service: Painting Services
          time: 120

data: =@ctx.datasources.repair_services_static
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.description
```
{% endcode %}

#### Static datasource configured globally on a jig

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/static-global-list.png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
Below is an example of static data that has been configured globally along with the example of where this is being referenced.

**Examples**: See the full example of static datasource in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx) See the full example of the list using this global static datasource in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/static-data/simple-list-sd-global.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="global-static-datasource.-jig" %}
```yaml
type: datasource.static
options:
  data:
    - id: 1
      description: Installation or repairs for doors. Doors to be provided by client
      hourlyRate: 70
      illustration: http://clipart-library.com/data_images/436224.png
      image: https://images.unsplash.com/photo-1500281781950-6cd80847ebcd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1469&q=80
      materials: false
      service: Door Installation/Repair
      time: 60
    - id: 2
      description: Repairs to door handles 
      hourlyRate: 40
      illustration: http://clipart-library.com/img1/1332215.jpg
      image: https://images.unsplash.com/photo-1538766017398-415434a31a5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
      materials: true
      service: Door Handle/Lock Repairs
      time: 60        
    - id: 3
      description: Installation or repairs of tiled surfaces. Tiles have to be provided by client
      hourlyRate: 110
      illustration: http://clipart-library.com/images/kcKnbzbXi.jpg
      image: https://images.unsplash.com/photo-1523413184730-e85dbbd04aba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80
      materials: false
      service: Tile Installation/Repair
      time: 120
```
{% endtab %}

{% tab title="referenced-data-jig" %}
```yaml
data: =@ctx.datasources.repair_services_static
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.description
```
{% endtab %}
{% endtabs %}

#### Static datasource configured inside a component

You can also create static data right inside your component or as an `initialValue`, without a need to specify the datasource.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/static-dropdown.png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
In this example static data is used to create the data need for selection in the `component.dropdown`. \
**Example:**\
See the full code sample on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-static-data/static-datasource/static-list.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="dropdown.jigx" %}
```yaml
title: Dropdown with values
type: jig.default

datasources:
  employees-list: 
    type: datasource.static
    options:
      data:
        - title: 'Jane Stevens'
          value: 'Jane'
        - title: 'Mark Anders'
          value: 'Mark'
        - title: 'Haley Marshall'
          value: 'Haley'
        - title: 'Andre Marks'
          value: 'Andre'
  
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown
          options:
            data: =@ctx.datasources.employees-list
            label: Dropdown with Employees
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.title
                value: =@ctx.current.item.value
```
{% endcode %}

#### Static datasource configured inside a dropdown component

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/static-list-data.png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
In this example static data is defined and used in the `component.list-item`.\


**Example:**\
See the code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/people.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="list.jigx" %}
```yaml
title: List
type: jig.list
icon: contact 

data: "=[{'name':'Jane Stevens','position':'Worker','initials':'JS'},
      {'name':'Peter Marks','position':'Designer','initials':'PM'},
      {'name':'Garry Marks','position':'Worker','initials':'GM'}]"
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.position
    leftElement: 
      element: avatar
      text: =@ctx.current.item.initials
```
{% endcode %}

## See also

* [Related Items (GitHub)](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/datasources)
