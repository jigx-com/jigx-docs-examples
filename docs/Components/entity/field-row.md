---
title: field-row
slug: iGAk-field-row
createdAt: Thu Jun 09 2022 19:32:19 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 24 2024 09:33:13 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to use the field-row component to display multiple components on the
  same row in this comprehensive document. Discover how rows can contain
  entity-field components and children components, a
---

# field-row

The field-row component contains other components and displays them on the same row. This component does not indicate a new row; all components are automatically placed in a new row. Instead, this component ensures that items are placed next to instead of underneath each other.

### Considerations

* Rows can contain [entity-field](entity-field.md) components:
  * On a [default jig](<../../Jig Types/jig_default.md>) or children components
  * On a [form](../form.md) component
  * Nested under [section](section.md) components
* A maximum of three components can be displayed per row.

Some properties are common to all components, see [Common component properties](docId:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

### Examples and code snippets

:::::ExpandableHeading

#### Field-row components with entity-fields (Display only)

::::VerticalSplit{layout="left"} :::VerticalSplitItem ![Field-row](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VA6mlFjt5KI9NaTxqInAb_mv9-5gc8jut5xwtpdtsmock-fieldiphone13blueportrait.png) :::

:::VerticalSplitItem Example showing how rows have been incorporated to display more than one component per row in certain instances.

**Examples:** See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/field-row/static-data/row-entity-field-sd.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/field-row/dynamic-data/row-entity-field-dd.jigx).

**Datasources:** See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx). ::: ::::

:::CodeblockTabs row-entity-fields (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.repair-services-static[id=2].service
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.repair-services-static[id=2].description
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.repair-services-static[id=2].hourlyRate
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.repair-services-static[id=2].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Materials
                  value: =(@ctx.datasources.repair-services-static[id=2].materials = 'True' ? true :false) 
                  contentType: checkbox   
```

row-entity-fields (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services-dd.service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services-dd.area
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services-dd.time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services-dd.indoor
                  contentType: checkbox
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services-dd.description
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services-dd.hourlyrate
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services-dd.onceoffrate      
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
          hourlyRat
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dd:
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
        FROM [default/cleaning-services] WHERE '$.service' = "Mattress Cleaning"
```

::: :::::

:::::ExpandableHeading

#### Field-row components on form with children components (Display and input)

::::VerticalSplit{layout="left"} :::VerticalSplitItem ![field-row on form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/O9ZlnWKC7QQAQScg2Klh4_8uyi918oalwk7j3rzytb1mock-field2iphone13blueportrait.png) :::

:::VerticalSplitItem **Examples:** See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/field-row/dynamic-data/form-row-children-dd.jigx).

**Datasource:** See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx). ::: ::::

:::CodeblockTabs form-rows-children (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: cleaning_serv_tf
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services-dd.service
              - type: component.text-field
                instanceId: cleaning_area_tf
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services-dd.area
        - type: component.field-row
          options:
            children:
              - type: component.number-field
                instanceId: cleaning_serv_time_num
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services-dd.time & ' minutes'
                  keyboardType: number-pad
              - type: component.checkbox
                instanceId: cleaning_serv_indoor_checkbox
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services-dd.indoor
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: cleaning_serv_desc_tf
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services-dd.description
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: cleaning_serv_hourly_tf
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services-dd.hourlyrate
              - type: component.text-field
                instanceId: cleaning_serv_once_tf
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services-dd.onceoffrate
```

datasources (dynamic)

```yaml
datasources:
  cleaning-services-dd:
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
        FROM [default/cleaning-services] WHERE '$.service' = "Mattress Cleaning"
```

::: :::::
