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
  tags:
    visible: true
  actions:
    visible: true
---

# summary

{% columns %}
{% column width="50%" %}
Summarize the information in the jig at the bottom of the screen using the summary component. For example, a count of the number orders, or the number of items in a cart for an online shopping app.

The summary is fixed and displays even when the screen is scrolled. Make the summary actionable by combining it with an [action](../Actions/).
{% endcolumn %}

{% column width="50%" %}
![Summary](../../.gitbook/assets/summary-intro.png)
{% endcolumn %}
{% endcolumns %}

## Configuration options

{% include "../../.gitbook/includes/common-component-properties.md" %}

<table><thead><tr><th width="151.33984375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>layout</code></td><td><p>There are three types to choose from:</p><ol><li><code>default</code> - used to display information. This is the default layout, allowing you to specify what must be shown.</li><li><code>cart</code> - useful for an online shopping app to show the number of items in a cart. The <code>value</code> is shown to the right of the <code>title</code>.</li><li><code>counter</code> - useful for showing a count, for example, the number of sales made in a month. The <code>value</code> is shown to the left of the <code>title</code>.</li><li><code>progress</code> - useful for displaying completion or status over time, such as task progress, goals, or performance metrics. The value is shown as a visual progress indicator. </li></ol></td></tr><tr><td><code>title</code></td><td>The main text to display on the component.</td></tr></tbody></table>

<table><thead><tr><th width="145.49609375">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>Changing color of <code>title</code> and <code>leftIcon</code> based on <code>when</code> conditions. First condition evaluated to <code>true</code> will be used. If the condition evaluates to <code>false</code> the default color (black) is used. Choose a color from the provided color palette as well as the status colors, e.g. <code>isWarning</code>. Default color is black if the property is not specified in the YAML. See the list of available colors in .</td></tr><tr><td><code>description</code></td><td>Provide third level of supporting text to be displayed. The position of the text is under the <code>subtitle</code> property. This property is only available with <code>layout</code> type <code>cart</code>.</td></tr><tr><td><code>leftIcon</code></td><td>Add an icon to show on the left before the <code>title</code>. A list of icons is available. See for more information. <code>leftIcon</code> is only available with the <code>default</code> layout.</td></tr><tr><td><code>steps</code></td><td>The number of steps in the progress bar or an expression that must equal a number.</td></tr><tr><td><code>subtitle</code></td><td>Provide supporting text to be displayed as a <code>subtitle</code>. The position of the subtitle text depends on the selected <code>layout</code> property.</td></tr><tr><td><code>value</code></td><td>The actual value in your summary configured by a string or an expression that must equal a number. This property is only available for <code>layout</code> types <code>cart</code>, <code>counter</code>, and <code>progress</code>.<br>- <code>current</code>: The current value of the progress bar.</td></tr></tbody></table>

<table><thead><tr><th width="146.0390625">Actions</th><th></th></tr></thead><tbody><tr><td><code>OnPress</code></td><td>The action is triggered while pressing on the <code>LeftIcon</code> in the summary. Use IntelliSense (ctrl+space) to see the available list of actions.</td></tr><tr><td><a href="../Actions/">Actions</a></td><td>By using the summary component along with actions, you can unlock a powerful feature that enables you to take necessary actions based on the information available from the summary. For instance, adding a sales opportunity. This feature can significantly enhance the usability of your jig and make it more efficient.</td></tr></tbody></table>

## Consideration

* The summary component is available on all [Jig Types](<../Jig Types/Jig Types.md>).
* To show an empty `title` use `title: ' '`.
* To format the `value` property, for example, adding a currency symbol in front of the value or percentage behind the value, use the `Text with Format` option available in IntelliSense (ctrl+space).
* Only numbers can be shown in the `value` property.
* If the `value` property exceeds 100 a default 99+ will be displayed in the property.
* Enhance the usability of your jig and make it more efficient by using the summary component along with an [action](../Actions/).
* **Working with Parent and Child Actions and Summaries:** When configuring `actions` or `summary` buttons across parent and child jigs, the following behavior applies:
  * If both the parent and child jigs have an `action` or `summary` configured, the child’s configuration takes precedence and overrides the parent’s.
  * If only the parent has an `action` or `summary`, it automatically applies to the child.
  * If only the child has an `action` or `summary`, it is used in the parent jig as well.

## Examples and code snippets

### Summary - default

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/summary-default.png" alt="Default layout" width="188"><figcaption><p>Default layout</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example the `default` layout property is used to show a `title` with a cart as a `leftIcon`.

**Example**: The full example is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="summary" %}
```yaml
title: Products
type: jig.list

# Add the summary showing an icon with default layout.  
summary:
  children:
    type: component.summary
    options:
      title: Your cart is empty
      layout: default
      leftIcon:
        element: icon
        icon: shopping-cart-empty-1
        
data: =@ctx.datasources.products
item:
  type: component.product-item
  options:
    title: =@ctx.current.item.title
    discount: =@ctx.current.item.discount
    image:
      uri: =@ctx.current.item.uri
    price:
      format:
        numberStyle: currency
      value: =@ctx.current.item.price
    tag: =@ctx.current.item.tag
```
{% endcode %}

### Summary - cart

{% columns %}
{% column %}
n this example the `cart` layout property is used in a `jig.list` with a `product-item` component to show the number of products in the cart. Notice the number of items in the cart is shown in a circle on the right of the `title`.\
**Example**:\
The full example of the summary type: cart using product-item is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-cart.jigx).\
The full example of the summary type: cart using expander is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-cart-expander.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/summary-Cart layout.png" alt="Cart layout" width="188"><figcaption><p>Cart layout</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="summary-cart-product-item" %}
```yaml
title: Products
type: jig.list

# Add the summary to show there are two products available using a cart layout.  
summary:
  children:
    type: component.summary
    options:
      title: "Items in cart:"
      layout: cart
      value: 2
      
data: =@ctx.datasources.products
item:
  type: component.product-item
  options:
    title: =@ctx.current.item.title
    discount: =@ctx.current.item.discount
    image:
      uri: =@ctx.current.item.uri
    price:
      format:
        numberStyle: currency
      value: =@ctx.current.item.price
    tag: =@ctx.current.item.tag
```
{% endtab %}

{% tab title="summary-cart-expander" %}
```yaml
title: Flights
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1490430657723-4d607c1503fc?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8ZmxpZ2h0c3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60
 
# Add the summary to show there are three flight available using a cart layout. 
summary:
  children:
    type: component.summary
    options: 
      layout: cart
      title: "Flights found:"
      value: 3
        
data: =@ctx.datasources.flight-schedule-static
item:
  type: component.expander
  options:
    header:
      centerElement: 
        type: component.stage
        options:
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.disembark
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.board
    children:
      - type: component.entity
        options:
          children:
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Boarding
                      value: =@ctx.current.item.from
                  - type: component.entity-field
                    options:
                      label: Destination
                      value: =@ctx.current.item.to
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Board Time
                      value: =@ctx.current.item.board
                  - type: component.entity-field
                    options:
                      label: Disembark Time
                      value: =@ctx.current.item.disembark
            - type: component.entity-field
              options:
                label: Passenger
                value: =@ctx.current.item.name
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Flight
                      value: =@ctx.current.item.flight
                  - type: component.entity-field
                    options:
                      label: Gate
                      value: =@ctx.current.item.gate
                  - type: component.entity-field
                    options:
                      label: Seat
                      value: =@ctx.current.item.seat
      - type: component.location
        options:
          viewPoint:
            centerPosition: middle
            address: =@ctx.current.item.to         
```
{% endtab %}

{% tab title="datasources 1 (static)" %}
```yaml
datasources:
  products:
    type: datasource.static
    options:
      data:
        - title: Headphones WH-1000XM4
          uri: https://images.unsplash.com/photo-1618366712010-f4ae9c647dcb?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=776&q=80
          tag: free transport 
          price: 211.96
          discount: 0.10
        - title: Bluetooth speaker Charge 5
          uri: https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2062&q=80
          tag: in stock
          price: 191.6
          discount: 0.15
        - title: M1 Bluetooth Wireless Mouse
          uri: https://images.unsplash.com/photo-1611850698562-ae3d28934080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          tag: in stock
          price: 59.96
          discount:
        - title: Wireless headphones T3S
          uri: https://images.unsplash.com/photo-1578319439584-104c94d37305?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          tag: in stock
          price: 84.3
          discount: 0.10
        - title: Multifunction charging station
          uri: https://images.unsplash.com/photo-1587749091230-fb8a034d695c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1160&q=80
          tag: in stock
          price: 71.08
          discount:
```
{% endtab %}

{% tab title="datasources 2 (static)" %}
```yaml
datasources:
  flight-schedule-static:
    type: datasource.static
    options:
      data: 
        - id: 1
          airline: Get Stuff Done Airlines
          board: 11:30
          disembark: 12:30
          date: 30 Jul
          flight: A 0123
          from: Hawaii
          fromabrv: HNL
          gate: 16
          name: July Nelson
          seat: 12F
          to: New York
          toabrv: JFK
          image: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 2
          airline: Get Stuff Done Airlines
          board: 08:10
          disembark: 10:45
          date: 30 Jul
          flight: A 5738
          from: Phoenix
          fromabrv: PHX
          gate: 2
          name: Nora Gordon
          seat: 27A
          to: Alabama
          toabrv: MCZ
          image: https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 3
          airline: Get Stuff Done Airlines
          board: 14:00
          disembark: 19:59
          date: 30 Jul
          flight: A 1123
          from: Iowa
          fromabrv: DSM
          gate: 15
          name: Tracy Matthews
          seat: 13F
          to: Columbus, Ohio, US
          toabrv: DAY
          image: https://images.unsplash.com/photo-1488085061387-422e29b40080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTN8fHBsYW5lfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
```
{% endtab %}
{% endtabs %}

### Summary - counter

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/summary-Counter layout.png" alt="Counter layout" width="188"><figcaption><p>Counter layout</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this example the `counter` layout property is used in a `jig.list` with a `product-item` component to show the number of products in the cart. Notice the number of products is show on the left of the `title`.

**Example**:\
The full example of the summary type: counter using product-item is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-counter.jigx). The full example of the summary type: counter using expander is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-counter-expander.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="summary-counter-product-item" %}
```yaml
title: Products
type: jig.list
# Add the summary to show there are two items.  
summary:
  children:
    type: component.summary
    options:
      title: Items in cart
      layout: counter
      value: 2
      
data: =@ctx.datasources.products
item:
  type: component.product-item
  options:
    title: =@ctx.current.item.title
    discount: =@ctx.current.item.discount
    image:
      uri: =@ctx.current.item.uri
    price:
      format:
        numberStyle: currency
      value: =@ctx.current.item.price
    tag: =@ctx.current.item.tag
```
{% endtab %}

{% tab title="summary-counter-expander" %}
```yaml
title: Today's Flights
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1490430657723-4d607c1503fc?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8ZmxpZ2h0c3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60
 
 # Add the summary to show there are three flight options available. 
summary:
  children:
    type: component.summary
    options:
      title: Flights found
      layout: counter
      value: 3
            
data: =@ctx.datasources.flight-schedule-static
item:
  type: component.expander
  options:
    header:
      centerElement:
        type: component.stage
        options:
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.board
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.disembark
        
    children:
      - type: component.entity
        options:
          children:
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Boarding
                      value: =@ctx.current.item.from
                  - type: component.entity-field
                    options:
                      label: Destination
                      value: =@ctx.current.item.to 
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Board Time
                      value: =@ctx.current.item.board  
                  - type: component.entity-field
                    options:
                      label: Disembark Time
                      value: =@ctx.current.item.disembark  
            - type: component.entity-field
              options:
                label: Passenger
                value: =@ctx.current.item.name
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Flight
                      value: =@ctx.current.item.flight
                  - type: component.entity-field
                    options:
                      label: Gate
                      value: =@ctx.current.item.gate
                  - type: component.entity-field
                    options:
                      label: Seat
                      value: =@ctx.current.item.seat   
      - type: component.location
        options:
          viewPoint:
            centerPosition: middle
            address: =@ctx.current.item.to
```
{% endtab %}

{% tab title="datasources 1 (static)" %}
```yaml
datasources:
  products:
    type: datasource.static
    options:
      data:
        - title: Headphones WH-1000XM4
          uri: https://images.unsplash.com/photo-1618366712010-f4ae9c647dcb?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=776&q=80
          tag: free transport 
          price: 211.96
          discount: 0.10
        - title: Bluetooth speaker Charge 5
          uri: https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2062&q=80
          tag: in stock
          price: 191.6
          discount: 0.15
        - title: M1 Bluetooth Wireless Mouse
          uri: https://images.unsplash.com/photo-1611850698562-ae3d28934080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          tag: in stock
          price: 59.96
          discount:
        - title: Wireless headphones T3S
          uri: https://images.unsplash.com/photo-1578319439584-104c94d37305?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          tag: in stock
          price: 84.3
          discount: 0.10
        - title: Multifunction charging station
          uri: https://images.unsplash.com/photo-1587749091230-fb8a034d695c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1160&q=80
          tag: in stock
          price: 71.08
          discount:
```
{% endtab %}

{% tab title="datasources 2 (static)" %}
```yaml
datasources:
  flight-schedule-static:
    type: datasource.static
    options:
      data: 
        - id: 1
          airline: Get Stuff Done Airlines
          board: 11:30
          disembark: 12:30
          date: 30 Jul
          flight: A 0123
          from: Hawaii
          fromabrv: HNL
          gate: 16
          name: July Nelson
          seat: 12F
          to: New York
          toabrv: JFK
          image: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 2
          airline: Get Stuff Done Airlines
          board: 08:10
          disembark: 10:45
          date: 30 Jul
          flight: A 5738
          from: Phoenix
          fromabrv: PHX
          gate: 2
          name: Nora Gordon
          seat: 27A
          to: Alabama
          toabrv: MCZ
          image: https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 3
          airline: Get Stuff Done Airlines
          board: 14:00
          disembark: 19:59
          date: 30 Jul
          flight: A 1123
          from: Iowa
          fromabrv: DSM
          gate: 15
          name: Tracy Matthews
          seat: 13F
          to: Ohio
          toabrv: DAY
          image: https://images.unsplash.com/photo-1488085061387-422e29b40080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTN8fHBsYW5lfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
```
{% endtab %}
{% endtabs %}

### Summary with action

{% columns %}
{% column %}
In this example the `cart` layout property is used in a `jig.list` with the `expander` component to show the number of available flights. A `go-to` action is added to take you to book a flight.

**Example**: The full example is on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-cart-action.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/summaryaction.png" alt="Summary with action" width="188"><figcaption><p>Summary with action</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="summary-cart-action" %}
```yaml
title: Flights
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1490430657723-4d607c1503fc?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8ZmxpZ2h0c3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60

# Add the summary to show there are three flight options available.
summary:
  children:
    type: component.summary
    options: 
      layout: counter
      value: 3
      title: "Flights found:"
                
data: =@ctx.datasources.flight-schedule-static
item:
  type: component.expander
  options:
    header:
      centerElement: 
        type: component.stage
        options:
          right:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.board
          left:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.disembark 
    children:
      - type: component.entity
        options:
          children:
            - type: component.entity-field
              options:
                label: Boarding
                value: =@ctx.current.item.from
            - type: component.entity-field
              options:
                  label: Destination
                  value: =@ctx.current.item.to
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Board Time
                      value: =@ctx.current.item.board
                  - type: component.entity-field
                    options:
                        label: Disembark Time
                        value: =@ctx.current.item.disembark 
                  - type: component.entity-field
                    options:
                      label: Passenger
                      value: =@ctx.current.item.name
            - type: component.field-row
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Flight
                      value: =@ctx.current.item.flight 
                  - type: component.entity-field
                    options:
                        label: Gate
                        value: =@ctx.current.item.gate
                  - type: component.entity-field
                    options:
                        label: Seat
                        value: =@ctx.current.item.seat    
      - type: component.location
        options:
            viewPoint:
                address: =@ctx.current.item.to  

# Use the go-to action to navigate to a jig to book a flight.    
actions:
  - children:
      - type: action.go-to
        options:
          title: Book a flight
          linkTo: expander-trip 
```
{% endtab %}

{% tab title="datasource" %}
```yaml
type: datasource.static
options:
  data: 
    - id: 1
      airline: Get Stuff Done Airlines
      board: 11:30
      disembark: 12:30
      date: 30 Jul
      flight: A 0123
      from: Hawaii
      fromabrv: HNL
      gate: 16
      name: July Nelson
      seat: 12F
      to: New York
      toabrv: JFK
      image: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
    - id: 2
      airline: Get Stuff Done Airlines
      board: 08:10
      disembark: 10:45
      date: 30 Jul
      flight: A 5738
      from: Phoenix
      fromabrv: PHX
      gate: 2
      name: Nora Gordon
      seat: 27A
      to: Alabama
      toabrv: MCZ
      image: https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
    - id: 3
      airline: Get Stuff Done Airlines
      board: 14:00
      disembark: 19:59
      date: 30 Jul
      flight: A 1123
      from: Iowa
      fromabrv: DSM
      gate: 15
      name: Tracy Matthews
      seat: 13F
      to: Columbus, Ohio, US
      toabrv: DAY
      image: https://images.unsplash.com/photo-1488085061387-422e29b40080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTN8fHBsYW5lfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60 
```
{% endtab %}
{% endtabs %}

### Summary - progress in a form

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/summary-progress-form.gif" alt="Summary showing progress" width="188"><figcaption><p>Summary showing progress</p></figcaption></figure>
{% endcolumn %}

{% column %}
This example defines a **summary component** that visually tracks a user's progress through a **3-step purchase order form**. It acts as a progress indicator, giving users real-time feedback on how far along they are in completing the order process. The component monitors three separate forms (`form1`, `form2`, `form3`) and evaluates whether each one has been successfully validated. Based on this, it calculates a current progress score between **0 and 3**, which is then displayed as a progress bar.

**Examples:**

See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-progress.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="summary-progress-form.jigx" %}
```yaml
title: Order Form
type: jig.default
isHomeButtonVisible: false
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1581094271901-8022df4466f9?w=400

children:
  - type: component.form
    instanceId: form1
    options:
      # isDiscardChangesAlertEnabled: false
      children:
        # Customer Information Expander
        - type: component.expander
          instanceId: customerInfo
          options:
            header:
              centerElement:
                type: component.titles
                options:
                  title: Customer Information
            children:
              - type: component.text-field
                instanceId: customerName
                options:
                  label: Customer Name
                  isRequired: true

              - type: component.email-field
                instanceId: customerEmail
                options:
                  label: Email Address
                  isRequired: true

              - type: component.text-field
                instanceId: customerPhone
                options:
                  label: Phone Number
                  isRequired: true
                  keyboardType: phone-pad

              - type: component.text-field
                instanceId: serviceAddress
                options:
                  label: Service Address
                  isRequired: true
                  helperText: Enter complete address
                  isMultiline: true

        # Equipment Details Expander
  - type: component.form
    instanceId: form2
    options:
      # isDiscardChangesAlertEnabled: false
      children:
        - type: component.expander
          instanceId: equipInfo
          options:
            header:
              centerElement:
                type: component.titles
                options:
                  title: Equipment Details

            children:
              - type: component.dropdown
                instanceId: equipmentType
                options:
                  data: =@ctx.datasources.equipment
                  label: Equipment Type
                  item:
                    type: component.dropdown-item
                    options:
                      title: =@ctx.current.item.title
                      value: =@ctx.current.item.value
                  isRequired: true

              - type: component.text-field
                instanceId: modelNumber
                options:
                  label: Model Number

              - type: component.number-field
                instanceId: quantity
                options:
                  label: Quantity
                  isRequired: true
                  minimum: 1

        # Installation Details Expander
  - type: component.form
    instanceId: form3
    options:
      # isDiscardChangesAlertEnabled: false
      children:
        - type: component.expander
          instanceId: installInfo
          options:
            header:
              centerElement:
                type: component.titles
                options:
                  title: Installation Details

            children:
              - type: component.choice-field
                instanceId: installationRequired
                options:
                  data: =@ctx.datasources.installation
                  item:
                    type: component.choice-field-item
                    options:
                      title: =@ctx.current.item.title
                      value: =@ctx.current.item.title
                  label: Installation required?

              - type: component.date-picker
                instanceId: preferredInstallDate
                options:
                  label: Preferred Installation Date
# Summary component displays a progress tracker for a multi-step.
summary:
  children:
   # Define the component type.
    type: component.summary
    # Unique identifier for the component instance, 
    # used to reference it in expressions.
    instanceId: progressSummary
    options:
      # Use the 'progress' layout style to display a progress bar/indicator.
      layout: progress
      value:
        # Dynamically calculate the current step based on form validation states:
        # - Returns 3 if form3 is valid (all 3 steps complete)
        # - Returns 2 if form2 is valid (2 steps complete)
        # - Returns 1 if form1 is valid (1 step complete)
        # - Returns 0 if no forms are valid (no steps complete)
        current: =@ctx.components.form3.state.isValid ? 3 :@ctx.components.form2.state.isValid ? 2 :@ctx.components.form1.state.isValid ?1 :0
        # Total number of steps in the purchase order process.
        max: 3
      # Color theme applied to the progress indicator.  
      color: color1
      # Display size of the summary component.
      size: small
      # Label shown above or with the progress indicator.
      title:
        value:
          text: Purchase order progress
          # Style the title.
          fontSize: regular
          isBold: true
        align: center
        # Position the title above the progress indicator.
        position: top
actions:
  - numberOfVisibleActions: 2
    style:
      isDisabled: =$not(@ctx.components.form1.state.isValid and @ctx.components.form2.state.isValid and @ctx.components.form3.state.isValid)
    children:
      - type: action.action-list
        options:
          title: Place order
          isSequential: true
          actions:
            - type: action.submit-form
              options:
                formId: form1
                provider: DATA_PROVIDER_LOCAL
                entity: order
                method: create
            - type: action.submit-form
              options:
                formId: form2
                provider: DATA_PROVIDER_LOCAL
                entity: order
                method: create
            - type: action.submit-form
              options:
                formId: form3
                provider: DATA_PROVIDER_LOCAL
                entity: order
                method: create
                onSuccess:
                  type: action.info-modal
                  options:
                    modal:
                      title: Order Placed
                      description: Your order has been successfully placed. We will contact you shortly to confirm the details.
                      buttonText: Close
            - type: action.reset-state
              options:
                state: =@ctx.components.form1.state.data
            - type: action.reset-state
              options:
                state: =@ctx.components.form2.state.data
            - type: action.reset-state
              options:
                state: =@ctx.components.form3.state.data
      - type: action.go-back
        options:
          title: Cancel
          style:
            isSecondary: true

```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  installation:
    type: datasource.static
    options:
      data:
        - id: 1
          title: Yes - Full Installation
          value: full-install
        - id: 2
          title: Yes - Partial Installation
          value: partial-install
        - id: 3
          title: No - Equipment Only
          value: equipment-only
  equipment:
    type: datasource.static
    options:
      data:
        - id: 1
        - title: Air Conditioning Unit
          value: ac-unit
        - id: 2
          title: Furnace
          value: furnace
        - id: 3
          title: Heat Pump
          value: heat-pump
        - id: 4
          title: Boiler
          value: boiler
        - id: 5
          title: Air Handler
          value: air-handler
        - id: 6
          title: Ductwork
          value: ductwork
        - id: 7
          title: Thermostat
          value: thermostat
        - id: 8
          title: Other
          value: other
```
{% endtab %}
{% endtabs %}

### Summary - progress in tabs

{% columns %}
{% column %}
This example defines a **summary component** that visually tracks a user's progress through a 4-step tab-based purchase order workflow. It provides users with a real-time `progress` indicator, clearly showing how far along they are in completing the purchase order process. The component monitors the active tab within the jig (screen) and maps each tab to a corresponding step number.

**Examples:**

See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/summary/summary-progress-tabs.jigx).
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/summary-progress-tabs.gif" alt="Summary showing progress based on tabs" width="188"><figcaption><p>Summary showing progress based on tabs</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="summary-progress-tabs.jigx" %}
```yaml
title: Purchase Order
type: jig.tabs
areTabsScrollable: false

# Specify the jigs that will open in each tab.
children:
  - jigId: customer-detail
    instanceId: customer
    tab:
      type: component.tab-button
      options:
        title: Customer
        icon: people-man-1
  - jigId: order-details
    instanceId: order
    tab:
      type: component.tab-button
      options:
        title: Equipment
        # Add an icon to the tab. The title is diplayed below the icon.
        icon: supply-chain-shipping-fee-included-truck
  - jigId: service-details
    instanceId: services
    tab:
      type: component.tab-button
      options:
        title: Services
        # Add an icon to the tab. The title is diplayed below the icon.
        icon: cog
  - jigId: sign-off
    instanceId: signature
    tab:
      type: component.tab-button
      options:
        title: Sign off
        # Add an icon to the tab. The title is diplayed below the icon.
        icon: signature
# Summary component that displays a progress tracker with 4 steps
summary:
  children:
    # Define the component type as a summary.
    type: component.summary
    options:
      # Use the 'progress' layout style to display a progress bar/indicator
      layout: progress
      value:
      # Dynamically calculate the current step based on the active tab ID:
        # - Returns 1 if the 'customer' tab is active (Step 1: Customer details)
        # - Returns 2 if the 'order' tab is active (Step 2: Order details)
        # - Returns 3 if the 'services' tab is active (Step 3: Services selection)
        # - Returns 4 if the 'signature' tab is active (Step 4: Signature/completion)
        # - Returns 0 if no matching tab is active (default/initial state)
        current: =@ctx.jig.state.activeTabId = 'customer' ? 1 :@ctx.jig.state.activeTabId = 'order' ? 2 :@ctx.jig.state.activeTabId = 'services' ? 3 :@ctx.jig.state.activeTabId = 'signature' ? 4:0
        # Total number of steps in the purchase order process
        max: 4
      color: color7
      size: small
      # Total number of steps to display as markers on the progress bar
      steps: 4
      title:
        # Label displayed with the progress indicator to describe its purpose
        value: Purchase order progress
actions:
  - numberOfVisibleActions: 2
    children:
      - type: action.execute-entity
        options:
          isHidden: =@ctx.jig.state.activeTabId != 'signature'
          title: Submit order
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/purchase-orders
          method: create
          data:
            firstName: =@ctx.jigs.customer.components.firstName.state.value
            lastName: =@ctx.jigs.customer.components.lastName.state.value
            email: =@ctx.jigs.customer.components.email.state.value
            phone: =@ctx.jigs.customer.components.phone.state.value
            company: =@ctx.jigs.customer.components.company.state.value
            address: =@ctx.jigs.customer.components.address.state.value
            poNumber: =@ctx.jigs.order.components.poNumber.state.value
            orderDate: =@ctx.jigs.order.components.orderDate.state.value
            requiredDate: =@ctx.jigs.order.components.requiredDate.state.value
            equipmentType: =@ctx.jigs.order.components.equipmentType.state.selected.value
            quantity: =@ctx.jigs.order.components.quantity.state.value
            unitPrice: =@ctx.jigs.order.components.unitPrice.state.value
            totalPrice: =@ctx.jigs.order.components.totalPrice.state.value
            shippingAddress: =@ctx.jigs.order.components.shippingAddress.state.value
            shippingMethod: =@ctx.jigs.order.components.shippingMethod.state.selected.value
            installationRequired: =@ctx.jigs.services.components.installationRequired.state.selected.value
            preferredInstallDate: =@ctx.jigs.services.components.preferredInstallDate.state.value
            installationNotes: =@ctx.jigs.services.components.installationNotes.state.value
            signatureDate: =@ctx.jigs.signature.components.signatureDate.state.value
            customerSignature: =@ctx.jigs.signature.components.customerSignature.state.value
          style:
            isDisabled: =$not(@ctx.jigs.customer.components.customerForm.state.isValid and @ctx.jigs.order.components.hvacPurchaseOrderForm.state.isValid and @ctx.jigs.services.components.installationForm.state.isValid and @ctx.jigs.signature.components.signOffForm.state.isValid)
          onSuccess:
            type: action.info-modal
            options:
              modal:
                title: Order successfully submitted
                element:
                  type: icon
                  icon: thumb-up-like
                  color: positive
                buttonText: Close

```
{% endtab %}
{% endtabs %}
