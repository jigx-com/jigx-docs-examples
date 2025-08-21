# Localization (Translation)

Solutions can easily be translated into any language by using the `Text Locale` property and creating a translation file with the translated text in Jigx Builder. On the device, use the _Profile>Settings>Language_ option and select _Device (Respects device settings)_. To understand how to configure localization in Jigx see [Localization](https://docs.jigx.com/localization).

{% hint style="info" %}
Adding dynamic values in localized jigs use **ICU message** definitions. Try it in the [Online ICU Message Editor](https://format-message.github.io/icu-message-format-for-translators/editor.html) or see the [ICU format messaging](https://unicode-org.github.io/icu/userguide/format_parse/messages/) documentation.
{% endhint %}

## Configuration options

<table><thead><tr><th width="156.765625">Core structure</th><th></th></tr></thead><tbody><tr><td><code>text Locale</code></td><td><ul><li><code>id</code> - provide a unique identifier for the property to be translated.</li><li><code>values</code> - create context variables with values to use in the translation file. This is useful when creating dynamic content.</li><li><code>defaultMessage</code> - If no translation is found for the active device's language, it will either fallback to the specified <code>defaultMessage</code> or, if one is not specified, to English.</li></ul></td></tr></tbody></table>

## Examples and code snippets

## Form localized in five languages with static values

In this example, the new employee form is translated into German, French, and Czech. To see the form in each of the languages change your device language setting to one of the configured languages.

**Examples**: See the jig example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-localization/localized-form-static.jigx). See the translation file examples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/translations).

![Chez, German, English](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2I1zBOgZCHFr3k64gXtrb_trans-form-static.PNG)

{% tabs %}
{% tab title="localized-form-static.jigx" %}
```yaml
title:
  id: title
  defaultMessage: New employee form
description: To view this jig in other languages, change your devices language settings to either German, French, or Czech
type: jig.default
icon: form

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1423666639041-f56000c27a9a?q=80&w=2374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.form
  # Used in the submit-form action to get context to the property instanceId.
    instanceId: form-employee 
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: first_name # becomes the name of the column in table
          options:
            label:
              id: first_name
              defaultMessage: First Name

        - type: component.text-field
          instanceId: last_name # becomes the name of the column in table
          options:
            label:
              id: last_name
              defaultMessage: Last Name

        - type: component.number-field
          instanceId: contact_number # becomes the name of the column in table
          options:
            label:
              id: contact_number
              defaultMessage: Mobile number

        - type: component.date-picker
          instanceId: date_of_birth # becomes the name of the column in table
          options:
            label:
              id: date_of_birth
              defaultMessage: Date of birth

        - type: component.avatar-field
          instanceId: photo # becomes the name of the column in table
          options:
            label:
              id: photo
              defaultMessage: My profile

        - type: component.signature-field
          instanceId: signature # becomes the name of the column in table
          options:
            label:
              id: signature
              defaultMessage: Sign

        - type: component.email-field
          instanceId: email # becomes the name of the column in table
          options:
            label:
              id: email
              defaultMessage: Email address

actions:
  - children:
      - type: action.execute-entity
        options:
          title:
            id: create
            defaultMessage: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/employees
          method: create
          data:
            first_name: =@ctx.components.first_name.state.value
            last_name: =@ctx.components.last_name.state.value
            contact_number: =@ctx.components.contact_number.state.value
            date_of_birth: =@ctx.components.date_of_birth.state.value
            photo: =@ctx.components.photo.state.value
            signature: =@ctx.components.signature.state.value
            email: =@ctx.components.email.state.value
          onSuccess:
            type: action.go-back
```
{% endtab %}

{% tab title="de.jigx" %}
```yaml
title: Formular für neue Mitarbeiter
description: Erfassen Sie die Details des neuen Mitarbeiters
first_name: Vorname
last_name: der Nachname
contact_number: Handynummer
date_of_birth: Geburtsdatum
photo: mein Profil
signature: Zeichen
email: E-Mail-Adresse
create: Mitarbeiter anlegen
```
{% endtab %}

{% tab title="fr.jigx" %}
```yaml
title: Formulaire de nouvel employé
description: Capturez les détails du nouvel employé
first_name: Prénom
last_name: Nom de famille
contact_number: Numéro de portable
date_of_birth: Date de naissance
photo: Mon profil
signature: Signe
email: Adresse e-mail
create: Créer un employé
```
{% endtab %}

{% tab title="cs.jigx" %}
```yaml
title: Nový zaměstnanecký formulář
description: Zachyťte podrobnosti o novém zaměstnanci
first_name: Jméno
last_name: Příjmení
contact_number: Číslo mobilního telefonu
date_of_birth: Datum narození
photo: Můj profil
signature: Podepsat
email: Emailová adresa
create: Vytvořit zaměstnance
```
{% endtab %}
{% endtabs %}

## Jig translated into German with dynamic values

In this example, a jigwith today's activites is translated into German. The translation is configured dynamically agains the `Text Locale` values. To see the form in each of the languages change your device language setting to one of the configured languages.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hoK-35uG5y6FomN9LyI0s\_trans-dynamic.PNG" size="82" position="center" caption="One jig in two languages" alt="One jig in two languages" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hoK-35uG5y6FomN9LyI0s\_trans-dynamic.PNG" width="800" height="787" darkWidth="800" darkHeight="787"}

**Examples**: See the jig example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-localization/localized-activities-dynamic.jigx). See the translation file examples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/translations).

{% tabs %}
{% tab title="localized-activities-dynamic.jigx" %}
```yaml
title:
  id: greeting
  values:
    name: =@ctx.user.displayName
    time: =$fromMillis($millis(),'[P]')
  defaultMessage: ="Welcome " & @ctx.user.displayName
description:
  id: activities
  defaultMessage: Today's activities
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1508614999368-9260051292e5?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

datasources:
  activities:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Swimming
          location: Pool
          previewDetail: 7pm
          icon: swimming-diving
        - id: 2
          name: Tennis
          location: Court
          previewDetail: 6am
          icon: tennis-backhand
        - id: 3
          name: Exercising
          location: Gym
          previewDetail: 5pm
          icon: fitness-weights

children:
  - type: component.avatar
    options:
      title: profile
      size: large
      align: center
      uri: https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8YXZhdGFyJTIwd29tYW58ZW58MHx8MHx8fDA%3D

  - type: component.list
    options:
      data: =@ctx.datasources.activities
      item:
        type: component.list-item
        options:
          title:
            id: sport
            values:
              name: =@ctx.current.item.name
          subtitle:
            id: venues
            values:
              location: =@ctx.current.item.location
          rightElement:
            element: icon
            icon: =@ctx.current.item.icon
```
{% endtab %}

{% tab title="de.jigx" %}
```yaml
greeting: "{time, select, am {Guten Morgen} pm {Guten Nachmittag} other {Hallo}} {name}"
activities: Die heutigen Aktivitäten
sport: "{name, select, Swimming {Baden} Tennis {Tennis} other {Trainieren}}"
venues: "{location, select, Pool {Schwimmbad} Court {Tennisplatz} other {Fitnessstudio}}"
```
{% endtab %}

{% tab title="en.jigx" %}
```yaml
greeting: "{time, select, am {Good Morning} pm {Good afternoon} other {Hello}} {name}"
sport: "{name, select, Swimming {Swimming} Tennis {Tennis} other {Exercising}}"
venues: "{location, select, Pool {Pool} Court {Court} other {Gym}}"
```
{% endtab %}
{% endtabs %}
