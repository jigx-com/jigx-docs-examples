# start-sync-scope

Action starts or restarts a specific sync scope. The scope completes once all defined sync-entity actions/datasources have finished.

## Examples and code snippets

* In this example, three entities (database tables) are synced using `action.sync-entities`, namely:
  1. earthquake (REST)
  2. hike (Dynamica Data)
  3. penguins ( Dynamic Data)
* The `action.start-sync-scope` is used to write the status of the database tables to the local **\_syncScope** table. In turn the **\_syncStatus** table is updated with the sync operation.
* A datasource is configured against the **\_syncScope** and **\_syncStatus** table, and the details are returned in a list (for visibility in this example).
* The `action.start-sync-scope`  is used to start the sync scope. The results of the sync operation is visible in the list.

{% tabs %}
{% tab title="start-sync-scope" %}
```yaml
title: Sync-scope examples
type: jig.default

children:
  - type: component.section
    options:
      title:
        text: Scope
        fontSize: medium
        color: color3
        isSubtle: false
        isBold: true
        numberOfLines: 1

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


  - type: component.section
    options:
      title:
        text: Status
        fontSize: medium
        color: color10
        isSubtle: false
        isBold: true
        numberOfLines: 1
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
