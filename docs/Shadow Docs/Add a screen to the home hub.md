---
title: Add a screen to the home hub
slug: VJFL-add-a
createdAt: Thu Jun 13 2024 09:57:57 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 10 2024 08:59:14 GMT+0000 (Coordinated Universal Time)
---

Add the following YAML content to reference a screen or jig on the home hub or app home page.&#x20;

```yaml
name: simple-list
title: simple-list
category: business    
   
widgets:
  - size: "1x1"
    jigId: notification-form
  - size: "1x1"
    jigId: notify-send-execute-entity
```

