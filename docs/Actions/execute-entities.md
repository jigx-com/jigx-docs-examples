# execute-entities

`Execute-entities` is used to modify, create, and delete **multiple rows** in a specific table in a database.

{% hint style="warning" %}
Execute-entities can't be used if you're using [Static Data](https://docs.jigx.com/examples/static).&#x20;
{% endhint %}

### Configuration options

An `execute-entities` action can be used in multiple areas:

1. Under action button
2. In action list
3. In onPress/onChange events (if the component has these options)
4. In onRefresh/onFocus

### Reference data properties and values as a group

With the `execute-entities` action, you can reference data properties and values as a group instead of listing them individually to be saved or created. See the data-grouped example below:

{% tabs %}
{% tab title="data-grouped" %}
```yaml
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Create Record(s)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/hikers
          method: create
          data: =@ctx.datasources.items
          onSuccess: 
            type: action.go-back
```
{% endtab %}

{% tab title="data-individual-listed" %}
```yaml
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Create Record(s)
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/hikers
          method: create
          goBack: previous
          data:
            contact: =@ctx.datasources.items.contact
            name: =@ctx.datasources.items.name
            email: =@ctx.datasources.items.email
            photo: =@ctx.datasources.items.photo
            participant-group: =@ctx.datasources.items.participant-group
```
{% endtab %}
{% endtabs %}

### Offline remote data handling

Dealing with offline remote data is fundamental to ensuring data synchronization and consistency between the mobile app and the remote data source, allowing users to continue using the app and performing actions without interruption. [Offline remote data handling](https://docs.jigx.com/offline-remote-data-handling) explains how to configure solutions to deal with data when the device is offline using the `queueOperations` property available in execute-entities, and provides examples and code samples.

### Examples and code snippets

#### Execute-entities in action

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZPfcvY8IXq38rfPeeZNGQ\_action-exec-entitiesaction.PNG" size="80" position="center" caption="Execute entities" alt="Execute entities" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZPfcvY8IXq38rfPeeZNGQ\_action-exec-entitiesaction.PNG
{% endcolumn %}

{% column %}
**Example:** See the full example of execute-entities as an action in [GitHub](%22https:/github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-action.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% code title="execute-entities-action" %}
```yaml
actions:
  - children:
    - type: action.execute-entities
      options:
        title: Add user
        provider: DATA_PROVIDER_DYNAMIC
        method: create
        entity: default/form
        data:
          firstname: =@ctx.datasources.employee-detail-dynamic.firstname
          lastname: =@ctx.datasources.employee-detail-dynamic.lastname
```
{% endcode %}

#### Execute-entities in action list

**Example:** See the full example of execute-entities in an action list in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-actionlist.jigx).

{% code title="execute-entities-action-list" %}
```yaml
actions:
  - children:
      - type: action.action-list
        options:
          isSequential: true
          title: Add user
          actions:
            - type: action.execute-entities
              options:
                provider: DATA_PROVIDER_DYNAMIC
                method: create
                entity: default/form
                data:
                  firstname: =@ctx.datasources.employee-detail-dynamic.firstname
                  lastname: =@ctx.datasources.employee-detail-dynamic.lastname
            - type: action.info-modal
              options:
                modal:
                  title: User successfully added  
                  buttonText: See user list
                  element: 
                    type: icon
                    icon: add-circle-bold-alternate
                    color: element
                onConfirmed: 
                  type: action.go-to
                  options:
                    linkTo: execute-entities-onPress
```
{% endcode %}

#### Execute-entities in onPress/onChange event

Here is the example of execute-entities in onPress/onChange event in [list-item](../Components/list/list-item.md).

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0N1UFXpdG5QljwfLgPb4P\_action-eentitiespress.PNG" size="80" position="center" caption="Execute-entities" alt="Execute-entities" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0N1UFXpdG5QljwfLgPb4P\_action-eentitiespress.PNG"}

**Example:**

See the full example of execute-entities in action onPress in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-onPress.jigx) See the full example of execute-entities in action onChange in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-onChange.jigx)

{% tabs %}
{% tab title="onPress" %}
```yaml
onPress: 
  type: action.execute-entities
  options:
      provider: DATA_PROVIDER_LOCAL
      method: update
      entity: default/employees
      data: 
        id: =@ctx.current.item.id
        modify: =($number(@ctx.current.item.modify) + 1) 
```
{% endtab %}

{% tab title="onChange" %}
```yaml
onChange: 
  type: action.execute-entities
  options:
    provider: DATA_PROVIDER_LOCAL
    method: update
    entity: default/employees
    data: 
      id: =@ctx.current.item.id
      modify: =$number(@ctx.current.item.modify) + 1
```
{% endtab %}
{% endtabs %}

#### Execute-entities in onRefresh/onFocus

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/S3C6VXWWnlIVhWPXbXlXh\_actioneenitiesonfocus.PNG" size="80" position="center" caption="Execute-entites" alt="Execute-entites" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/S3C6VXWWnlIVhWPXbXlXh\_actioneenitiesonfocus.PNG"}

**Example:**

See the full example of execute-entities in onRefresh in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-onRefresh.jigx). See the full example of execute-entities in onFocus in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/execute-entities/execute-entities-onFocus.jigx).

{% tabs %}
{% tab title="execute-entities-onRefresh" %}
```yaml
onRefresh: 
  type: action.execute-entities
  options:
    provider: DATA_PROVIDER_LOCAL
    method: update
    entity: default/employees
    data: =@ctx.datasources.employee-detail-dynamic.{'id':id, 'modify':$number(modify)+1}
```
{% endtab %}

{% tab title="execute-entities-onFocus" %}
```yaml
onFocus: 
  type: action.execute-entities
  options:
    provider: DATA_PROVIDER_LOCAL
    method: update
    entity: default/employees
    data: =@ctx.datasources.employee-detail-dynamic.{'id':id, 'modify':$number(modify)+1}
```
{% endtab %}
{% endtabs %}

#### Deleting multiple data records using execute-entities

To delete multiple data records in a Dynamic data table use the execute entities action with an expression as shown below.

{% hint style="info" %}
This code example is **not** in the jigx.samples solution in GitHub.&#x20;
{% endhint %}

**Example:**

{% code title="Execute-entities-multiple" %}
```yaml
actions:
  - children:
      - type: action.execute-entities
        options: 
          title: Delete employees
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/employees
          method: delete
          data: =@ctx.datasources.employee.{"id" :id}[]
```
{% endcode %}

#### Updating multiple data records using execute-entities

To update multiple data records in a Dynamic data table use the execute entities action with an expression as shown below.

{% hint style="info" %}
This code example is **not** in the jigx.samples solution in GitHub.&#x20;
{% endhint %}

**Example:**

```yaml
actions:
  - children:
      - type: action.execute-entities
        options:
          title: Update Records
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/penguin_species
          method: update
          data: =@ctx.datasources.penguin-species ~> | $ | {"endangered":"Yes"} |    
```

#### Updating multiple data records in a single REST call

See [Update multiple records in a single REST call](<../Data Providers/REST/Create an app using REST APIs/Update multiple records in a single REST call.md>) for an example of using execute-entities with REST.
