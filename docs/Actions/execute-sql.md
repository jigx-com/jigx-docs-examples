# execute-sql

This action allows the app to execute a SQL statement during local SQLite execution, which is used to edit either local tables or Dynamic Data tables. It's useful for running custom queries or updates in response to user interactions or app events. To improve performance, consider creating indexes on frequently queried columns—this enables SQLite to locate rows more efficiently using optimized lookup structures.

### Configuration options

<table><thead><tr><th width="152.64453125">Core structure</th><th></th></tr></thead><tbody><tr><td><code>entities</code></td><td>The entities/tables affected by the statements. Before executing the statements, a check ensures that the tables exist. After execution any datasources that use these entities will be notified that the database was changed.</td></tr><tr><td><code>statements</code></td><td>List of statements to execute in sequence. Multiple statements can be configured to execute in sequence. <code>statement</code> - the SQL statement to execute against the solution database. <code>parameters</code> - The parameters used in the above statement.</td></tr><tr><td><code>title</code></td><td>Provide the action button with a title, for example, <em>Delete record</em>.</td></tr></tbody></table>

<table><thead><tr><th width="155.98828125">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Select an to display when the action is configured as the secondary button or in a <a href="../Components/jig-header.md">header action</a>.</td></tr><tr><td><code>isHidden</code></td><td><code>true</code> hides the action button, <code>false</code> shows the action button. Default setting is <code>false</code>.</td></tr><tr><td><code>style</code></td><td><ul><li><code>isDanger</code> - Styles the action button in red or your brand's designated danger color.</li><li><code>isDisabled</code> - Displays the action button as greyed out.</li><li><code>isPrimary</code> - Styles the action button in blue or your brand's designated primary color.</li><li><code>isSecondary</code> - Sets the action as a secondary button, accessible via the ellipsis. The <code>icon</code> property can be used when the action button is displayed as a secondary button.</li></ul></td></tr></tbody></table>

### Considerations

* Validation currently only applies to SELECT statements and does not apply to INSERT, UPDATE, or DELETE operations, due to limitations in the SQLite parser.
* Creating indexes should occur before actual queries are run against the tables. Creating the index in the `onLoad` event in the index.jigx file ensures the app loads with the exact data.

### Examples and code snippets

#### Execute SQL statements to update & delete

This example shows a list with an `onPress` event that executes a SQL statement to update the _Tags_ table in the local database. A `swipeable` event is configured to delete the list item record from the local database.&#x20;

{% tabs %}
{% tab title="create-tag.jigx" %}
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
            # Create the tags record in the local SQLite table,
            # by writing a SQL statement to insert the record,
            # and parameters defining the record's data.
            - type: action.execute-sql
              options:
                statements:
                  - statement: |
                      INSERT INTO tags (id, data)
                      VALUES (@id, @data)
                    parameters:
                      data: |
                        ={
                          "name": @ctx.components.name.state.value,
                          "description": @ctx.components.description.state.value,
                          "count": 0
                        }
                      id: =@ctx.components.id.state.value
                entities:
                  - tags
            - type: action.go-back
# Configure a form to capture the tag details.
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
            value: "=$base64encode(@ctx.components.name.state.value ?
              @ctx.components.name.state.value : '')"
        - type: component.text-field
          instanceId: name
          options:
            label: Name
        - type: component.text-field
          instanceId: description
          options:
            label: Description
```
{% endtab %}

{% tab title="list-tag.jigx" %}
```yaml
title: Tags (execute-sql)
type: jig.list
# Add the action button in the list to create a new tag.
actions:
  - children:
      - type: action.go-to
        options:
          title: Create Tag
          linkTo: create-tag
# In the list display the tag's details, use an onPress with the execute-sql
# action to update the dataset by increasing the tag count
# when the item is pressed.
data: =@ctx.datasources.tags
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: "='count: ' & @ctx.current.item.count"
    description: =@ctx.current.item.description
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
                  "name": @ctx.current.item.name,
                  "description": @ctx.current.item.description,
                  "count": @ctx.current.item.count + 1
                }
              id: =@ctx.current.item.id
    # When swiping left on the list item, delete the tag's record
    # from the local database using the execute-sql action.
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
                title: Do you really want to remove this Tag?
              onConfirmed:
                type: action.execute-sql
                options:
                  statements:
                    - statement: |
                        DELETE FROM tags WHERE id = @id
                      parameters:
                        id: =@ctx.current.item.id
                  entities:
                    - tags
```
{% endtab %}

{% tab title="tags (datasource)" %}
```yaml
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
```
{% endtab %}
{% endtabs %}

#### Execute SQL statements to create indexes

This example demonstrates how to use the `execute-sql` action to run the CREATE statements. It also shows how to incorporate indexes to optimize query performance. Using SQL statements in this way allows you to define and manage table structures, remove data, and improve efficiency through indexing—all directly from your Jigx solution. Creating indexes should occur before actual queries are run against the tables. In this example we create the index on the `assignedTo` column in the `onLoad` event in the index.jigx file, ensuring that only the tasks for the logged on user are displayed.

{% tabs %}
{% tab title="index.jigx" %}
```yaml
name: jigx-demo-2025
title: jigx-demo-2025
category: analytics

# When the app loads, return only the tasks assigned to the logged-in user.
# Execute a SQLite statement to create an index on the assignedTo column
# in the task table.
onLoad:
  type: action.execute-sql
  options:
    # Specify the table where the index is required.
    entities:
      - default/tasks
    statements:
      # Create the index that returns the tasks for the assignedTo user.
      - statement: |
          CREATE INDEX IF NOT EXISTS idx_task__assignedTo
          ON [default/tasks] (JSON_EXTRACT(data, '$.assignedTo'))
tabs:
  home:
    label: Home label
    jigId: create-task-dd
    icon: home-apps-logo
```
{% endtab %}

{% tab title="create-task-dd.jigx" %}
```yaml
title: Create Task
type: jig.default
icon: checklist
# Pulling down on the jig will clear the form of any data.
onRefresh:
  type: action.reset-state
  options:
    state: =@ctx.components.task-form.state.data
# Configure the action to create the task record in the Dynamic Data table.
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: create
          goBack: previous
          data:
            assignedTo: =@ctx.user.email
            createdAt: =$now()
            createdBy: =@ctx.user.email
            description: =@ctx.components.description.state.value
            name: =@ctx.components.name.state.value
# Use the form component to capture the task name and description.
children:
  - type: component.form
    instanceId: task-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: name
          options:
            label: Name
        - type: component.text-field
          instanceId: description
          options:
            label: Description
```
{% endtab %}

{% tab title="list-tasks-dd.jigx" %}
```yaml
title: Tasks (DD)
type: jig.list
icon: checklist
# Add the action button in the list to create a new task.
actions:
  - children:
      - type: action.go-to
        options:
          title: Create Task
          linkTo: create-task-dd

data: =@ctx.datasources.task-dd
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.description
    # Complete the task by adding an onPress action.
    onPress:
      type: action.execute-entity
      options:
        provider: DATA_PROVIDER_DYNAMIC
        entity: default/tasks
        method: save
        data:
          id: =@ctx.current.item.id
          completed: "=(@ctx.current.item.completed = 1 ? 0 : 1)"
    # Edit or delete the task by swiping left, use the execute-entity action.
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
                title: Do you really want to remove this Task?
              onConfirmed:
                type: action.execute-entity
                options:
                  provider: DATA_PROVIDER_DYNAMIC
                  entity: default/tasks
                  method: delete
                  data:
                    id: =@ctx.current.item.id
        - icon: pencil-2
          label: Edit
          onPress:
            type: action.go-to
            options:
              inputs:
                task: =@ctx.current.item
              linkTo: edit-task-dd
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="edit-task-dd.jigx" %}
```yaml
title: Edit Task
type: jig.default
icon: checklist
# Use inputs to pass the task record as an object from the list.
# Allowing the form to be pre-filled with all the task details for editing.
inputs:
  task:
    type: object
    required: true
# Use update to save the changes made in the edit form.
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Update
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/tasks
          method: update
          goBack: previous
          data:
            id: =@ctx.jig.inputs.task.id
            description: =@ctx.components.description.state.value
            assignedTo: =@ctx.components.assignedTo.state.value
            name: =@ctx.components.name.state.value
# Use the defined jig inputs to populate the form fields,
# with the current records details.
children:
  - type: component.form
    instanceId: task-form
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: name
          options:
            initialValue: =@ctx.jig.inputs.task.name
            label: Name
        - type: component.text-field
          instanceId: description
          options:
            initialValue: =@ctx.jig.inputs.task.description
            label: Description
        - type: component.text-field
          instanceId: assignedTo
          options:
            initialValue: =@ctx.jig.inputs.task.assignedTo
            label: assignedTo
            style:
              isDisabled: true
```
{% endtab %}

{% tab title="task-dd.jigx" %}
```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - default/tasks
  # Configure the datasource query, ensuring the assignTo parameter uses
  # the logged in user. This is used by the execute-sql action to create the
  # index when the app loads. Only the logged on user's tasks are displayed.
  query: |
    SELECT
      id,
      json_extract(data, '$.name') as name,
      json_extract(data, '$.description') as description,
      json_extract(data, '$.complete') as complete,
      json_extract(data, '$.completed') as completed,
      json_extract(data, '$.assignedTo') as assignedTo
    FROM [default/tasks]
    WHERE json_extract(data, '$.assignedTo') = @assignedTo
    ORDER BY name
  queryParameters:
    assignedTo: =@ctx.user.email
```
{% endtab %}
{% endtabs %}
