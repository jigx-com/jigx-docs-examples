# product-item

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The product item component is suitable for a list of products and should be used with the [list components](./../list.md) or the [list jig](<./../../Jig Types/jig_list.md>).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ydImhfWqF3Ei8FmcgBdc6_product-item.png" size="78" position="center" caption="Product Item Preview" alt="Product Item Preview" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ydImhfWqF3Ei8FmcgBdc6_product-item.png" width="800" height="536" darkWidth="800" darkHeight="536"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure** |                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| `title`            | Add a `title` for the for the product-item. You can use an expression and datasource to set the title. |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="149">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>amountControl</code></p>
    </td>
    <td selected="false" align="left">
      <p>This property has several setup options:</p>
      <ul>
      <li><code>initialValue</code></li>
      <li><code>minimum</code> - Set a minimum limit to the number that can be selected. Default is 0.</li>
      <li><code>maximum</code> - Set a maximum limit to the number that can be selected.</li>
      <li><code>step</code> - Set the increments/decrement. Default is 1.</li>
      <li><code>value</code> - Value of amount control.</li>
      <li><code>onChange</code> action - will be triggered when value is changed.</li>
      <li><code>onDelete</code> action - A trash symbol is displayed when the value is 1 or (min + 1).</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>discount</code></p>
    </td>
    <td selected="false" align="left">
      <p>This allows you to display the discount price including the currency. Set the discount in the range 0 - 1 (1 = 100%). Discount is set in float format e.g. 0.12.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>image</code></p>
    </td>
    <td selected="false" align="left">
      <p>The option to add an image of your product by providing the <code>uri</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>price</code></p>
    </td>
    <td selected="false" align="left">
      <p>This allows you to display the base price of the product  including the currency.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>isWaitingSync</code> - Displays a Waiting sync indicator.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>tag</code></p>
    </td>
    <td selected="false" align="left">
      <p>The option to add a tag to your item. Add a tag title for example max amount, the tag can be configured with an expression to determine when it should be displayed.
      <code>tag: =@ctx.current.state.amount =10 ? 'max amount':''</code></p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="145">
  <tr>
    <td selected="false" align="left">
      <p><strong>Actions</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p>The action is triggered while pressing on a product item in the list. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218,121">
  <tr>
    <td selected="false" align="left">
      <p><strong>State Configuration</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Key</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Notes</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.current.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>amount</p>
    </td>
    <td selected="false" align="left">
      <p>Applies to a list, list.item, product-item, and stage components. List's data is an array of records. The <code>=@ctx.current.state</code> is the state of the current object in the array.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.component.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>amount</p>
    </td>
    <td selected="false" align="left">
      <p>State is the variable of the component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>activeItemId
      now</p>
    </td>
    <td selected="false" align="left">
      <p>Global state variable that can be used throughout the solution.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Simple product-item with tags

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, a simple list containing a product-item component is shown. Each product contains a title, tag, image, and price.  The discount property calculates the price after the discount.

**Examples:**
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-tags-dynamic.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/didhCaT9vWYQmsSdxiZXT_cc-product-item-simple.PNG" size="80" position="center" caption="Product-item with tags" alt="Product-item with tags" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/didhCaT9vWYQmsSdxiZXT_cc-product-item-simple.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
:::
::::

:::CodeblockTabs
product-item-tags-dynamic

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

datasource (dynamic)

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
:::
:::::

:::::ExpandableHeading
### Product-item with onChange, amountControl and search

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Product-item](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/sCr2-5Hh2_2y2q4BwUcBl_prodiphone13blueportrait.png "Product-item with search")
:::

:::VerticalSplitItem
In this example, a simple list containing a product-item component is shown. Each product contains a title, tag, image, amountControl, and price. The added advantage is that you can search the list making it suitable for a larger number of products. The discount property calculates the price after the discount.

**Examples:**
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-example/product-item-example-dynamic.jigx).

**Datasource:**
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-example/product-item-example-dynamic.jigx).
:::
::::

:::CodeblockTabs
product-item-example- dynamic

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

datasources (dynamic)

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
:::
:::::

:::::ExpandableHeading
### Product-item with summary

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, a list containing a product-item component is shown. Each product contains a title, image, and price. The discount property calculates the price after the discount. The summary component at the bottom shows the total of items selected in the amountControl.

**Examples:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/static-data/product-item-summary-static.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/V6T6Og9SB2WN43MPrH8Dw_cc-productitemsummary.PNG" size="80" position="center" caption="Product-item with summary" alt="Product-item with summary" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/V6T6Og9SB2WN43MPrH8Dw_cc-productitemsummary.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
:::
::::

:::CodeblockTabs
product-item-summary-static

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

datasource (static)

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
:::
:::::

## See also

- [State](https://docs.jigx.com/state)

