---
title: Common component properties
slug: LLnT-lg-work-area
description: Learn how to use the "When" property in Jigx components to conditionally show or hide components and execute actions. This comprehensive document includes an example code snippet demonstrating how the "When" property is utilized to display a text field ex
createdAt: Fri Apr 14 2023 12:19:19 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 09:46:37 GMT+0000 (Coordinated Universal Time)
---

Some properties are common to all Jigx components. See the details below:

::::ExpandableHeading

### When

`when` - this property is used at two levels, in components to show/hide any component conditionally and in actions to execute/not execute an action.

Below are the settings to use with the `when` property:

- `when: true`
- `when: false`
- `when: =@ctx` set with an expression

**Example and code snippet**

The example below demonstrates how the `when` property is used at a component level to display a `component.text-field` (Note requirements) only when the `component.checkbox` (Special Diet) is selected.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Xic9Zc-dcHhgZJ_-_qata-20250225-095457.png" size="62" position="center" caption="When-Display a field  " alt="When-Display a field  "}

:::CodeblockTabs
When.jigx

```yaml
title: Lunch Order
description: Place your lunch order here
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: >
            https://images.unsplash.com/photo-1543352634-99a5d50ae78e
            ?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
            &auto=format&fit=crop&w=1171&q=80
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Order Date
            value: =$now()
  - type: component.form
    instanceId: MealSelection
    options:
      children:
        - type: component.dropdown
          instanceId: Meal
          options:
            label: Select your meal
            data: =@ctx.datasources.meals
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.meal
                value: =@ctx.current.item.meal
        - type: component.checkbox
          instanceId: SpecialDiet
          options:
            label: Special Diet
            helperText: Select if you have special diet requirments
            isRequired: false
        - type: component.text-field
          instanceId: SpecialDietDescp
          # Use the when property to set a condition in an expression.
          # When the checkbox is selected the text-field displays. 
          # If the condition evaluates to false the text-field is hidden.
          when: =@ctx.components.SpecialDiet.state.value = true ? true:false
          options:
            label: Note Requirements
            isMultiline: true
            isRequired: false       
actions:
  - children:
      - type: action.submit-form
        options:
          formId: MealSelection
          provider: DATA_PROVIDER_DYNAMIC
          title: Book Meal
          entity: default/meal-selection
          method: create
          onSuccess: 
            type: action.go-back
```

datasource

```yaml
datasources: 
  meals: 
    type: datasource.static 
    options: 
      data: 
          - id: 1 
            meal: Beef Lasagne 
          - id: 2
            meal: Chicken Wrap
          - id: 3
            meal: Tuna Pasta 
          - id: 4 
            meal: Toasted Ham Cheese and Tomato
          - id: 5 
            meal: Flapjacks with Fresh Berries
```

:::
::::

::::ExpandableHeading

### Colors

**Applying colors based on specific conditions**: Colors can be configured based on specific conditions. For example, a payment amount exceeding a certain threshold can be displayed in red. However, conditional color configurations are only available in areas that support conditions, such as list items. In contrast, direct color options are more widely supported, for example, `lists` allow both conditional and direct setups, whereas `interactive-images` only support direct options. Additionally, certain areas restrict the available color choices, while UI elements support the predefined set of fourteen colors.

- When configuring the `color` property, select the `color condition` option.
- Under the `when` property, add an expression that defines the condition under which the specified color should be applied.

:::CodeblockTabs
color-condition

```yaml
color:
   - when: =@ctx.current.item.registered = true 
     color: color2
   - when: =@ctx.current.item.registered = false
     color: color4          
```

color (no condition)

```yaml
options:
  color: color2
```

:::
::::
