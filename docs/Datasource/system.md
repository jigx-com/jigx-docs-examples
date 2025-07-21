---
title: system
slug: _E0A-system
description: Learn how to utilize the system datasource in Jig UI components for efficient data management. This document outlines two methods of implementation: configuring it locally for storing data within a Jig, or setting it up globally for seamless access across
createdAt: Thu Jun 09 2022 18:33:57 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Feb 25 2025 10:32:26 GMT+0000 (Coordinated Universal Time)
---

The system datasource is usually used to get the list of country flag icons that can be used in a jig's components.

## Configuration options

When setting up a system datasource within a jig you can use it:

1. As a locally configured datasource within a jig for locally stored data to be available.
2. As a global datasource that allows easy access and reusability to the data across various jigs and components.

### System as jig local datasource

:::CodeblockTabs
system-local-datasource-jig.jigx

```yaml
# Add YAML in a jig file.
datasources:
  system:
    type: datasource.system
    options:
      source: flags
```

:::

### System as global datasource

:::CodeblockTabs
system

```yaml
# Add file under the datasource folder.
type: datasource.system
options:
  source: flags
```

:::

## Considerations

- For the flag to show you need to use a component or action that has an `icon` property, for example, `leftElement` or `rightElement`.

## See also

- [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/system.jigx)
