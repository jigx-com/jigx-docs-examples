---
title: divider
slug: BFgX-divider
createdAt: Wed Jan 29 2025 07:48:11 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 03 2025 08:08:23 GMT+0000 (Coordinated Universal Time)
---

# divider

A divider is a simple yet effective UI component that creates a visual separation between components. It helps improve readability, structure content, and enhance user experience by distinguishing different sections. Common use cases include grouping related content or enhancing visual hierarchy.

#### Examples and code snippets

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-wbWNQ7aP448sIxR7cCoQW-20250203-075934.png" size="66" position="center" caption="Dividers" alt="Dividers"} :::

:::VerticalSplitItem This example demonstrates using dividers between components and creating a double-line divider between the horizontal list and the form. ::: ::::

:::CodeblockTabs divider.jigx

```yaml
children:
  - type: component.section
    options:
      title: Available cleaning options
      children:
        # Add a simple line divider between components.      
        - type: component.divider
        - type: component.list
          instanceId: service-list
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
  # Add multiple dividers between components.
  # A double line divider is made by stacking two component.divider components.                 
  - type: component.divider
  - type: component.divider
  - type: component.form
    instanceId: service-appt
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: fullName
          options:
            label: Full Name
        - type: component.field-row
          options:
            children:
              - type: component.number-field
                instanceId: contact
                options:
                  label: Contact Number
              - type: component.date-picker
                instanceId: appoint-date
                options:
                  label: Service Date
  # Add a simple line divider between components.                   
  - type: component.divider
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: ' '
            value: Thank you for your support
```

datasource (static)

```yaml
datasources:
  repair-services-static:
    type: datasource.static
    options:
      data:
        - id: 1
          image: https://images.unsplash.com/photo-1500281781950-6cd80847ebcd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1469&q=80
          service: Door Installation/Repair
          time: 60
        - id: 2
          image: https://images.unsplash.com/photo-1538766017398-415434a31a5b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          service: Door Handle/Lock Repairs
          time: 60        
        - id: 3
          image: https://images.unsplash.com/photo-1523413184730-e85dbbd04aba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80
          service: Tile Installation/Repair
          time: 120
        - id: 4
          image: https://images.unsplash.com/photo-1628901551715-7234d14fb7a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          service: Drywall Installation/Repair
          time: 120
        - id: 5
          image: https://images.unsplash.com/photo-1585313647787-7a061b5a85a6?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1423&q=80
          service: Bathroom Repairs
          time: 60
        - id: 6
          image: https://images.unsplash.com/photo-1562259949-e8e7689d7828?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1431&q=80
          service: Painting Services
          time: 120
        - id: 7
          image: https://images.unsplash.com/photo-1583805978118-ba9a81ac1399?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          service: Fence Installation/Repair
          time: 60
        - id: 8
          image: https://images.unsplash.com/photo-1581850518616-bcb8077a2336?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
          materials: false
          time: 120
        - id: 9
          image: https://images.unsplash.com/photo-1522791465802-47616431a4cf?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1451&q=80
          service: Cupboard Door Repairs
          time: 60
        - id: 10
          image: https://images.unsplash.com/photo-1591804774220-c1db3673d05b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80
          service: Plumbing
          time: 60
```
