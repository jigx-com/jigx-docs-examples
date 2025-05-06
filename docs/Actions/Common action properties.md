---
title: Common action properties
slug: xwLa-common-component-properties
createdAt: Mon Feb 24 2025 08:03:32 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Mar 10 2025 17:52:53 GMT+0000 (Coordinated Universal Time)
---

Certain properties are shared across all actions, ensuring consistency and flexibility in configuration. These common properties allow you to define behaviors, appearance, and functionality that apply universally, regardless of the specific actions used. This simplifies the setup process and helps maintain uniformity across different jigs.

## Dual action buttons&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Configure `actions` to display two action buttons on the jig's main screen. In this example, the first button has a secondary button `style` applied, by default, the button normally uses the primary color. Additionally, you can set up a third action, referred to as a secondary action button, that appears when the ellipsis (...) is tapped. This allows multiple action options to be accessible within a single jig.
:::

:::VerticalSplitItem
![Dual action buttons & secondary button](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-TZVU6r07hz0LEPo_3zZ2W-20250225-092012.png "Dual action buttons & secondary button")
:::
::::

| **Property**             | **Description**                                                                                                                                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `numberOfVisibleActions` | Configure this property to display multiple action buttons on the screen. The recommended number is two. A numerical value is expected, such as `2`. |

```yaml
actions:
# Number of visible buttons displayed on the jig.
  - numberOfVisibleActions: 2       
    children:
      # First action button.
      - type: action.go-back
        options:
          # Apply a style to the button. 
          style:
            isSecondary: true
          title: Back
      # Second action button.                
      - type: action.go-to
        options:
          title: Continue
          behaviour: new
          linkTo: contact  
      # Third action button configured (secondary action).
      # The button displays when the ellipsis is tapped.    
      - type: action.execute-entity
        options:
          title: Save  
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/contacts
          method: create
          data:
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            phone: =@ctx.components.phone.state.value
            jobTitle: =@ctx.components.jobTitle.state.value
            companyName: =@ctx.components.companyName.state.value    
```

