# product-item



{% columns %}
{% column %}
The product item component is suitable for a list of products and should be used with the [list components](../list.md) or the [list jig](<../../Jig Types/jig_list.md>).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ydImhfWqF3Ei8FmcgBdc6\_product-item.png" size="78" position="center" caption="Product Item Preview" alt="Product Item Preview" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ydImhfWqF3Ei8FmcgBdc6\_product-item.png" width="800" height="536" darkWidth="800" darkHeight="536"}&#x20;
{% endcolumn %}
{% endcolumns %}

### Configuration options

Some properties are common to all components, see [Common component properties](product-item.md) for a list and their configuration options.

<table><thead><tr><th width="205.8046875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Add a <code>title</code> for the for the product-item. You can use an expression and datasource to set the title.</td></tr></tbody></table>

<table><thead><tr><th width="206.81640625">Other options</th><th></th></tr></thead><tbody><tr><td><code>amountControl</code></td><td><p>This property has several setup options:</p><ul><li><code>initialValue</code></li><li><code>minimum</code> - Set a minimum limit to the number that can be selected. Default is 0.</li><li><code>maximum</code> - Set a maximum limit to the number that can be selected.</li><li><code>step</code> - Set the increments/decrement. Default is 1.</li><li><code>value</code> - Value of amount control.</li><li><code>onChange</code> action - will be triggered when value is changed.</li><li><code>onDelete</code> action - A trash symbol is displayed when the value is 1 or (min + 1).</li></ul></td></tr><tr><td><code>discount</code></td><td>This allows you to display the discount price including the currency. Set the discount in the range 0 - 1 (1 = 100%). Discount is set in float format e.g. 0.12.</td></tr><tr><td><code>image</code></td><td>The option to add an image of your product by providing the <code>uri</code></td></tr><tr><td><code>price</code></td><td>This allows you to display the base price of the product including the currency.</td></tr><tr><td><code>style</code></td><td><code>isWaitingSync</code> - Displays a Waiting sync indicator.</td></tr><tr><td><code>tag</code></td><td>The option to add a tag to your item. Add a tag title for example max amount, the tag can be configured with an expression to determine when it should be displayed. <code>tag: =@ctx.current.state.amount =10 ? 'max amount':''</code></td></tr></tbody></table>

<table><thead><tr><th width="207.2421875">Actions</th><th></th></tr></thead><tbody><tr><td><code>onPress</code></td><td>The action is triggered while pressing on a product item in the list. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="208.36328125">State Configuration</th><th width="125.23828125">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.current.state.</code></td><td>amount</td><td>Applies to a list, list.item, product-item, and stage components. List's data is an array of records. The <code>=@ctx.current.state</code> is the state of the current object in the array.</td></tr><tr><td><code>=@ctx.component.state.</code></td><td>amount</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

### Examples and code snippets

#### Simple product-item with tags

{% columns %}
{% column %}
&#x20;In this example, a simple list containing a product-item component is shown. Each product contains a title, tag, image, and price. The discount property calculates the price after the discount.

**Examples:** See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-tags-dynamic.jigx).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/didhCaT9vWYQmsSdxiZXT\_cc-product-item-simple.PNG" size="80" position="center" caption="Product-item with tags" alt="Product-item with tags" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/didhCaT9vWYQmsSdxiZXT\_cc-product-item-simple.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="product-item-tags-dynamic" %}
```yaml
title: Product item list
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1498049794561-7780e7231661?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OXx8dGVjaG5vbG9neSUyMHByb2R1Y3RzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
        title: Product item
        subtitle: List with product item

data: =@ctx.datasources.product
item:
  type: component.product-item
  options:
    title: =@ctx.current.item.title
    image:
      uri: =@ctx.current.item.uri
    discount: =@ctx.current.item.discount
    price:
      value: =@ctx.current.item.price
      format:
        numberStyle: currency
    tag: =@ctx.current.item.tag
```
{% endtab %}

{% tab title="datasource (dynamic)" %}
```yaml
datasources:
  product:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/products
      query: |
        SELECT 
          id, 
          '$.title', 
          '$.uri',
          '$.tag', 
          '$.price',
          '$.discount', 
          '$.quantity',
          '$.category',
          '$.productId'
        FROM [default/products]
        WHERE '$.category' = "product" ORDER BY '$.title'          
```
{% endtab %}
{% endtabs %}

#### Product-item with onChange, amountControl and search

{% columns %}
{% column %}
&#x20;![Product-item](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/sCr2-5Hh2_2y2q4BwUcBl_prodiphone13blueportrait.png)
{% endcolumn %}

{% column %}
&#x20;In this example, a simple list containing a product-item component is shown. Each product contains a title, tag, image, amountControl, and price. The added advantage is that you can search the list making it suitable for a larger number of products. The discount property calculates the price after the discount.

**Examples:** See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-example/product-item-example-dynamic.jigx).

**Datasource:** See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-example/product-item-example-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title=" product-item-example- dynamic" %}
```yaml
data: =@ctx.datasources.product
isSearchable: true
item: 
  type: component.product-item
  options:
    tag: =@ctx.current.state.amount =10 ? 'max amount':''
    title: =@ctx.current.item.title
    image:
      uri: =@ctx.current.item.uri
    discount: =@ctx.current.item.discount
    price:
      value: 
        =@ctx.component.state.amount = 0 ? @ctx.current.item.price :(@ctx.component.state.amount * $number(@ctx.current.item.price))
      format:
        numberStyle: currency
    amountControl:
      initialValue: =$number(@ctx.current.item.quantity)
      maximum: 10
      onChange:
        type: action.execute-entity
        options:
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/products
          method: update
          data:
            id: =@ctx.current.item.id
            quantity: =@ctx.current.state.amount
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  product:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/products
      query: |
        SELECT 
          id, 
          '$.title', 
          '$.uri',
          '$.tag', 
          '$.price',
          '$.discount', 
          '$.quantity',
          '$.category',
          '$.productId'
        FROM [default/products] WHERE '$.title' LIKE '%'||@search||'%' AND '$.category' = "product" OR @search IS NULL AND '$.category' = "product" ORDER BY '$.title'
      queryParameters:
        search: =@ctx.jig.state.searchText
```
{% endtab %}
{% endtabs %}

#### Product-item with summary

{% columns %}
{% column %}
In this example, a list containing a product-item component is shown. Each product contains a title, image, and price. The discount property calculates the price after the discount. The summary component at the bottom shows the total of items selected in the amountControl.

**Examples:** See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/static-data/product-item-summary-static.jigx).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/V6T6Og9SB2WN43MPrH8Dw\_cc-productitemsummary.PNG" size="80" position="center" caption="Product-item with summary" alt="Product-item with summary" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/V6T6Og9SB2WN43MPrH8Dw\_cc-productitemsummary.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="product-item-summary-static" %}
```yaml
title: Product item and summary
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1498049794561-7780e7231661?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OXx8dGVjaG5vbG9neSUyMHByb2R1Y3RzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
        title: Product item and summary
        subtitle: List with product item and summary

data: =@ctx.datasources.product-item1
item:
  type: component.product-item
  options:
    title: =@ctx.current.item.title
    image:
      uri: =@ctx.current.item.uri
    discount: =@ctx.current.item.discount
    price:
      value: =@ctx.component.state.amount = 0 ? @ctx.current.item.price :$sum(@ctx.component.state.amount * @ctx.current.item.price)
      format:
        numberStyle: currency
    amountControl:
      maximum: 10
      initialValue: =@ctx.current.item.amount

summary:
  children:
    type: component.summary
    options:
      layout: cart
      title: Items in your cart
      value: =$sum(@ctx.jig.state.amounts.amount)
```
{% endtab %}

{% tab title="datasource (static)" %}
```yaml
datasources:
  product-item1: 
    type: datasource.static
    options:
      data:
        - id: 1
          title: Title
          uri: https://images.unsplash.com/photo-1618366712010-f4ae9c647dcb?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=776&q=80
          price: 211.96
          discount: 0.1
          amount: 2
        - id: 2
          title: Title
          uri: https://images.unsplash.com/photo-1611850698562-ae3d28934080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
          price: 59.96
          discount:
          amount: 1
        - id: 3
          title: Title
          uri: https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2062&q=80
          price: 191.6
          discount: 0.15
          amount: 0
```
{% endtab %}
{% endtabs %}

### See also

* [State](https://docs.jigx.com/state)
