# interactive-image-item

The interactive-image-item is used in the `item` property of the [interactive-image](../interactive-image.md) component that servers as a container. The `interactive-image-item` can be set in various ways using the properties of the [interactive-image](../interactive-image.md) as well as the properties described below.

## Configuration options

Some properties are common to all components, see [Common component properties](interactive-image-item.md) for a list and their configuration options.

<table><thead><tr><th width="214.78515625">Core structure</th><th></th></tr></thead><tbody><tr><td><code>id</code></td><td>Provide an id for the item that is used for filtering and as a key</td></tr><tr><td><code>percentageCoordinates</code></td><td>Percentage <code>x</code> and <code>y</code> coordinates are required. Coordinates are represented as absolute percentage numbers between 0-100.</td></tr><tr><td><code>title</code></td><td>Give a name/title for the point, for example, Table 1.</td></tr></tbody></table>

<table><thead><tr><th width="217.328125">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>This allows you to set a specific color for the active/selected point (e.g., when the point is selected or active).</td></tr><tr><td><code>icon</code></td><td>This allows you to set a specific icon for different states (e.g., when the point is selected active or inactive).</td></tr><tr><td><code>index</code></td><td>Index for the initial animation.</td></tr><tr><td><code>groupId</code></td><td>This property allows you to add the item to the group. The groups are created inside the component. Effective only initial load.</td></tr><tr><td><code>style</code></td><td>The following style options are available: <code>isActive</code> - shows if the point is active or available for selection. <code>isDisabled</code> - shows if the point is disabled and is unavailable for selection.</td></tr></tbody></table>

<table><thead><tr><th width="219.9453125">Actions</th><th></th></tr></thead><tbody><tr><td><code>onPress</code></td><td>The action is triggered when pressing the image's marked coordinate point. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="217.06640625">State Configuration</th><th width="130.71875">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>selected</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

## Examples and code snippets

### Restaurant table booking example

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CMhbVlUlzyLfHdBw3tyE8\_rest-1iphone13blueportrait.png" size="80" position="center" caption="Table booking" alt="Table booking" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CMhbVlUlzyLfHdBw3tyE8\_rest-1iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/isZZRxFP0Mj\_WAUzvJz1S\_rest-2iphone13blueportrait.png" size="80" position="center" caption="Table booking" alt="Table booking" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/isZZRxFP0Mj\_WAUzvJz1S\_rest-2iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}&#x20;
{% endcolumn %}
{% endcolumns %}

The example shows tables in a restaurant that are available for booking, the `pointColor` property is set to blue to show availabilty. Once a table is reserved the `icon` and `color` property are set to show that the tables are reserved and cannot be booked.

**Examples:** \
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/interactive-image/static-data/interactive-image-rest-sd.jigx) \
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/interactive-image/dynamic-data/interactive-image-rest-dd.jigx)

**Datasource:** \
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/interactive-image/floorplan-restaurant-static.jigx) \
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/interactive-image/floorplan-restaurant-dynamic.jigx)

{% tabs %}
{% tab title="interactive-image-rest (static)" %}
```yaml
children:
  - type: component.interactive-image
    options:
      imageHeight: 1500
      source: 
        uri:  https://fpg.roomsketcher.com/image/level/164/3d/Elegant-Restaurant-Plan-3D.jpg

          
      data: =@ctx.datasources.floorplan-restaurant-static
      pointColor: color10
      groups:
        - title: Reserved Tables
          id: Reserved
          color: color14

      item:
        type: component.interactive-image-item
        options:
          id: =@ctx.current.item.id
          title: =@ctx.current.item.name
          icon: =@ctx.current.item.isReserved = true ? 'close' :null
          color: =@ctx.current.item.isReserved = true ? 'color3' :null
          style:
            isDisabled: =@ctx.current.item.isReserved = true ? true :false
          
          percentageCoordinates:
            x: =@ctx.current.item.xCoordinate
            y: =@ctx.current.item.yCoordinate
```
{% endtab %}

{% tab title="interactive-image-rest (dynamic)" %}
```yaml
children:
  - type: component.interactive-image
    options:
      imageHeight: 1500
      source: 
        uri:  https://fpg.roomsketcher.com/image/level/164/3d/Elegant-Restaurant-Plan-3D.jpg

          
      data: =@ctx.datasources.floorplan-restaurant-dynamic
      pointColor: color10
      groups:
        - title: Reserved Tables
          id: Reserved
          color: color14

      item:
        type: component.interactive-image-item
        options:
          id: =@ctx.current.item.id
          title: =@ctx.current.item.name
          icon: =@ctx.current.item.isreserved = 'TRUE' ? 'close' :null
          color: =@ctx.current.item.isreserved = 'TRUE' ? 'color3' :null
          style:
            isDisabled: =@ctx.current.item.isreserved = 'TRUE' ? true :false
          
          percentageCoordinates:
            x: =@ctx.current.item.x
            y: =@ctx.current.item.y
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  floorplan-restaurant-static:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Table 1
          pax: 4
          xCoordinate: 7
          yCoordinate: 12
          isReserved: true
        - id: 2
          name: Table 2
          pax: 2
          xCoordinate: 15
          yCoordinate: 12
          isReserved: true
        - id: 3
          name: Table 3
          pax: 4
          xCoordinate: 23
          yCoordinate: 12
          isReserved: false
        - id: 4
          name: Table 4
          pax: 4
          xCoordinate: 48
          yCoordinate: 12
          isReserved: true
        - id: 5
          name: Table 5
          pax: 2
          xCoordinate: 56
          yCoordinate: 12
          isReserved: false
        - id: 6
          name: Table 6
          pax: 4
          xCoordinate: 64
          yCoordinate: 12
          isReserved: false
        - id: 7
          name: Table 7
          pax: 8
          xCoordinate: 64
          yCoordinate: 35
          isReserved: true
        - id: 8
          name: Table 8
          pax: 8
          xCoordinate: 64
          yCoordinate: 60
          isReserved: false
        - id: 9
          name: Table 9
          pax: 4
          xCoordinate: 48
          yCoordinate: 40
          isReserved: false
        - id: 10
          name: Table 10
          pax: 4
          xCoordinate: 25
          yCoordinate: 60
          isReserved: false
        - id: 11
          name: Table 11
          pax: 8
          xCoordinate: 11
          yCoordinate: 35
          isReserved: true
        - id: 12
          name: Table 12
          pax: 8
          xCoordinate: 11
          yCoordinate: 60
          isReserved: true
        - id: 13
          name: Table 13
          pax: 4
          xCoordinate: 6
          yCoordinate: 87
          isReserved: false
        - id: 14
          name: Table 14
          pax: 2
          xCoordinate: 15
          yCoordinate: 87
          isReserved: false
        - id: 15
          name: Table 15
          pax: 4
          xCoordinate: 23
          yCoordinate: 87
          isReserved: true
        - id: 16
          name: Table 16
          pax: 4
          xCoordinate: 49
          yCoordinate: 87
          isReserved: true
        - id: 17
          name: Table 17
          pax: 2
          xCoordinate: 58
          yCoordinate: 87
          isReserved: false
        - id: 18
          name: Table 18
          pax: 4
          xCoordinate: 66
          yCoordinate: 87 
          isReserved: true
        - id: 19
          name: Table 19
          pax: 2
          xCoordinate: 74
          yCoordinate: 87
          isReserved: false
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  floorplan-restaurant-dynamic:
    type: 'datasource.sqlite'
    options:
      provider: DATA_PROVIDER_DYNAMIC
    
      entities:
        - entity: default/interactive-image
    
      query: |
        SELECT 
          id, 
          '$.name', 
          '$.pax', 
          json_extract(data, '$.xcoordinate') as x, 
          json_extract(data, '$.ycoordinate') as y, 
          '$.isreserved', 
          '$.category' 
        FROM [default/interactive-image] WHERE '$.category' = 'floorplan-restaurant'
```
{% endtab %}
{% endtabs %}

### Hot seat and meeting room booking example

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2s0Sja4waFBBBLOPViRiQ\_interactive-image-1iphone13blueportrait.png" size="80" position="center" caption="Office desk booking" alt="Office desk booking" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2s0Sja4waFBBBLOPViRiQ\_interactive-image-1iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQ3a9vG8LXZ\_HVAl1AUyX\_interactive-image-2iphone13blueportrait.png" size="80" position="center" caption="Office desk booking" alt="Office desk booking" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQ3a9vG8LXZ\_HVAl1AUyX\_interactive-image-2iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
{% endcolumn %}
{% endcolumns %}

The example shows how hot seats and meeting rooms at an office can be booked. The `groups` property is used to differentiate between the types of available bookings, namely, seats, meeting rooms and reserved seats. The `maximumPoints` property specifies how many of each type can be booked, for example, there are three hot desks for booking.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/interactive-image/static-data/interactive-image-office-sd.jigx)&#x20;

{% tabs %}
{% tab title="interactive-image (static)" %}
```yaml
children:
  - type: component.interactive-image
    options:
      imageHeight: 1500
      source: 
        uri:  https://i.pinimg.com/564x/b0/eb/52/b0eb52122452257e955f210e7fdb8f55.jpg
          
      data: =@ctx.datasources.interactive-image-office
      pointColor: color10
      groups:
        - title: Selected desks
          id: Selected desks
          color: color2
        - title: Hot desk - reserved
          id: Hot desk - reserved
          color: color14
          maximumPoints: 3
        - title: Meeting room - reserved
          id: Meeting room
          color: color14
          maximumPoints: 1

      item:
        type: component.interactive-image-item
        options:
          id: =@ctx.current.item.id
          title: =@ctx.current.item.name
          icon: =@ctx.current.item.isReserved = true ? 'close' :null
          color: =@ctx.current.item.isReserved = true ? 'color3' :null
          groupId: =@ctx.current.item.group
          style:
            isDisabled: =@ctx.current.item.isReserved = true ? true :false
          percentageCoordinates:
            x: =@ctx.current.item.xCoordinate
            y: =@ctx.current.item.yCoordinate
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  interactive-image-office:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Meeting Room
          xCoordinate: 65
          yCoordinate: 43
          isReserved: true
          group: Meeting room
        - id: 2
          name: Hot Desk 1
          xCoordinate: 22
          yCoordinate: 12
          isReserved: true
          group: Hot desk - reserved
        - id: 3
          name: Hot Desk 2
          xCoordinate: 22
          yCoordinate: 22.5
          isReserved: false
          group:
        - id: 4
          name: Hot Desk 3
          xCoordinate: 22
          yCoordinate: 33
          isReserved: true
          group: Hot desk - reserved
        - id: 5
          name: Hot Desk 4
          xCoordinate: 22
          yCoordinate: 44
          isReserved: false
          group:
        - id: 6
          name: Hot Desk 5
          xCoordinate: 22
          yCoordinate: 55.5
          isReserved: false
          group:
        - id: 7
          name: Hot Desk 6
          xCoordinate: 22
          yCoordinate: 66.5
          isReserved: true
          group: Hot desk - reserved
```
{% endtab %}
{% endtabs %}

## See also

* [State](https://docs.jigx.com/state)
