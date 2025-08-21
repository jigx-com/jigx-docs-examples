# entity

The entity component is a container for the following components:

* [entity-field](entity/entity-field.md)
* [entity-field](entity/entity-field.md)
* [section](entity/section.md)

## Considerations

* The `component.entity` used with the above-mentioned components is configurable on a `jig.default`.
* [Section](entity/section.md) and [field-row](entity/field-row.md) are also available under the `component.form` as its container. Here the [entity-field](entity/entity-field.md) is replaced by the [form's](form.md) children field.
* When setting up a `component.entity`, either a [default jig](<../Jig Types/jig_default.md>) or `component.form` can be used in the following combinations:
  * An entity containing [section(s)](entity/section.md) with [rows](entity/field-row.md) and [entity-field](entity/entity-field.md)
  * An entity containing [section(s)](entity/section.md) and [entity-field](entity/entity-field.md)An entity containing [rows](entity/field-row.md) and [entity-field](entity/entity-field.md)
  * An entity containing [entity fields](entity/entity-field.md)

## Configuration options

Some properties are common to all components, see [Common component properties](entity.md) for a list and their configuration options.

<table><thead><tr><th width="138.28515625">Other options</th><th></th></tr></thead><tbody><tr><td><code>isCompact</code></td><td>When this property is set to <code>true</code> the entity-field will cover the entire row. This compact variant does not allow usage of field-row components. By default, a label is at the top and the value below. <code>isCompact</code> will place the label on the left and the value on the right. Columns are not supported.</td></tr></tbody></table>

## Examples and code snippets

{% columns %}
{% column %}
![Entity with sections, row & field](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xQ6vW15SRw79rWRz5aMxz_img9802iphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
![Entity with sections & field](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/P7cVpxb09Yx1ZnvKqqhc8_img9803iphone13blueportrait.png)
{% endcolumn %}
{% endcolumns %}

### Entity example

**Compact**

**Examples**: **Basic** - See the full example using static data in [GitHub](entity.md). **Compact** - See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/section/dynamic-data/section-entity-field-dd-compact.jigx).

{% tabs %}
{% tab title="Basic-entity-section-row-entity-field" %}
```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Biographical & Membership Details
            children:
              - type: component.field-row
                options:
                  children: 
                    - type: component.entity-field
                      options:
                        label: First Name
                        value: Samantha
                        contentType: default
                        rightIcon: person
                    - type: component.entity-field
                      options:
                        label: Surname
                        value: Jackson
                        contentType: default
                        rightIcon: person
                    - type: component.entity-field
                      options:
                        label: Member
                        value: true
                        contentType: checkbox
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Date of Birth
                        value: 1988-01-19
                        contentType: date
                        rightIcon: calendar
                    - type: component.entity-field
                      options:
                        label: Last Login Time
                        value: =$now()
                        contentType: time
                        rightIcon: time-clock-circle
        - type: component.section
          options:
            title: Contact & Other Details
            children:
            - type: component.entity-field
              options:
                label: Clipboard Info
                value: Copy me!
                contentType: copy
            - type: component.entity-field
              options:
                label: Contact Number
                value: +2776 123 4567
                contentType: phone
                rightIcon: phone
            - type: component.entity-field
              options:
                label: Email Address
                value: samjax@emailaddress.com
                contentType: email
                rightIcon: email
            - type: component.entity-field
              options:
                label: Web Address
                value: samjax@website.me
                contentType: link
                rightIcon: google
            - type: component.entity-field
              options:
                label: About
                value: Lorem ipsum dolor sit amet, putent viderer pericula per ex, cu ius sonet referrentur. Cu pri ubique mediocrem maluisset, eum ea assum vivendum constituto. Fierent accusata nec ut, ullum impetus omittam cu per. Perpetua consectetuer no ius. Nam error elitr no, ferri praesent te cum. An commodo aliquando dissentiet duo. Primis eripuit bonorum ius ei, usu cu posse mazim. Elitr alterum mentitum eos cu, sit te quodsi everti neglegentur. Est in diam causae, erat conceptam eum an. Sea ullum causae temporibus ex, libris delectus pro et.
                isMultiline: true
                contentType: default
```
{% endtab %}

{% tab title="Compact-entity-section-entity-field" %}
```yaml
children:
  - type: component.entity
    options:
      isCompact: true
      children:
        - type: component.section
          options:
            title: Cleaning Services
            children:
              - type: component.entity-field
                options:
                  label: Service
                  value: =@ctx.datasources.cleaning-services[0].service
              - type: component.entity-field
                options:
                  label: Area
                  value: =@ctx.datasources.cleaning-services[0].area
              - type: component.entity-field
                options:
                  label: Time
                  value: =@ctx.datasources.cleaning-services[0].time & ' minutes'
              - type: component.entity-field
                options:
                  label: Indoor
                  value: =@ctx.datasources.cleaning-services[0].indoor
                  contentType: checkbox
              - type: component.entity-field
                options:
                  label: Description
                  value: =@ctx.datasources.cleaning-services[0].description
                  isMultiline: true
        - type: component.section
          options:
            title: Rates
            children:
              - type: component.entity-field
                options:
                  label: Hourly Rate
                  value: =@ctx.datasources.cleaning-services[0].hourlyrate != null ? @ctx.datasources.cleaning-services[0].hourlyrate :'N/A'
              - type: component.entity-field
                options:
                  label: Once Off Rate
                  value: =@ctx.datasources.cleaning-services[0].onceoffrate != null ? @ctx.datasources.cleaning-services[0].onceoffrate :'N/A'
```
{% endtab %}

{% tab title="Datasource (dynamic)" %}
```yaml
datasources:
  cleaning-services:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - entity: default/cleaning-services
  
      query: |
        SELECT 
          id, 
          '$.area', 
          '$.description', 
          '$.hourlyrate', 
          '$.illustration', 
          '$.image', 
          '$.indoor', 
          '$.onceoffrate', 
          '$.service', 
          '$.time' 
        FROM [default/cleaning-services] ORDER BY '$.service' ASC
```
{% endtab %}
{% endtabs %}

### See also

* [entity-field](entity/entity-field.md)
* [field-row](entity/field-row.md)
* [section](https://docs.jigx.com/docs/jc-section%22)
