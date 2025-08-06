# list

This component is very similar to the [jig.list](<./../Jig Types/jig_list.md>) the only exception is that this list component can be used in a [jig.default](<./../Jig Types/jig_default.md>) with other items, whereas the [jig.list](<./../Jig Types/jig_list.md>) is a jig dedicated to a list only. With this component, you can typically combine a list with other components. Another difference is that [jig.list](<./../Jig Types/jig_list.md>) automatically display lists on the widget, which is not true with lists on a [jig.default](<./../Jig Types/jig_default.md>).

As far as the functionality goes, the same list options are available as with the List Jig where the list itself can either be a list of values with list items or it can be one of the following:

1. [List item](https://docs.jigx.com/examples/list-item)
2. [Bar charts](https://docs.jigx.com/examples/bar-chart)
3. [Expander](https://docs.jigx.com/examples/expander)
4. [Pie charts](https://docs.jigx.com/examples/pie-chart)
5. [Product item](https://docs.jigx.com/examples/product-item)
6. [Stage](./list/stage.md)

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="209">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>data</code></p>
    </td>
    <td selected="false" align="left">
      <p>The items you want to show in the list.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>item</code></p>
    </td>
    <td selected="false" align="left">
      <p>There is a list of components available to use:
      <a href="./charts/bar-chart.md">bar-chart</a>
      <a href="./expander.md">expander</a>
      <a href="./charts/pie-chart.md">pie-chart</a>
      <a href="./list/product-item.md">product-item</a>
      <a href="./list/stage.md">stage</a>
      If you use the list component in a <a href="https://docs.jigx.com/examples/jigcomposite">https://docs.jigx.com/examples/jigcomposite</a> jig.composite  , the maximum number of displayed items is 8. If you set the <code>maximumItemsToRender</code> to a higher number, the rest of the list will display after clicking on the 'Show more' option.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>maximumItemsToRender</code></p>
    </td>
    <td selected="false" align="left">
      <p>The number of items you would like to display in your list.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="210">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>badge</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add a badge to the list that displays on the widget to highlight critical information and capture the user's attention, ensuring key updates or notifications are easily noticeable within the app. The badge can be configured at the root level of the jig file:</p>
      <ul>
      <li>To display as a red dot using the <code>empty</code> value.</li>
      <li>A red dot with a number using an expression to perform a count.
      For example, counting the number of tasks in the list.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>filter</code></p>
    </td>
    <td selected="false" align="left">
      <p>Allows you to create lists filtered by a key/value. Set the filter to open on a specific tab in a list.</p>
      <ul>
      <li><code>initialValue</code> - Predefine the default selected tab for a filter on the list, when opening the jig the default filter tab is displayed.</li>
      <li><code>data</code> -  define the filter tabs using:
      <ul>
      <li><code>title</code> - give the filter a name. The text that will be displayed in the tab, for example, in-stock.</li>
      <li><code>value</code> - The value that the list filter returns. Use the following expressions to return this value:
      - <code>=@ctx.components.my-list.state.filter</code> (for a list in a default jig)
      - <code>=@ctx.jig.state.filter</code> (for a list jig)
      For <code>true/false</code> values that are saved as <strong>boolean</strong> ensure the filter has a <strong>boolean</strong> value.
      For <code>true/false</code> values that are saved as <strong>string</strong> ensure the filter has a <strong>string</strong> value.
      When using the <code>value</code> property for filtering, it's recommended to use simple values such as strings or numbers (e.g., 'today', '7d', '14d'). Avoid using objects, as the filter logic is designed for strict equality checks. Instead, derive complex data like date ranges elsewhere based on the selected value.</li>
      </ul>
      </li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHorizontal</code></p>
    </td>
    <td selected="false" align="left">
      <p>The boolean value that transforms the list into a horizontal one.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isSearchable</code></p>
    </td>
    <td selected="false" align="left">
      <p>The boolean value which allows you to add a search bar on the top of your list.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onShowMorePress</code></p>
    </td>
    <td selected="false" align="left">
      <p>Action to be performed when you press on the <em>show more</em> button. This is <code>type: action.go-to</code> with a <code>linkTo:</code> option.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="219">
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
      <p>amount
      checked</p>
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
      <p>amount
      checked</p>
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

## Considerations

- When using the `value` property for filtering, it's recommended to use simple values such as strings or numbers (e.g., 'today', '7d', '14d'). Avoid using objects, as the filter logic is designed for strict equality checks. Instead, derive complex data like date ranges elsewhere based on the selected value.

## List functionality

::::::ExpandableHeading
### List with Search functionality

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![List with search](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_bTEwNxapZnocXZQDpY_Z_jih8qge9gqguamhh99d6cimg2152iphone13blueportrait.png "List with search")
:::

::::VerticalSplitItem
This example displays the search functionality of a basic list jig that allows you to search a large list  instantly based on certain keywords entered.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-search-sd.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-search-dd.jigx).

:::hint{type="warning"}
By design, search functionality is automatically disabled when using it on a composite jig.
:::

**Datasource:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-search-dd.jigx).
::::
:::::

:::CodeblockTabs
search (static)

```yaml
children:
  - type: component.list
    instanceId: cleaning_serv_items
    options:
      # Data configured to use datasource (static)      
      data: =$filter(@ctx.datasources.repair-services-static, function($v){$contains($string($v.service),$string(@ctx.components.cleaning_serv_items.state.searchText != null ? @ctx.components.cleaning_serv_items.state.searchText:''))})[]
      isSearchable: true
      maximumItemsToRender: 50
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.description
```

search (dynamic)

```yaml
children:
  - type: component.list
    instanceId: cleaning_serv_items
    options:
      # Data configured to use datasource (dynamic)      
      data: =@ctx.datasources.cleaning-services-dynamic
      isSearchable: true
      maximumItemsToRender: 50
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.area
```

datasources (static)

```yaml
datasources:
  repair-services-static:
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
        - id: 4
          description: Installation or repairs of dry-wall surfaces
          hourlyRate: 80
          illustration: http://clipart-library.com/img1/505759.jpg
          image: https://images.unsplash.com/photo-1628901551715-7234d14fb7a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: true
          service: Drywall Installation/Repair
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
        - id: 7
          description: Repairs to fences. Tools and items not included
          hourlyRate: 90
          illustration: http://clipart-library.com/img/18345.gif
          image: https://images.unsplash.com/photo-1583805978118-ba9a81ac1399?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: false
          service: Fence Installation/Repair
          time: 60
        - id: 8
          description: Removal of graffiti and painting. Paint and brushes not included in cost
          hourlyRate: 110
          illustration: http://clipart-library.com/images/6cy5aL5gi.jpg
          image: https://images.unsplash.com/photo-1581850518616-bcb8077a2336?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: false
          service: Removal of Graffiti
          time: 120
        - id: 9
          description: Repairs to cupboard doors
          hourlyRate: 60
          illustration: http://clipart-library.com/img1/1605140.jpg
          image: https://images.unsplash.com/photo-1522791465802-47616431a4cf?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1451&q=80
          materials: true
          service: Cupboard Door Repairs
          time: 60
        - id: 10
          description: Plumbing issues and repairs
          hourlyRate: 90
          illustration: http://clipart-library.com/images_k/plumbing-silhouette/plumbing-silhouette-6.png
          image: https://images.unsplash.com/photo-1591804774220-c1db3673d05b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80
          materials: true
          service: Plumbing
          time: 60
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services
      query: |
        SELECT
         id, 
         '$.area',
         '$.description', 
         '$.hourlyrate',
         '$.illustration',
         '$.image', 
         '$.indoor', 
         '$.onceoffrate',
         '$.service',
         '$.time'
        FROM [default/cleaning-services]
        WHERE '$.service' LIKE '%'||@search||'%' OR @search IS NULL
      queryParameters:
        search: =@ctx.components.cleaning_serv_items.state.searchText
```
:::
::::::

:::::ExpandableHeading
### List with Filter functionality

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![List with filter](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bHiss0wgKVKlzkhquqLtf_lt6pfxjmnbkzj07kxqormlist-filteriphone13blueportrait.png "List with ")
:::

:::VerticalSplitItem
This example helps to filter the items in a list to create meaningful sections or split the data for ease of use.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-filter-label-sd.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-filter-label-dd.jigx).

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-filter-label-sd.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-filter-label-dd.jigx).
:::
::::

:::CodeblockTabs
filter-label (static)

```yaml
children:
  - type: component.list
    instanceId: filter-list
    options:
      filter: 
        - title: All
          value: ''
        - title: Indoor
          value: indoor
        - title: Outdoor
          value: outdoor
      # Data configured to use datasource (static)             
      data: =$filter(@ctx.datasources.cleaning-services-static, function($v){$contains($string($v.status), $string(@ctx.components.filter-list.state.filter != null ? @ctx.components.filter-list.state.filter:'')) })[]
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.area
          label:
            title: =(@ctx.current.item.status = "indoor" ? 'Indoor' :'Outdoor')
          leftElement: 
            element: avatar
            text: =$substring($substringBefore(@ctx.current.item.service, " "), 1, 1) & $substring($substringAfter(@ctx.current.item.service, " ") , 1, 1)
            uri: =@ctx.current.item.image
```

filter-label (dynamic)

```yaml
children:
  - type: component.list
    instanceId: cleaning_serv_items
    options:
      # Data configured to use datasource (dynamic)     
      data: =@ctx.datasources.cleaning-services-dynamic
      maximumItemsToRender: 50
      filter: 
        - title: All
          value: ''
        - title: Indoor
          value: "TRUE"
        - title: Outdoor
          value: "FALSE"
      
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.area
          label:
            title: =(@ctx.current.item.indoor = "TRUE" ? 'Indoor' :'Outdoor')
          leftElement: 
            element: avatar
            text: =$substring($substringBefore(@ctx.current.item.service, " "), 1, 1) & $substring($substringAfter(@ctx.current.item.service, " ") , 1, 1)
            uri: =@ctx.current.item.image
```

datasources (static)

```yaml
datasources:
  cleaning-services-static:
    type: datasource.static
    options:
      data:
        - area: Bathroom
          category: withRate
          description: Steam cleaning and disinfecting of the bathroom in its totality. Provision of fresh towels.
          hourlyrate: 30
          illustration: http://clipart-library.com/newimages/bathroom-clip-art-15.jpg
          image: https://images.unsplash.com/photo-1646592472335-fa6be8e9bc7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1471&q=80
          status: indoor
          onceoffrate:
          service: Bathroom Deep Clean
          time: 90
        - area: Garden
          category:
          description: Taking care of general gardening to provide an immaculate first impression
          hourlyrate:
          illustration: http://clipart-library.com/images/6Tr8BrjTK.jpg
          image: https://images.unsplash.com/photo-1416879595882-3373a0480b5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: outdoor
          onceoffrate: 100
          service: Gardening
          time: 120
        - area: General
          category:
          description: Cleaning and streak removal of external windows
          hourlyrate: 35
          illustration: http://clipart-library.com/img1/872145.png
          image: https://images.unsplash.com/photo-1650538250295-6ef68d7ae1f4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: outdoor
          onceoffrate: 
          service: Window Cleaning - External
          time: 60
        - area: Driveway
          category:
          description: Car wash including vacuum
          hourlyrate:
          illustration: http://clipart-library.com/new_gallery/9-95271_car-wash-comments-car-dry-wash-icon.png
          image: https://images.unsplash.com/photo-1520340356584-f9917d1eea6f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1631&q=80
          status: outdoor
          onceoffrate: 50
          service: Car Washing
          time: 60
        - area: Laundry
          category:
          description: Provision of laundry services by removal of laundry and return of laundry. Includes a surcharge for delivery.
          hourlyrate:
          illustration: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTLoH-sLiGa5Q2WgJLodqiqnxhGCHmNz2iTF9BOuLESQ-SGdI0&s
          image: https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1439&q=80
          status: indoor
          onceoffrate: 110
          service: Offsite laundry services
          time: 120
        - area: Laundry
          category:
          description: Provision of laundry services making use of client's machines. Note that where this has been booked, but machines are not available, this will automatically be adjusted to offsite laundry services.
          hourlyrate:
          illustration: http://clipart-library.com/newhp/white-laundry-basket-clip-art-laundry-basket-clipart-black-and-white-clipground_a28f63e33793a653.jpg
          image: https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1439&q=80
          status: indoor
          onceoffrate: 110
          service: Onsite laundry services
          time: 120
        - area: Lounge
          category:
          description: Maintain your upholstery (chair, couch and seat) in pristine condition. We use only the most delicate clearning methods.
          hourlyrate: 40
          illustration: http://clipart-library.com/images_k/carpet-cleaning-silhouette/carpet-cleaning-silhouette-12.png
          image: https://images.unsplash.com/photo-1612696733290-a2a26ce8131c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: indoor
          onceoffrate:
          service: Upholstery Cleaning
          time: 60
        - area: Pool
          category:
          description: Cleaning of pool, including chemical treatments, sweeping and proper flush.
          hourlyrate:
          illustration: http://clipart-library.com/data_images/476778.jpg
          image: https://images.unsplash.com/photo-1562844275-857f6e7c429e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1603&q=80
          status: outdoor
          onceoffrate: 40
          service: Pool Cleaning
          time: 45
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services
      query: |
        SELECT 
          id, 
          '$.area', 
          '$.description',
          '$.hourlyrate', 
          '$.illustration',
          '$.image', 
          '$.indoor', 
          '$.onceoffrate', 
          '$.service',
          '$.time'
        FROM [default/cleaning-services]
        WHERE '$.indoor' LIKE @filter or @filter IS NULL
      queryParameters:
          filter: =@ctx.components.cleaning_serv_items.state.filter
```
:::
:::::

:::::ExpandableHeading
### Filtered list with default tab set

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, there are four tabs to filter on. By default we want the jig to open on the third tab to show the in progress work by default. This is achieved by setting the `initialValue` property to the `filter` property.

**Examples**:
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-filter-initialvalue.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Tcoz4aCsZXsAf45JxF6ym-20240913-142629.PNG" size="80" position="center" caption="Filtered list with default tab" alt="Filtered list with default tab" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Tcoz4aCsZXsAf45JxF6ym-20240913-142629.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"}
:::
::::

:::CodeblockTabs
default-w-filter-initialvalue

```yaml
title: Filter List with default tab 
description: A dynamic list displaying filter options opening with a default tab showing tasks in progress
type: jig.default
icon: notes-paper-approve

header:
  type: component.jig-header
  options:
    children:
      options:
        source:
          uri: https://images.unsplash.com/photo-1590402494628-9b9acf0b90ae?q=80&w=2970&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
      type: component.image
    height: medium

datasources:
  team-tasks:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/tasks
      query: |
        SELECT 
          id, 
          '$.taskAssignee',
          '$.taskName',
          '$.taskCost',
          '$.taskId', 
          '$.taskStatus',
          '$.team', 
          '$.Profile'       
        FROM [default/tasks]
        WHERE '$.taskStatus' LIKE @filter or @filter IS NULL
      queryParameters:
          filter: =@ctx.components.task-progress.state.filter
    
children:
  - type: component.list
    instanceId: task-progress
    options:
      filter:
        initialValue: "In Progress"
        data: 
        - title: All
          value: ""
        - title: Not Started
          value: Not Started  
        - title: In Progress
          value: In Progress
        - title: Complete
          value: Complete            
      data: =@ctx.datasources.team-tasks         
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.taskName
          subtitle: =@ctx.current.item.taskId
          label:
            color:
              - when: =@ctx.current.item.taskStatus = "In Progress"
                color: color7
              - when: =@ctx.current.item.taskStatus = "Not Started"
                color: color4
              - when: =@ctx.current.item.taskStatus = "Complete"
                color: color2
            title: =@ctx.current.item.taskStatus
          leftElement:
            element: avatar
            text: =@ctx.current.item.taskAssignee
            uri: =@ctx.current.item.Profile  
      maximumItemsToRender: 50
```
:::
:::::

::::::ExpandableHeading
### List with Search and Filter functionality

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![List with search & filter](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9Z_36FsaTrAMuCRas1_OB_vmadtk6wrobldr9mo8fvilist-searchiphone13blueportrait.png "List with search & filter")
:::

::::VerticalSplitItem
Combine the search and filter capabilities to enhance the list functionalty.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-search-filter-sd.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-search-filter-dd.jigx).

:::hint{type="warning"}
By design, search functionality is automatically disabled when using it on a composite jig.
:::

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-search-filter-sd.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-search-filter-dd.jigx").
::::
:::::

:::CodeblockTabs
search-filter (static)

```yaml
children:
  - type: component.list
    instanceId: search-filter-list
    options:
      filter:
        data: 
        - title: All
          value: ''
        - title: Indoor
          value: indoor
        - title: Outdoor
          value: outdoor
      isSearchable: true
      # Data configured to use datasource (static)       
      data: =$filter($filter(@ctx.datasources.cleaning-services-static, function($v){$contains($string($v.service),$string(@ctx.components.search-filter-list.state.searchText != null ? @ctx.components.search-filter-list.state.searchText:'')) }), function($v){$contains($string($v.status), $string(@ctx.components.search-filter-list.state.filter != null ? @ctx.components.search-filter-list.state.filter:'')) })[]                                                                                                                                                                                                
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.area
          label:
            title: =(@ctx.current.item.status = "indoor" ? 'Indoor' :'Outdoor')
          leftElement: 
            element: avatar
            text: =$substring($substringBefore(@ctx.current.item.service, " "), 1, 1) & $substring($substringAfter(@ctx.current.item.service, " ") , 1, 1)
            uri: =@ctx.current.item.image
```

search-filter (dynamic)

```yaml
children:
  - type: component.list
    instanceId: cleaning_serv_items
    options:
      # Data configured to use datasource (dynamic)     
      data: =@ctx.datasources.cleaning-services-dynamic
      isSearchable: true
      maximumItemsToRender: 50
      filter:
        data: 
        - title: All
          value: ''
        - title: Indoor
          value: "TRUE"
        - title: Outdoor
          value: "FALSE"
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.area
          label:
            title: =(@ctx.current.item.indoor = "TRUE" ? 'Indoor' :'Outdoor')
          leftElement: 
            element: avatar
            text: =$substring($substringBefore(@ctx.current.item.service, " "), 1, 1) & $substring($substringAfter(@ctx.current.item.service, " ") , 1, 1)
            uri: =@ctx.current.item.image
```

datasources (static)

```yaml
datasources:
  cleaning-services-static:
    type: datasource.static
    options:
      data:
        - area: Bathroom
          category: withRate
          description: Steam cleaning and disinfecting of the bathroom in its totality. Provision of fresh towels.
          hourlyrate: 30
          illustration: http://clipart-library.com/newimages/bathroom-clip-art-15.jpg
          image: https://images.unsplash.com/photo-1646592472335-fa6be8e9bc7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1471&q=80
          status: indoor
          onceoffrate:
          service: Bathroom Deep Clean
          time: 90
        - area: Garden
          category:
          description: Taking care of general gardening to provide an immaculate first impression
          hourlyrate:
          illustration: http://clipart-library.com/images/6Tr8BrjTK.jpg
          image: https://images.unsplash.com/photo-1416879595882-3373a0480b5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: outdoor
          onceoffrate: 100
          service: Gardening
          time: 120
        - area: General
          category:
          description: Cleaning and streak removal of external windows
          hourlyrate: 35
          illustration: http://clipart-library.com/img1/872145.png
          image: https://images.unsplash.com/photo-1650538250295-6ef68d7ae1f4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: outdoor
          onceoffrate: 
          service: Window Cleaning - External
          time: 60
        - area: Driveway
          category:
          description: Car wash including vacuum
          hourlyrate:
          illustration: http://clipart-library.com/new_gallery/9-95271_car-wash-comments-car-dry-wash-icon.png
          image: https://images.unsplash.com/photo-1520340356584-f9917d1eea6f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1631&q=80
          status: outdoor
          onceoffrate: 50
          service: Car Washing
          time: 60
        - area: Laundry
          category:
          description: Provision of laundry services by removal of laundry and return of laundry. Includes a surcharge for delivery.
          hourlyrate:
          illustration: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTLoH-sLiGa5Q2WgJLodqiqnxhGCHmNz2iTF9BOuLESQ-SGdI0&s
          image: https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1439&q=80
          status: indoor
          onceoffrate: 110
          service: Offsite laundry services
          time: 120
        - area: Laundry
          category:
          description: Provision of laundry services making use of client's machines. Note that where this has been booked, but machines are not available, this will automatically be adjusted to offsite laundry services.
          hourlyrate:
          illustration: http://clipart-library.com/newhp/white-laundry-basket-clip-art-laundry-basket-clipart-black-and-white-clipground_a28f63e33793a653.jpg
          image: https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1439&q=80
          status: indoor
          onceoffrate: 110
          service: Onsite laundry services
          time: 120
        - area: Lounge
          category:
          description: Maintain your upholstery (chair, couch and seat) in pristine condition. We use only the most delicate clearning methods.
          hourlyrate: 40
          illustration: http://clipart-library.com/images_k/carpet-cleaning-silhouette/carpet-cleaning-silhouette-12.png
          image: https://images.unsplash.com/photo-1612696733290-a2a26ce8131c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          status: indoor
          onceoffrate:
          service: Upholstery Cleaning
          time: 60
        - area: Pool
          category:
          description: Cleaning of pool, including chemical treatments, sweeping and proper flush.
          hourlyrate:
          illustration: http://clipart-library.com/data_images/476778.jpg
          image: https://images.unsplash.com/photo-1562844275-857f6e7c429e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1603&q=80
          status: outdoor
          onceoffrate: 40
          service: Pool Cleaning
          time: 45
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dynamic:
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services
      query: |
        SELECT
         id, 
         '$.area',
         '$.description', 
         '$.hourlyrate',
         '$.illustration',
         '$.image', 
         '$.indoor',
         '$.onceoffrate',
         '$.service',
         '$.time'
        FROM [default/cleaning-services] 
        WHERE ('$.indoor' LIKE @filter OR @filter IS NULL) AND ('$.service' LIKE '%'||@search||'%' OR @search IS NULL)
      queryParameters:
        filter: =@ctx.components.cleaning_serv_items.state.filter
        search: =@ctx.components.cleaning_serv_items.state.searchText
```
:::
::::::

::::::ExpandableHeading
### Horizontal list

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Horizontal](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/PUolQC5rzXgpeRKu8dIlf_w42pf50snuglxtnxqaupyzoyiwlc9fs6cevvalpuslist-horizontal-w-janeiphone13blueportrait.png "Horizontal")
:::

::::VerticalSplitItem
This is an example of a horizontal list with UI elements such as an image and values configured. Horizontal lists are especially helpful when used on a composite jig.
**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-horizontal-list-sd.jigx).
See the full example using dynamic data in [GitHub]().

**Datasources**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx).

:::hint{type="warning"}
Horizontal lists cannot be used with the [section](./entity/section.md) component as an empty white jig will be displayed.
:::
::::
:::::

:::CodeblockTabs
horizontal-list (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      isHorizontal: true
      isHorizontalScrollIndicatorHidden: false
      # Data configured to use datasource (static) 
      data: =@ctx.datasources.repair-services-static
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.time & ' mins'
          divider: solid
          horizontalItemSize: large
          leftElement: 
            element: image
            text: ''
            uri: =@ctx.current.item.image
```

horizontal-list (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      isHorizontal: true
      isHorizontalScrollIndicatorHidden: false
      # Data configured to use datasource (dynamic)       
      data: =@ctx.datasources.cleaning-services-dynamic
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.service
          subtitle: =@ctx.current.item.time & ' mins'
          divider: solid
          horizontalItemSize: large
          leftElement: 
            element: image
            text: ''
            uri: =@ctx.current.item.image
```

datasources (static)

```yaml
datasources:
  repair-services-static:
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
        - id: 4
          description: Installation or repairs of dry-wall surfaces
          hourlyRate: 80
          illustration: http://clipart-library.com/img1/505759.jpg
          image: https://images.unsplash.com/photo-1628901551715-7234d14fb7a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: true
          service: Drywall Installation/Repair
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
        - id: 7
          description: Repairs to fences. Tools and items not included
          hourlyRate: 90
          illustration: http://clipart-library.com/img/18345.gif
          image: https://images.unsplash.com/photo-1583805978118-ba9a81ac1399?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: false
          service: Fence Installation/Repair
          time: 60
        - id: 8
          description: Removal of graffiti and painting. Paint and brushes not included in cost
          hourlyRate: 110
          illustration: http://clipart-library.com/images/6cy5aL5gi.jpg
          image: https://images.unsplash.com/photo-1581850518616-bcb8077a2336?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: false
          service: Removal of Graffiti
          time: 120
        - id: 9
          description: Repairs to cupboard doors
          hourlyRate: 60
          illustration: http://clipart-library.com/img1/1605140.jpg
          image: https://images.unsplash.com/photo-1522791465802-47616431a4cf?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1451&q=80
          materials: true
          service: Cupboard Door Repairs
          time: 60
        - id: 10
          description: Plumbing issues and repairs
          hourlyRate: 90
          illustration: http://clipart-library.com/images_k/plumbing-silhouette/plumbing-silhouette-6.png
          image: https://images.unsplash.com/photo-1591804774220-c1db3673d05b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80
          materials: true
          service: Plumbing
          time: 60
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services
      query: |
        SELECT 
          id, 
          '$.id' as sqlid, 
          '$.area', 
          '$.description', 
          '$.hourlyrate', 
          '$.illustration', 
          '$.image', 
          '$.indoor', 
          '$.onceoffrate', 
          '$.service', 
          '$.pressed', 
          '$.time',
          '$.quantity'
        FROM [default/cleaning-services] 
        WHERE '$.hourlyrate' IS NOT NULL ORDER BY id DESC
```
:::
::::::

## See also

- [State](https://docs.jigx.com/state)

