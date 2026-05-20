# delete-sync-scope

Action deletes a specific sync scope from the \_syncScope database table using its sync-scope ID.

## Examples and code snippets

1. In this example, three entities (database tables) are synced using `action.sync-entities`, namely:
   1. earthquake (REST)
   2. hike (Dynamica Data)
   3. penguins ( Dynamic Data)
2. The `action.start-sync-scope` is used to write the scope of the database tables to the local **\_syncScope** table.&#x20;
3. A datasource is configured against the **\_syncScope** table, and the details are returned in a list (for visibility in this example).
4. The `action.delete-sync-scope`  is used to delete the scope that was written to the **\_syncScope table** using the `instanceId` given in the `action.start-sync-scope` .

{% tabs %}
{% tab title="delete-sync-scope" %}
```yaml
title: Sync-scope examples
type: jig.default

children:
  - type: component.list
    options:
      # Bind data from the sync-scopes datasource
      data: =@ctx.datasources.sync-scopes
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          # Display the sync scope state (syncing, synced, failed, interrupted)
          title:
            text: =@ctx.current.item.state
          # Display the details JSON structure as subtitle  
          subtitle:
            text: =@ctx.current.item.details
            fontSize: regular
            numberOfLines: 3
          # Show the sync scope ID on the right side of the list item  
          rightElement:
            element: text
            firstLine: =@ctx.current.item.id
# Define actions available for each sync scope            
actions:
  - numberOfVisibleActions: 2
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
      # Action to delete a specific sync scope from the _syncScope table 
      # using the instanceId of the start-sync action as a reference.   
      - type: action.delete-sync-scope
        options:
          # ID of the sync scope to delete (matches instanceId above) 
          id: sync-all
          title: Delete scope

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

{% tab title="datasources" %}
```yaml
datasources:
  sync-scopes:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _syncScope
      query: |
        SELECT 
          id, 
          state, 
          timestamp, 
          lastSyncedAt, 
          lastStartedAt, 
          lastFailedAt, 
          notStarted, 
          syncing, 
          synced, 
          failed, 
          details 
        FROM [_syncScope]

```
{% endtab %}
{% endtabs %}
