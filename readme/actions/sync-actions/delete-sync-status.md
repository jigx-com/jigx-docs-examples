# delete-sync-status

Action deletes a specific sync scope from the \_syncStatus database table using its sync-scope ID.

## Examples and code snippets

1. In this example, three entities (database tables) are synced using `action.sync-entities`, namely:
   1. earthquake (REST)
   2. hike (Dynamica Data)
   3. penguins ( Dynamic Data)
2. The `action.start-sync-scope` is used to write the status of the database tables to the local **\_syncScope** table. In turn the **\_syncStatus** table is updated with the sync operation.
3. A datasource is configured against the **\_syncStatus** table, and the details are returned in a list (for visibility in this example).
4. The `action.delete-sync-status`  is used to delete the scope that was written to the **\_syncStatus** table using the `instanceId` given in the `action.start-sync-scope` .

{% tabs %}
{% tab title="delete-sync-status" %}
```yaml
title: Sync-scope examples
type: jig.default

children:
  - type: component.list
    options:
      # Bind data from the sync-status datasource
      data: =@ctx.datasources.sync-status
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
        # Display the sync scope state 
          title: =@ctx.current.item.state
          # Display the datasource table that the state applies to.
          subtitle: =@ctx.current.item.entity
          # Add a tag to show the status of the sync-scope.
          tags:
            - text: =@ctx.current.item.state
              color: primary
          # Show the id of each sync scope status. The id is used in the action to
          # identify the sync status that must be deleted.     
          rightElement:
            element: text
            firstLine: =@ctx.current.item.id
# Define actions available for each sync scope  
actions:
  - numberOfVisibleActions: 3
    children:
      # Action to start a new sync scope.
      - type: action.start-sync-scope
        # Specify a unique identifier for this sync scope action. 
        instanceId: sync-all
        options:
          # List the individual instanceIds of each sync (sync-entities)
          # that the sync scope applies to.
          instanceIds:
            - sync-quakes
            - sync-enviro
          title: Start sync
      # Action to delete a specific sync status from the _syncStatus table 
      # using the id of the sync-status in the table as a reference.   
      - type: action.delete-sync-status
        options:
          id: "7"
          title: Delete status
```
{% endtab %}

{% tab title="sync-entities" %}
```yaml
onFocus:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        instanceId: sync-quakes
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: earthquakes
              function: earthquake-data
      - type: action.sync-entities
        instanceId: sync-enviro
        options:
          provider: DATA_PROVIDER_DYNAMIC
          entities:
            - default/hike
            - default/penguins
```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  sync-status:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _syncStatus
      query: |
        SELECT
          id, 
          provider, 
          entity, 
          functionId, 
          timestamp, 
          state, 
          error
        FROM [_syncStatus]
        ORDER BY provider
```
{% endtab %}
{% endtabs %}
