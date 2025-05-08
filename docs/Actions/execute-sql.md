---
title: execute-sql
slug: 2uGD-execute
createdAt: Fri Apr 25 2025 06:52:04 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 30 2025 15:51:55 GMT+0000 (Coordinated Universal Time)
---

This action allows the mobile app to execute a SQL statement on local execution of SQLite,  used in editing LOCAL tables or Dynamic Data tables. It’s useful for running custom queries or updates based on user interaction or app events.

## Configuration options

| **Core structure** |                                                                                                                                                                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `entities`         | The entities/tables affected by the statements. Before executing the statements, a check ensures that the tables exist.&#xA;After execution any datasources that use these entities will be notified that the database was changed.                   |
| `statements`       | List of statements to execute in sequence. Multiple statements can be configured to execute in sequence.&#xA;`statement` - the SQL statement to execute against the solution database.&#xA;`parameters` - The parameters used in the above statement. |
| `title`            | Provide the action button with a title, for example, *Delete record*.                                                                                                                                                                                 |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon]() to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                                                        |
| `isHidden`        | `true` hides the action button, `false` shows the action button. Default setting is `false`.                                                                                                                                                                                                                                                                                                                                       |
| `style`           | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Examples and code snippets

### Execute SQL statements to update & delete

This example shows a list with an `onPress` event that executes a SQL statement to update the *Tags* table in the database. A `swipeable` event is also configured to delete the list item record from the SQL database.

:::CodeblockTabs
create-tag.jigx

```yaml
title: Create Tag
type: jig.default
icon: checklist

actions:
  - children:
      - type: action.action-list
        options:
          title: Create Tag
          isSequential: true
          actions:
            - type: action.execute-sql
              options:
                statements:
                - statement: |
                      INSERT INTO tags (id, data)
                      VALUES (@id, @data)
                  parameters:
                      data: |
                        ={
                          "name": @.components.name.state.value,
                          "description": @.components.description.state.value,
                          "count": 0
                        }
                      id: =@.components.id.state.value   
                entities:
                  - tags
            - type: action.go-back
                  
children:
  - type: component.form
    instanceId: tag-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: id
          options:
            label: Id
            style:
              isDisabled: true
            value: "=$base64encode(@.components.name.state.value ?
              @.components.name.state.value : '')"
        - type: component.text-field
          instanceId: name
          options:
            label: Name
        - type: component.text-field
          instanceId: description
          options:
            label: Description
```

list-tag.jigx

```yaml
title: Tags (execute-sql)
type: jig.list

actions:
  - children:
      - type: action.go-to
        options:
          title: Create Tag
          linkTo: create-tag
        
datasources:
  tags:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: tags
      query: |
        SELECT id,
         '$.name', 
         '$.description',
         '$.count'
        FROM [tags]
    
data: =@.datasources.tags
item:
  type: component.list-item
  options:
    title: =@.current.item.name
    subtitle: "='count: ' & @.current.item.count"
    description: =@.current.item.description
    onPress:
      type: action.execute-sql
      options:
        entities:
          - tags
        statements:
          - statement: |
              UPDATE tags SET [data] = @data WHERE id = @id
            parameters:
              data: |
                ={
                  "name": @.current.item.name,
                  "description": @.current.item.description,
                  "count": @.current.item.count + 1
                }
              id: =@.current.item.id
              
    swipeable:
      left:
        - icon: close
          label: Delete
          onPress:
            type: action.confirm
            options:
              isConfirmedAutomatically: false
              modal:
                cancel: Do not delete
                confirm: DELETE
                description: =@.parents.list-data.item.name
                title: Do you really want to remove this Tag?
              onConfirmed:
                type: action.execute-sql
                options:
                  statements:
                    - statement: |
                        DELETE FROM tags WHERE id = @id
                      parameters:
                        id: =@.current.item.id  
                  entities:
                      - tags
```
:::

### Execute SQL statements to create & drop  indexes

description

:::CodeblockTabs
list-tasks-dd.jigx

```yaml
title: Tasks (DD)
type: jig.list
icon: checklist

onRefresh:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/tasks
    force: true
  
actions:
  - children:
      - type: action.go-to
        options:
          title: Create Task
          linkTo: create-task-dd
        
      - type: action.execute-sql
        options:
          title: Create Indexes
          statements:
            - statement: |
                CREATE UNIQUE INDEX IF NOT EXISTS udx_task_categories__name
                ON [default/task-categories] (JSON_EXTRACT(data, '$.name'))
            - statement: |
                CREATE INDEX IF NOT EXISTS idx_task__assignedTo
                ON [default/tasks] (JSON_EXTRACT(data, '$.assignedTo'))
          entities:
            - default/task-categories
            - default/tasks
            
      - type: action.execute-sql
        options:
          title: Delete Indexes
          statements:
            - statement: |
                DROP INDEX IF EXISTS udx_task_categories__name
            - statement: |
                DROP INDEX IF EXISTS idx_tasks__assignedTo
          entities:
            - default/task-categories
            - default/tasks

datasources:
  tasks:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/tasks
        - default/task-categories
      query: |
        SELECT
          T.id,
          json_extract(T.data, '$.name') as name,
          json_extract(T.data, '$.description') as description,
          json_extract(T.data, '$.complete') as complete,
          C.id as categoryId,
          json_extract(C.data, '$.name') as category,
          json_extract(T.data, '$.completed') as completed,
          json_extract(T.data, '$.assignedTo') as assignedTo
        FROM [default/tasks] AS T
        LEFT JOIN [default/task-categories] AS C
        ON json_extract(T.data,'$.categoryId') = C.id
        WHERE json_extract(T.data, '$.assignedTo') = @assignedTo
        ORDER BY [name]
      queryParameters:
        assignedTo: =@.user.email
    
data: =@.datasources.tasks
item:
  type: component.list-item
  options:
    title: =@.current.item.title
    subtitle: =@.current.item.description
    onPress:
      type: action.execute-entity
      options:
        provider: DATA_PROVIDER_DYNAMIC
        entity: default/tasks
        data:
          completed: "=(@.current.item.completed = 1 ? 0 : 1)"
          id: =@.current.item.id
        method: save  
    swipeable:
      left:
        - icon: close
          label: Delete
          onPress:
            type: action.confirm
            options:
              isConfirmedAutomatically: false
              modal:
                cancel: Do not delete
                confirm: DELETE
                description: =@.parents.list-data.item.name
                title: Do you really want to remove this Task?
              onConfirmed:
                type: action.execute-entity
                options:
                  provider: DATA_PROVIDER_DYNAMIC
                  entity: default/tasks
                  data:
                    id: =@.current.item.id
                  method: delete 
        - icon: pencil-2
          label: Edit
          onPress:
            type: action.go-to
            options:
              inputs:
                taskId: =@.current.item.id
              linkTo: edit-task-dd
```

create-task-dd.jigx

```yaml
itle: Create Task
type: jig.default
icon: checklist

actions:
  - children:
      - type: action.submit-form
        options:
          title: Create (submit-form)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: create
          formId: task-form
          goBack: previous
          data:
            assignedTo: =@.user.email
            createdAt: =$now()
            createdBy: =@.user.email
            owner: =@.user.email

      - type: action.execute-entity
        options:
          title: Create (execute-entity)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: create
          data:
            assignedTo: =@.user.email
            createdAt: =$now()
            createdBy: =@.user.email
            description: =@.components.description.state.value
            owner: =@.user.email
            title: =@.components.title.state.value
          goBack: previous
           
datasources:
  static:
    type: datasource.static
    options:
      data:
        - field1: value
          field2: value
          id: 1
    
children:
  - type: component.form
    instanceId: task-form
    options:
      children:
        - type: component.text-field
          instanceId: title
          options:
            label: Title
        - type: component.text-field
          instanceId: description
          options:
            label: Description
```

edit-task-dd.jigx

```yaml
title: Edit Task
type: jig.default
icon: checklist

actions:
  - children:
      - type: action.submit-form
        options:
          title: Create (submit-form)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: create
          formId: task-form
          data:
            owner: =@.user.email
          goBack: previous
      - type: action.execute-entity
        options:
          title: Create (execute-entity)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: create
          data:
            description: =@.components.description.state.value
            owner: =@.user.email
            title: =@.components.title.state.value
          goBack: previous
            
children:
  - instanceId: task-form
    options:
      type: component.form
      children:
        - type: component.text-field
          instanceId: title
          options:
            label: Title
        - type: component.text-field
          instanceId: description
          options:
            label: Description 
        - type: component.text-field
          instanceId: owner
          options:
            initialValue: =@ctx.user.email
            label: Owner
            style:
              isDisabled: true
```

task-dd.jigx

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - default/tasks
    - default/task-categories
  query: |
    SELECT
      T.id,
      json_extract(T.data, '$.name') as name,
      json_extract(T.data, '$.description') as description,
      json_extract(T.data, '$.status') as status,
      json_extract(T.data, '$.assignedTo') as assignedTo,
      json_extract(T.data, '$.createdAt') as createdAt,
      C.id as categoryId,
      json_extract(C.data, '$.name') as category
    FROM [default/tasks] AS T
    LEFT JOIN [default/task-categories] AS C
    ON json_extract(T.data,'$.categoryId') = C.id
    WHERE json_extract(T.data, '$.assignedTo') = @assignedTo
    ORDER BY [name]
  queryParameters:
    assignedTo: =@ctx.user.email
```
:::

:::CodeblockTabs
create-task-category.jigx

```yaml
title: Create Task Category
type: jig.default

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.components.create-category-form.state.data

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/task-categories
          method: create
          data:
            description: =@ctx.components.description.state.value
            id: =$replace($lowercase(@ctx.components.name.state.value), ' ', '-')
            name: =@ctx.components.name.state.value
          goBack: previous
      - type: action.go-back
        options:
          title: Cancel
        
children:
  - type: component.form
    instanceId: create-category-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: name
          options:
            isRequired: true
            label: Name
        - type: component.text-field
          instanceId: description
          options:
            isMultiline: true
            isRequired: false
            label: Description
            textArea: large
```

edit-task-category.jigx

```yaml
title: Edit Task Category
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Save
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/task-categories
          method: save
          data:
            description: =@ctx.components.description.state.value
            id: =@ctx.jig.inputs.categoryId
            name: =@ctx.components.name.state.value
          goBack: previous

      - type: action.confirm
        options:
          title: Delete Task Category
          isConfirmedAutomatically: false
          modal:
            title: =@ctx.datasources.category.name
            cancel: Cancel
            confirm: DELETE
            description: Do you really want to remove this Task Category?
          onConfirmed:
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/task-categories
              method: delete
              data:
                id: =@ctx.jig.inputs.categoryId
              
datasources:
  category:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/task-categories
      query: SELECT id, '$.name', '$.description' FROM [default/task-categories] WHERE
        [id] = @categoryId
      queryParameters:
        categoryId: =@ctx.jig.inputs.categoryId
    
children:
  - type: component.form
    instanceId: edit-category-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: categoryId
          options:
            label: Id
            style:
              isDisabled: true
            value: =@ctx.jig.inputs.categoryId 
        - type: component.text-field
          instanceId: name
          options:
            label: Name
            value: =@ctx.datasources.category.name     
        - type: component.text-field
          instanceId: description
          options:
            isMultiline: true
            isRequired: false
            label: Description
            textArea: large
            value: =@ctx.datasources.category.description
```

list-task-categories.jigx

```yaml
title: Task Categories
type: jig.list

onRefresh:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/task-categories
    force: true
    
actions:
  - children:
      - type: action.go-to
        options:
          title: Create New Category
          linkTo: create-task-category
        
data: =@ctx.datasources.task-categories-dd
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.description
    description: =$count(@ctx.datasources.tasks-dd[data.categoryId = @ctx.current.item.id])
    onPress:
      type: action.go-to
      options:
        inputs:
          categoryId: =@ctx.current.item.id
        linkTo: edit-task-category
      
    swipeable:
      left:
        - color: negative
          icon: bin-1
          label: Delete
          onPress:
            type: action.confirm
            options:
              isConfirmedAutomatically: false
              modal:
                cancel: Cancel
                confirm: DELETE
                description: Do you really want to remove this Task Category?
                title: =@ctx.current.item.name
              onConfirmed:
                type: action.execute-entity
                options:
                  provider: DATA_PROVIDER_DYNAMIC
                  entity: default/task-categories
                  method: delete
                  data:
                    id: =@ctx.current.item.id
                  
```

task-categories-dd.jigx

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - default/tasks
    - default/task-categories
  query: >
    SELECT
      C.id,
      json_extract(C.data, '$.name') as name,
      json_extract(C.data, '$.description') as description,
      json_extract(C.data, '$.image') as image,
      SUM(IFNULL(json_extract(T.data, '$.status') = 'ACTIVE', 0)) as activeTasks
    FROM [default/task-categories] AS C

    LEFT JOIN [default/tasks] AS T

    ON json_extract(T.data,'$.categoryId') = C.id AND json_extract(T.data, '$.assignedTo') = @assignedTo

    GROUP BY
      json_extract(C.data, '$.name'),
      json_extract(C.data, '$.description')
    ORDER BY [name]
  queryParameters:
    assignedTo: =@ctx.user.email

```
:::

