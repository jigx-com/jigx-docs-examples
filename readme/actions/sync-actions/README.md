# Sync actions

Sync actions focused on synchronization processes, such as starting sync operations, managing sync scopes, or deleting sync-related data. These actions ensure data consistency across different parts of the system.

## **Types of Syncs**

<table><thead><tr><th width="169.64239501953125">Action name</th><th width="243.597900390625">Action</th><th>Description</th></tr></thead><tbody><tr><td><a href="delete-sync-scope.md">Delete sync scope</a></td><td><code>action.delete-sync-scope</code></td><td>Deletes a specific sync scope from the database table using its sync-scope ID.</td></tr><tr><td><a href="delete-sync-status.md">Delete sync statu</a>s</td><td><code>action.delete-sync-status</code></td><td>Deletes a specific sync status from the database table using its sync-status ID.</td></tr><tr><td><a href="start-sync-scope.md">Start sync scope</a></td><td><code>action.start-sync-scope</code></td><td>Starts or restarts a specific sync scope. The scope completes once all defined sync-entity actions/datasources have finished.</td></tr><tr><td><a href="sync-entities.md">Sync entities</a></td><td><code>action-sync-entities</code></td><td>Syncs the local database with the live database on the server.</td></tr></tbody></table>

## Key Components

#### 1. The `_syncStatus` Table

This table tracks the status of individual sync operations with the following properties:

<table><thead><tr><th width="122.5372314453125">Column</th><th>Description</th></tr></thead><tbody><tr><td><strong>id</strong></td><td> Unique identifier for the sync operation.</td></tr><tr><td><strong>provider</strong></td><td>The data provider being used.</td></tr><tr><td><strong>entity</strong></td><td>The entity being synchronized.</td></tr><tr><td><strong>functionId</strong> </td><td>The function handling the sync.</td></tr><tr><td><strong>state</strong></td><td><p>Current sync state, which is either:</p><ul><li> <code>syncing</code></li><li><code>synced</code></li><li><code>failed</code></li></ul></td></tr><tr><td><strong>timestamp</strong> </td><td>When the last status change occurred.</td></tr><tr><td><strong>error</strong></td><td>Contains any errors that occurred during sync.</td></tr></tbody></table>

#### 2. The `_syncScope` Table

This table tracks declared sync scopes and monitors their overall progress. The table allows  a sync scope to be started and use a datasource to track the progress of the sync scope.

<table><thead><tr><th width="144.51654052734375">Column</th><th>description</th></tr></thead><tbody><tr><td><strong>id</strong></td><td>Comes from the <code>instanceId</code> of the <code>action.start-sync-scope</code></td></tr><tr><td><strong>state</strong></td><td><p>Overall scope state, which is either:</p><ul><li><code>syncing</code>: Not all instances completed (i.e. failed or succeeded), some may not have started yet.</li><li><code>failed</code>: All instances completed, at least one failed</li><li><code>synced</code>: All instances completed successfully</li><li><code>interrupted</code>: App was closed, crashed, or put in the background</li></ul></td></tr><tr><td><strong>notStarted</strong></td><td>Count of instances not yet started.</td></tr><tr><td><strong>syncing</strong></td><td>Count of instances currently syncing, and have not completed or been interrupted.</td></tr><tr><td><strong>failed</strong></td><td>Count of instances that completed with errors.</td></tr><tr><td><strong>synced</strong></td><td>Count of instances that completed successfully.</td></tr><tr><td><strong>lastStartedAt</strong></td><td>Timestamp when scope last started (epoch milliseconds).</td></tr><tr><td><strong>lastFailedAt</strong></td><td>Timestamp when scope last failed (epoch milliseconds).</td></tr><tr><td><strong>lastSyncedAt</strong></td><td>Timestamp when scope last succeeded (epoch milliseconds).</td></tr><tr><td><strong>details</strong></td><td>JSON structure with per-instance details and failure information.</td></tr></tbody></table>

## How to use sync scopes

#### Step 1: Define the `action-start-sync-scope`

Use `action.start-sync-scope` to initialize a sync scope with a unique `instanceId`:

```yaml
- type: action.start-sync-scope
  instanceId: "sync-scope-lookup-data"
  options:
    instanceIds:
      - sync-tasks-and-categories-via-dd
      - sync-local-books-via-rest
      - sync-acuerp-customers-via-rest
      - sync-acuerp-stock-items-via-rest
```

#### Step 2: Define individual sync actions

Each sync operation needs its own `action.sync-entities` with a matching `instanceId`:

```yaml
- type: action.sync-entities
  instanceId: sync-tasks-and-categories-via-dd
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/tasks
      - default/task-categories

- type: action.sync-entities
  instanceId: sync-local-books-via-rest
  options:
    provider: DATA_PROVIDER_REST
    entities:
      - entity: local/books
        function: list-books-local-rest
```

#### Step 3: Conditionally trigger sync

Prevent multiple simultaneous syncs using a condition:

```yaml
- type: action.action-list
  when: "=@ctx.datasources.sync-scopes[id = 'sync-scope-lookup-data'].state = 'syncing' ? false : true"
  options:
    title: Sync data
    actions:
      # Your sync scope and sync actions go here
```

## Monitoring Sync Progress

### Query `_syncStatus` for individual operations

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

### Query `_syncScope` for overall progress

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

## Benefits

1. **Coordinated syncing**: Manage multiple entity syncs as a single operation.
2. **Progress tracking**: Monitor counts of syncing, synced, failed, and pending operations.
3. **Error Handling**: Track failures with detailed error information.
4. **State Management**: Prevent duplicate syncs and handle interruptions.
5. **Historical Data**: Access timestamps for sync events and detailed operation history.

## Best practices

* Always assign unique `instanceId` values to each sync operation.
* Use conditional logic to prevent overlapping sync operations.
* Monitor the `_syncScope` state to provide user feedback.
* Handle the `interrupted` state for better user experience when apps are put in the background.
* Check the `details` column for granular failure information.
