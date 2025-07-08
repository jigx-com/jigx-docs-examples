---
title: section
slug: g1WJ-section
description: Learn how to use the section component in your user interface to group related items together. This document provides examples and code snippets for creating display sections for repair services and cleaning services. Explore different repair and installa
createdAt: Thu Jun 09 2022 19:48:21 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 24 2024 09:33:04 GMT+0000 (Coordinated Universal Time)
---

The section component groups related items together under a single title. A section can be set up on a [jig.default](<./../../Jig Types/jig_default.md>) under the [entity](./../entity.md) component or on a [form](./../form.md) component as its container. The component can contain <a href="https://docs.jigx.com/examples/field-row" target="_blank">field-row</a> and [entity-field](./entity-field.md) components or children components on a [form](./../form.md) component.

A `component.section` can be set up with the following combinations:

1. An entity containing sections with [rows](./field-row.md) and [entity-field](./entity-field.md) for display purposes.
2. An entity containing sections and [entity-field](./entity-field.md) for display purposes.
3. A form component containing sections with [rows](./field-row.md) and children for display/capturing purposes.
4. A form component containing sections and children components for display/capturing purposes.
5. Horizontal lists cannot be used with the [section]() components as an empty white jig will be displayed.

Some properties are common to all components, see [Common component properties](docId:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

## Examples and code snippets

:::::ExpandableHeading

### The Entity with sections, rows, and entity fields (Display only)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Jig with sections](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5SKtUcADiqdQ1iYCL3z1M_sec1iphone13blueportrait.png "Jig with sections")
:::

:::VerticalSplitItem
Using sections, rows, and entity fields to create relevant display sections for the information to be functional yet elegant and neatly organized.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/static-data/section-row-entity-field-sd)
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/section-row-entity-field-dd.jigx).

**Datasources:**
See the full datasource for static data in [GitHub](tps://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/section-row-entity-field-dd.jigx)
:::
::::

:::CodeblockTabs
Section-rows-entity-fields (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Repair Services
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Service
                        value: =@ctx.datasources.repair-services-static[id=1].service
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Description
                        value: =@ctx.datasources.repair-services-static[id=1].description
                        isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Hourly Rate
                        value: =@ctx.datasources.repair-services-static[id=1].hourlyRate
                    - type: component.entity-field
                      options:
                        label: Time
                        value: =@ctx.datasources.repair-services-static[id=1].time & ' minutes'
                    - type: component.entity-field
                      options:
                        label: Materials
                        value: =(@ctx.datasources.repair-services-static[id=1].materials = 'True' ? true :false)
                        contentType: checkbox
```

Section-rows-entity-fields (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Service
                        value: =@ctx.datasources.cleaning-services-dynamic[0].service
                    - type: component.entity-field
                      options:
                        label: Area
                        value: =@ctx.datasources.cleaning-services-dynamic[0].area
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Time
                        value: =@ctx.datasources.cleaning-services-dynamic[0].time & ' minutes'
                    - type: component.entity-field
                      options:
                        label: Indoor
                        value: =@ctx.datasources.cleaning-services-dynamic[0].indoor
                        contentType: checkbox
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Description
                        value: =@ctx.datasources.cleaning-services-dynamic[0].description
                        isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Hourly Rate
                        value: =@ctx.datasources.cleaning-services-dynamic[0].hourlyrate != null ? @ctx.datasources.cleaning-services-dynamic[0].hourlyrate:'N/A'
                    - type: component.entity-field
                      options:
                        label: Once Off Rate
                        value: =@ctx.datasources.cleaning-services-dynamic[0].onceoffrate != null ? @ctx.datasources.cleaning-services-dynamic[0].onceoffrate:'N/A'
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
```

:::
:::::

:::::ExpandableHeading

### Form with sections, rows, and children components (Display and input)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Jig with sections & rows](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9vfRyetsrPXmlodRx0toQ_form-with-sectionsiphone13blueportrait.png "Jig with sections & rows")
:::

:::VerticalSplitItem
Similar to the above example, this has the same functionality, except that this is for adding or editing data too, and not just for display purposes.

**Examples:**
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/form-section-row-children-dd.jigx).

**Datasource:**
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx).
:::
::::

:::CodeblockTabs
form-section-row (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.text-field
                      instanceId: cleaning_serv_tf
                      options:
                        label: Service
                        value: =@ctx.datasources.cleaning-services-dynamic[0].service
                    - type: component.text-field
                      instanceId: cleaning_serv_area_tf
                      options:
                        label: Area
                        value: =@ctx.datasources.cleaning-services-dynamic[0].area
              - type: component.field-row
                options:
                  children:
                    - type: component.number-field
                      instanceId: cleaning_serv_time_num
                      options:
                        label: Time in mins
                        value: =@ctx.datasources.cleaning-services-dynamic[0].time
                        keyboardType: number-pad
                    - type: component.checkbox
                      instanceId: cleaning_serv_indoor_checkbox
                      options:
                        label: Indoor
                        value: =@ctx.datasources.cleaning-services-dynamic[0]].indoor

              - type: component.field-row
                options:
                  children:
                    - type: component.text-field
                      instanceId: cleaning_serv_desc_tf
                      options:
                        textArea: dynamic
                        label: Description
                        value: =@ctx.datasources.cleaning-services-dynamic[0].description
                        isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.text-field
                      instanceId: cleaning_serv_hourly_tf
                      options:
                        label: Hourly Rate
                        value: =@ctx.datasources.cleaning-services-dynamic[0].hourlyrate != null ? @ctx.datasources.cleaning-services-dynamic[0].hourlyrate:'N/A'
                    - type: component.text-field
                      instanceId: cleaning_serv_once_tf
                      options:
                        label: Once Off Rate
                        value: =@ctx.datasources.cleaning-services-dynamic[0].onceoffrate != null ? @ctx.datasources.cleaning-services-dynamic[0].onceoffrate :'N/A'
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
        FROM [default/cleaning-services] WHERE '$.hourlyrate' IS NOT NULL   ORDER BY id DESC
```

:::
:::::

:::::ExpandableHeading

### Entity with sections and entity-fields (Display only)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
**Basic**

![Jig with display sections & fields](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nMs-BfhD6R1UM-4N3Q6BL_img9804iphone13blueportrait.png "Jig with display sections & fields")
:::

:::VerticalSplitItem
**Compact**

![Jig with display sections & fields](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hNKX2CKxIPamHFP1U0RPu_img9803iphone13blueportrait.png)
:::
::::

This is another example for display purposes only, but this time without the rows. Note the difference in the fields as they now display below each other instead of numerous entity-fields in a row.

**Examples:**
**Basic**- See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/static-data/section-entity-field-sd.jigx).
**Compact** - See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/static-data/section-entity-field-sd-compact.jigx).

**Datasources:**
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/section-entity-field-dd.jigx).

:::CodeblockTabs
section-entity-field (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Repair Services
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.repair-services-static[id=1].service
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.repair-services-static[id=1].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.repair-services-static[id=1].hourlyRate
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.repair-services-static[id=1].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Materials
                  value: =(@ctx.datasources.repair-services-static[id=1].materials = 'True' ? true :false)
                  contentType: checkbox
```

section-entity-field-compact (static)

```yaml
children:
  - type: component.entity
    options:
      isCompact: true
      children:
        - type: component.section
          options:
            title: Repair Services
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.repair-services-static[id=1].service
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.repair-services-static[id=1].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.repair-services-static[id=1].hourlyRate
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.repair-services-static[id=1].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Materials
                  value: =(@ctx.datasources.repair-services-static[id=1].materials = 'True' ? true :false)
                  contentType: checkbox
```

section-entity-field (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services[0].service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services[0].area
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services[0].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services[0].indoor
                  contentType: checkbox
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services[0].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services[0].hourlyrate != null ? @ctx.datasources.cleaning-services[0].hourlyrate :'N/A'
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services[0].onceoffrate != null ? @ctx.datasources.cleaning-services[0].onceoffrate :'N/A'
```

section-entity-field-compact (dynamic)

```yaml
children:
  - type: component.entity
    options:
      isCompact: true
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services[0].service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services[0].area
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services[0].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services[0].indoor
                  contentType: checkbox
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services[0].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services[0].hourlyrate != null ? @ctx.datasources.cleaning-services[0].hourlyrate :'N/A'
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services[0].onceoffrate != null ? @ctx.datasources.cleaning-services[0].onceoffrate :'N/A'
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
  cleaning-services:
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
        FROM [default/cleaning-services] ORDER BY '$.service' ASC
```

:::
:::::

:::::ExpandableHeading

### Form with sections and entity-fields (Display and input)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Form with sections](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U_yPbJflLyS_T1tiIygID_secc3iphone13blueportrait.png "Form with sections")
:::

:::VerticalSplitItem
This is the same as the above, again with the exception of being used in a form component and not just being for display purposes, but allowing input from the user.

**Examples:**
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/form-section-children-dd.jigx).

**Datasources:**
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/form-section-children-dd.jigx).
:::
::::

:::CodeblockTabs
form-section-children (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.text-field
                instanceId: cleaning_serv_tf
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services-dynamic[0].service
              - type: component.text-field
                instanceId: cleaning_serv_area_tf
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services-dynamic[0].area
              - type: component.number-field
                instanceId: cleaning_serv_time_num
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services-dynamic[0].time & ' minutes'
                  keyboardType: number-pad
              - type: component.checkbox
                instanceId: cleaning_serv_indoor_checkbox
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services-dynamic[0].indoor
              - type: component.text-field
                instanceId: cleaning_serv_desc_tf
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services-dynamic[0].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.text-field
                instanceId: cleaning_serv_hourly_tf
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services-dynamic[0].hourlyrate != null ? @ctx.datasources.cleaning-services-dynamic[0].hourlyrate:'N/A'
              - type: component.text-field
                instanceId: cleaning_serv_once_tf
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services-dynamic[0].onceoffrate != null ? =@ctx.datasources.cleaning-services-dynamic[0].onceoffrate :'N/A'
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
          '$.time', 
          '$.category' 
        FROM [default/cleaning-services]
```

:::
:::::
