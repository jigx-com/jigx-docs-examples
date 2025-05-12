# countdown

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The countdown component functionality counts down from a date, date/time, and time.  When the time expires, you can configure an outcome, for example, open a different jig, or perform an action. The countdown starts as soon as the jig containing the `component.countdown` opens.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-laofo1T3WD_bJvdgslD-_cd-inputsl.PNG" size="80" position="center" caption="Countdown" alt="Countdown" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-laofo1T3WD_bJvdgslD-_cd-inputsl.PNG"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `expiresAt`        | Add a date, date/time or time when the countdown must expire/stop, either using:&#xA;- datasource, e.g. `=@ctx.datasources.events.date`&#xA;- expression, e.g. `=$fromMillis($toMillis($now()) + 50000)`&#xA;- string, e.g. `"2023-09-20 18:00"`, or `"2023-07-25T17:30:00+02:00"` |

| **Other options** |                                                                                                                                                                                                                                              |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `align`           | `center`, `left`, `right`, and `stretch`, with `center` as the default if the property is not specified in the YAML.                                                                                                                         |
| `labels`          | `isVisible` - `true` or `false` with `true` as the default. Setting `false` will hide the countdown component.&#xA;`position` - The countdown labels of Days : Hours : Minutes: Seconds are shown at the `bottom` or `top` of the countdown. |
| `size`            | Choose from `extra-large`, `large`, `medium`, `small`, with `large` being the default if the property is not specified in the YAML.                                                                                                          |

| **Actions** |                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------- |
| `onPress`   | Choose from the provided list of available actions, for example, use the `go-to` action to open a different jig. |
| `onFinish`  | Choose from the provided list of available actions. For example, `go-back` action.                               |

## Considerations

- This component's function is to countdown to a predefined date/time. It is not recommended to use the component as a timer.
- The `component.countdown` can only be used in a `jig.default`.
- The countdown's separator is by default shown as a colon `:`.
- The countdown starts when you navigate to the jig containing the `component.countdown`.
- Use any inputs for the countdown configuration, for example, different types of datasources, states and inputs.
- Use the `set-state` and `reset-state` actions to set and reset the countdown.

## Examples and code snippets

:::::ExpandableHeading
### Countdown with inputs (static, dynamic, expression, & datasource)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-laofo1T3WD_bJvdgslD-_cd-inputsl.PNG" size="80" position="center" caption="Countdown" alt="Countdown" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-laofo1T3WD_bJvdgslD-_cd-inputsl.PNG"}
:::

:::VerticalSplitItem
This example shows the `expiresAt` property value set using a static value, an expression, a static datasource, and a dynamic datasource.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-input.jigx").
:::
::::

:::CodeblockTabs
countdown-input.jigx

```yaml
children:
  - type: component.section
    options:
      title: COUNTDOWN WITH STATIC VALUE
      children:
      - type: component.countdown
        options:
          expiresAt: "2025-10-06 22:00"

  - type: component.section
    options:
      title: COUNTDOWN WITH COUNT FROM NOW
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 3600000)

  - type: component.section
    options:
      title: COUNTDOWN WITH DATASOURCE INPUT (STATIC)
      children:
      - type: component.countdown
        options:
          expiresAt: =@ctx.datasources.dates[1].date

  - type: component.section
    options:
      title: COUNTDOWN WITH DATASOURCE INPUT (DYNAMIC)
      children:
      - type: component.countdown
        options:
          expiresAt: =@ctx.datasources.event-dd[2].StartDate
```

event-dd.jigx

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC

  entities:
    - default/events

  query: SELECT id, '$.EventName', '$.StartDate', '$.Tickets', '$.Time', '$.Type', '$.Venue' FROM [default/events] 
    
```

static-data

```yaml
datasources:
  dates: 
    type: datasource.static
    options:
      data:
        - id: 1
          dateType: Clothes Sale
          date: "2025-08-17 07:00"
        - id: 2
          dateType: flights
          date: "2025-07-10 08:00"
        - id: 3
          dateType: Books
          date: "2025-07-18 14:00"
```
:::
:::::

:::::ExpandableHeading
### Countdown with alignment

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
You can choose to `align` the `component.countdown` to the `left`, `right`, `center` and `stretch` it across the screen.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-align.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5fs13z66fs4frrvBiL0V6_cd-alignl.PNG" size="80" position="center" caption="Aligning countdown" alt="Aligning countdown" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5fs13z66fs4frrvBiL0V6_cd-alignl.PNG"}
:::
::::

:::CodeblockTabs
countdown-align.jigx

```yaml
children:
  - type: component.section
    options:
      title: COUNTDOWN ALIGN - LEFT
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 3600000)
          align: left

  - type: component.section
    options:
      title: COUNTDOWN ALIGN - CENTER
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 3600000)
          align: center

  - type: component.section
    options:
      title: COUNTDOWN ALIGN - RIGHT
      children:
      - type: component.countdown
        options: 
          expiresAt: =$fromMillis($toMillis($now()) + 3600000)
          align: right

  - type: component.section
    options:
      title: COUNTDOWN ALIGN - STRETCH
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 3600000)
          align: stretch
```
:::
:::::

:::::ExpandableHeading
### Countdown with different sizes

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/InsX4GIv9T12zvbtQjiDp_cd-sizel.PNG" size="80" position="center" caption="Size variations" alt="Size variations" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/InsX4GIv9T12zvbtQjiDp_cd-sizel.PNG"}
:::

:::VerticalSplitItem
Use the `size` property in the `component.countdown` to change the size from `extra-large` to `small`.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-sizes.jigx).
:::
::::

:::CodeblockTabs
count-down-sizes.jigx

```yaml
children:
  - type: component.section
    options:
      title: COUNTDOWN SIZE - EXTRA-LARGE
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: extra-large
            
  - type: component.section
    options:
      title: COUNTDOWN SIZE - LARGE (Default)
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: large
          
  - type: component.section
    options:
      title: COUNTDOWN SIZE - MEDIUM
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: medium

  - type: component.section
    options:
      title: COUNTDOWN SIZE - SMALL
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: small
```
:::
:::::

:::::ExpandableHeading
### Countdown onPress

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
![Action when pressed](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/w0GIWssJYaMr0muw1PZwb_cd-onpressl.PNG "Action when pressed")
:::

:::VerticalSplitItem
This example shows two scenarios, the first opens a different jig when the component is pressed and the second opens a URL when pressed. Use the `onPress` property to set up an action when pressing on the component.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-onpress.jigx).
:::
::::

:::CodeblockTabs
countdown-OnPress.jigx

```yaml
children:
  - type: component.section
    options:
      title: COUNTDOWN - G0-T0 JIG WHEN PRESSED
      children:
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + 360000)
            onPress: 
              type: action.go-to
              options:
                linkTo: countdown-sizes

  - type: component.section
    options:  
      title: COUNTDOWN - OPEN URL WHEN PRESSED
      
      children:
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + 360000)     
            onPress: 
              type: action.open-url
              options:
               url: https://www.tourismthailand.org/Destinations/Provinces/Phuket/350
        - type: component.web-view
          options: 
            uri: https://www.tourismthailand.org/Destinations/Provinces/Phuket/350          
```

countdown-sizes.jigx

```yaml
title: Countdown - size
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1531303435785-3853ba035cda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTh8fHByb21vdGlvbnxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60
        title: Countdown - sizes

children:
  - type: component.section
    options:
      title: COUNTDOWN SIZE - EXTRA-LARGE
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: extra-large      

  - type: component.section
    options:
      title: COUNTDOWN SIZE - LARGE (Default)
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: large
          
  - type: component.section
    options:
      title: COUNTDOWN SIZE - MEDIUM
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: medium

  - type: component.section
    options:
      title: COUNTDOWN SIZE - SMALL
      children:
      - type: component.countdown
        options:
          expiresAt: =$fromMillis($toMillis($now()) + 36000000)
          size: small
```
:::
:::::

:::::ExpandableHeading
### Countdown onFinish

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
In this example the `onFinish` property is used to show a modal when the `component.countdown` `expiresAt` property reaches zero.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-onfinish.jigx).
:::

:::VerticalSplitItem
![Modal when countdown expires](https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_Cmtlj3SADsfj7CruXBXF-20240822-125634.PNG "Modal when countdown expires")
:::
::::

:::CodeblockTabs
count-down-onFinish.jigx

```yaml
 children:
        - type: component.countdown
          options:
            expiresAt: =$fromMillis($toMillis($now()) + 3600)
            onFinish: 
              type: action.info-modal
              options:
                modal:
                  title: 🏖️ Holiday time!
                  buttonText: Enjoy!
```
:::
:::::

:::::ExpandableHeading
### Countdown started from another jig

::::VerticalSplit{layout="right"}
:::VerticalSplitItem
![Countdown from jig input](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-R9XOjo8mV7rhiI2DHdOQW-20250304-070603.png "Countdown from jig input")
:::

:::VerticalSplitItem
Add inputs from another jig to set the `expiresAl` property for the countdown to start.

**Example:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/countdown-jig-input.jigx).

Supporting example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/countdown/start-countdown-support.jigx).
:::
::::

:::CodeblockTabs
count-down-jig-input.jigx

```yaml
title: =@ctx.jig.inputs.packageName
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://plus.unsplash.com/premium_photo-1675989167596-915a77b361e5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8ODN8fGhvbGlkYXl8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60
        

children:                                
  - type: component.countdown
    options:
      size: extra-large  
      expiresAt: =@ctx.jig.inputs.packageDate
      
actions:
  - children:
      - type: action.info-modal
        options:
          title: =@ctx.jig.inputs.packagePrice & " - BUY"
          modal:
            title: Let the countdown begin!
            buttonText: Close
            element: 
              type: image
              resizeMode: contain
              uri: https://plus.unsplash.com/premium_photo-1680466283263-91b51ab91832?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OXx8YmVhY2glMjB1bWJyZWxsYXxlbnwwfHwwfHx8MA%3D%3D
```

start-countdown-support.jigx

```yaml
title: Island Holiday Packages
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1440778303588-435521a205bc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8aG9saWRheXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60
          
datasources:
  packages:
    type: datasource.static
    options:
      data: 
        - name: Thailand
          days: 30
          description: "10 days in luxury accomodation"
          Price: "$ 1500"
        - name: Phuket
          days: 60
          description: "7 days experience cultural activities"
          Price: "$ 1000"
        - name: Mauritius
          days: 120
          description: "8 days includes watersports"   
          Price: "$ 2350"
        - name: Bali
          days: 95
          description: "15 days all inclusive experience"
          Price: "$ 3760"
data: =@ctx.datasources.packages
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.description
    rightElement: 
      element: button
      title: =$fromMillis($toMillis($now()) + (@ctx.current.item.days * 24 * 60 * 60 * 1000), '[Y0001]-[M01]-[D01]')
     
      onPress: 
        type: action.go-to
        options:
          linkTo: countdown-jig-input
          parameters:
            packageDate: =$fromMillis($toMillis($now()) + (@ctx.current.item.days * 24 * 60 * 60 * 1000))
            packagePrice: =@ctx.current.item.Price
            packageName: =@ctx.current.item.name
```
:::
:::::

