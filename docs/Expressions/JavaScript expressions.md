---
title: JavaScript expressions
slug: fRwc-me
createdAt: Wed May 22 2024 12:31:51 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Oct 11 2024 09:14:53 GMT+0000 (Coordinated Universal Time)
---

JavaScript functions allow you to write modular and reusable code. By encapsulating specific functionalities within functions, you can easily reuse them across different parts of your application. This modular approach not only reduces redundancy but also makes the codebase more maintainable and scalable. For example, a function that handles user date and time can be reused in multiple components or screens, ensuring consistency and reducing the likelihood of errors.

Refer to the section on [JavaScript expressions]() to learn:

- [What is supported]()
- [How and where to configure the JavaScript functions]()

## Examples and code snippets

## Text formatting

:::::ExpandableHeading
### Return a string

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-sS6PAehgDxXFhL9p0MOSe-20240919-062431.PNG" size="70" position="center" caption="JavaScript function returning a string" alt="JavaScript function returning a string"}
:::

:::VerticalSplitItem
In this example, a JavaScript function called helloWorld is created to return a string showing *Hello World*  in a [text-field](./../Components/form/text-field.md). In the `value` property an expression calling the function is used.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-string.jigx).



:::
::::

:::CodeblockTabs
hello-world.jigx

```yaml
title: helloWorld
description: |
  The function returns static text Hello World
type: jig.default
icon: dog

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: textField
          options:
            label: Function Result
# Use an expression and call the JavaScript file and function in the file.            
            value: =$jsfunctions.helloWorld()
```

jsfunctions.js

```javascript
export function helloWorld() {
  return 'Hello World'
}
```
:::
:::::

:::::ExpandableHeading
### Concatenate first and last name

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Create a full name by joining a first and last name using a simple JavaScript function, but using JSONata offers a faster and more efficient approach due to its inline nature.  In the `value` property [text-field](./../Components/form/text-field.md) an expression is used that calls the function to provide the full name. The functions variables values are defined in the form's text-field components.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-concatenate.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY--3XKaQJ8QzDJviYHr82mq-20240919-064930.PNG" size="70" position="center" caption="Concatenate JavaScript Function " alt="Concatenate JavaScript Function "}
:::
::::

:::CodeblockTabs
fullname.jigx

```yaml
title: getFullName
description: Creating a full name from a first and last name can be done using a simple JavaScript function, but using JSONata offers a faster and more efficient approach due to its inline nature.
type: jig.default
icon: dog-carrying-bring-play-ball

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: firstName
          options:
            label: First Name
            initialValue: Bobby
        - type: component.text-field
          instanceId: lastName
          options:
            label: Last Name
            initialValue: Smith
        - type: component.text-field
          instanceId: fullName
          options:
            label: Full Name
# Use an expression and call the JavaScript file and function in the file.
# Provide the values to be used in the function by referencing components values.                        
            value: =$jsfunctions.getFullName(@ctx.components.firstName.state.value, @ctx.components.lastName.state.value)
            style:
              isDisabled: true
              
```

jsfunctions.js

```javascript
export function getFullName(firstName, lastName) {
  return firstName + ' ' + lastName;
}
```
:::
:::::

:::::ExpandableHeading
### Capitalize job title

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Rxqd_ngkDbzh4qCeqA-kW-20240919-065058.PNG" size="70"  position="center" caption="Capatilize job title function" alt="Capatilize job title function"}
:::

:::VerticalSplitItem
The function capitalizes the first letter of each word in a string while fully capitalizing specific acronyms such as CEO, COO, CFO, CTO, CIO, CMO, CSO, CPO, CHRO, and CDO. This ensures that job titles are formatted accurately, respecting the conventions for common acronyms. In the `value` property an expression is used that calls the function to capitalize the job title. The functions variables values are defined in the form's text-field components.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-capitalize-text.jigx).
:::
::::

:::CodeblockTabs
job-title.jigx

```yaml
title: capitalizeJobTitle
description: |
  The capitalizeJobTitle function capitalizes the first letter of each word in a string while fully capitalizing specific acronyms such as CEO, COO, CFO, CTO, CIO, CMO, CSO, CPO, CHRO, and CDO. This ensures that job titles are formatted accurately, respecting the conventions for common acronyms.
type: jig.default
icon: dog-race-compettion-2

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: jobTitle
          options:
            label: Job Title
            initialValue: Product marketing manager
        - type: component.text-field
          instanceId: formattedText
          when: =@ctx.components.jobTitle.state.value != ''
          options:
            label: Capitilized Job Title
# Use an expression and call the JavaScript file and function in the file.
# Provide the values to be used in the function by referencing components values.                            
            value: =$jsfunctions.capitalizeJobTitle(@ctx.components.jobTitle.state.value)
```

jsfunctions.js

```javascript
export function capitalizeJobTitle(str) {
  if (!str) {
    return '';
  }

  const exceptions = ['CEO', 'COO', 'CFO', 'CTO', 'CIO', 'CMO', 'CSO', 'CPO', 'CHRO', 'CDO'];

  return str.split(' ').map(word => {
    if (exceptions.includes(word.toUpperCase())) {
      return word.toUpperCase();
    }
    return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
  }).join(' ');
}
```
:::
:::::

## Numbers and dates

:::::ExpandableHeading
### Calculate tax plus total

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example three functions are used:

- The **calculateTax** function is designed to compute the tax amount based on a given subtotal and a specified tax rate. It takes two parameters: subtotal, which represents the pre-tax amount, and taxRate, which is the tax percentage to be applied.
- The **calculateTotal** function takes a subtotal and a tax rate, calculates the tax, adds it to the subtotal to get the total.
- The **formatCurrency** function converts a numerical amount into a string formatted as currency, including commas for thousands and two decimal places, and prefixes it with the specified currency symbol.

In the `value` property of the `text-field` an expression is used that calls the function to show the tax and the total. The functions variables values are defined in the form's text-field components.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-calculation.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-KAFfpDrBMtsqtzdjsS6d0-20240919-065231.PNG" size="70" position="center" caption="Function calculating tax" alt="Function calculating tax"}
:::
::::

:::CodeblockTabs
tax.jigx

```yaml
title: calculateTax & calculateTotal
description: |
  The calculateTax function is designed to compute the tax amount based on a given subtotal and a specified tax rate. It takes two parameters: subtotal, which represents the pre-tax amount, and taxRate, which is the tax percentage to be applied.
  
  Take a look at the configuration of Total Amount. You can use a function as a parameter for another function. 
type: jig.default
icon: dog-bark

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: subTotal
          options:
            label: Sub Total
            initialValue: =$number(345.78)
            format:
              numberStyle: currency
              currencyDisplay: symbol
              currencySign: standard
        - type: component.text-field
          instanceId: taxRate
          options:
            label: Tax Rate
            initialValue: =$number(8.6)
            format:
              numberStyle: percent
        - type: component.text-field
          instanceId: tax
          options:
            label: TAX
# Use an expression and call the JavaScript file and functions in the file.
# Nest functions in the expression to get the result you require
# Provide the values to be used in the function by referencing components values.                                   
            value: |
              =$jsfunctions.formatCurrency(
                  $jsfunctions.calculateTax(
                    @ctx.components.subTotal.state.value, 
                    @ctx.components.taxRate.state.value)
                ,'$')
            style:
              isDisabled: true
        - type: component.text-field
          instanceId: totalAmount
          options:
            label: Total Amount
# Use an expression and call the JavaScript file and functions in the file.
# Nest functions in the expression to get the result you require
# Provide the values to be used in the function by referencing components values.                                               
            value: |
              =$jsfunctions.formatCurrency(
                  $jsfunctions.calculateTotal(
                    $number(@ctx.components.subTotal.state.value),
                    $number($jsfunctions.calculateTax(@ctx.components.subTotal.state.value, @ctx.components.taxRate.state.value)))
                ,'$')
            style:
              isDisabled: true
```

jsfunctions.js

```javascript
export function calculateTax(subtotal, taxRate) {
  const tax = subtotal * (taxRate / 100);
  return Math.round(tax * 100) / 100;
}

export function calculateTotal(subtotal, taxRate) {
  const tax = subtotal * (taxRate / 100);
  const total = subtotal + tax;
  return total;
}

export function formatCurrency(amount, currencySymbol) {
  return currencySymbol + parseFloat(amount).toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
}
```
:::
:::::

:::::ExpandableHeading
### Calculate loan payment

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Fpz7MLSFjObQEogI1-XhE-20240919-070345.PNG" size="70" position="center" caption="Calulate loan payment function" alt="Calulate loan payment function"}
:::

:::VerticalSplitItem
The **calculateLoanPayment** function calculates the monthly loan payment based on the principal amount, annual interest rate (as a percentage), and loan term in years. This function is useful for financial applications that calculate monthly mortgage or loan payments based on the principal amount, annual interest rate, and loan term in years. It helps users determine their monthly payment obligations accurately.

The **formatCurrency** function converts a numerical amount into a string formatted as currency, including commas for thousands and two decimal places, and prefixes it with the specified currency symbol.

In the `value` property of the `text-field` an expression is used that calls the function to show the monthly repayment amount. The functions variables values are defined in the form's `text-field` components.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-loan-payment.jigx).
:::
::::

:::CodeblockTabs
loan-repayment.jigx

```yaml
title: calculateLoanPayment
description: |
  The function calculates the monthly loan payment based on the principal amount, annual interest rate (as a percentage), and loan term in years.
  
  This function is useful for financial applications that calculate monthly mortgage or loan payments based on the principal amount, annual interest rate, and loan term in years. It helps users determine their monthly payment obligations accurately.
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
          
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: principal
          options:
            label: Loan Amount
            initialValue: =$number(830000)
        - type: component.text-field
          instanceId: annualRatePercent
          options:
            label: Annual Rate (%)
            initialValue: =$number(5.5)
        - type: component.text-field
          instanceId: loanDuration
          options:
            label: Loan Duration (years)
            initialValue: =$number(30)
        - type: component.text-field
          instanceId: loanPayment
          options:
            label: Estimated monthly payment amount
# Use an expression and call the JavaScript file and functions in the file.
# Nest functions in the expression to get the result you require
# Provide the values to be used in the function by referencing components values.                                                           
            value: =$jsfunctions.formatCurrency($jsfunctions.calculateLoanPayment(@ctx.components.principal.state.value, @ctx.components.annualRatePercent.state.value, @ctx.components.loanDuration.state.value),'$')
            style:
              isDisabled: true
```

jsfunction.js

```javascript
export function calculateLoanPayment(principal, annualRatePercent, years) {
  const annualRate = annualRatePercent / 100; // Convert percentage to decimal
  const monthlyRate = annualRate / 12;
  const numberOfPayments = years * 12; // Calculate the total number of payments

  return (principal * monthlyRate) / (1 - Math.pow(1 + monthlyRate, -numberOfPayments));
}

export function formatCurrency(amount, currencySymbol) {
  return currencySymbol + parseFloat(amount).toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
}
```
:::
:::::

:::::ExpandableHeading
### Calculate age

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The **calculateAge** function determines a person's age based on their date of birth provided in the YYYY-MM-DD format.
This function is particularly useful in scenarios requiring age verification, such as user registration forms, social media profile management, or determining eligibility for age-restricted services.

A `date-picker` is used to select the date of birth, which is set as a state using the `onChange` event. The state's `value` uses an expression with a function to calculate the age and show it in a `text-field`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-calculate-age.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-v8Gc91Be3cfzuVlTQwVU0-20240919-070438.PNG" size="70" position="center" caption="Function to calulate age" alt="Function to calulate age"}
:::
::::

:::CodeblockTabs
age-calculation.jigx

```yaml
title: calculateAge
description: |
  The calculateAge function determines a person's age based on their date of birth provided in the YYYY-MM-DD format. 
  
  This function is particularly useful in scenarios requiring age verification, such as user registration forms, social media profile management, or determining eligibility for age-restricted services.
type: jig.default
icon: dog-playing-ball

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.date-picker
          instanceId: dob
          options:
            label: Date of Birth
            onChange: 
              type: action.set-state
              options:
                state: =@ctx.solution.state.age
# Use an expression and call the JavaScript file and functions in the file and set the result in a state.
# Provide the values to be used in the function by referencing the date picked in the component.                                                           
                value: =$jsfunctions.calculateAge(@ctx.components.dob.state.value)
        - type: component.text-field
          instanceId: result
          when: =@ctx.components.result.state.value = 'NaN' ? false:true
          options:
            label: Age
            value: =@ctx.solution.state.age
```

jsfunctions.js

```javascript
export function calculateAge(dateOfBirth) {
  if (!dateOfBirth) {
    return NaN;
  }
  // Parse the date of birth
  const dob = new Date(dateOfBirth);
  
  // Get today's date
  const today = new Date();
  
  // Calculate the difference in years
  let age = today.getFullYear() - dob.getFullYear();
  
  // Adjust the age if the birthdate hasn't occurred yet this year
  const monthDifference = today.getMonth() - dob.getMonth();
  const dayDifference = today.getDate() - dob.getDate();
  if (monthDifference < 0 || (monthDifference === 0 && dayDifference < 0)) {
    age--;
  }
  
  return age;
}
```
:::
:::::

:::::ExpandableHeading
### Distance between two cities

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The **distanceApart** function takes the longitude and latitude coordinates of two cities and calculates the straight-line distance between them, as the crow flies.
Use a dropdown to select the to and from cities. When a selection is made the `onChange` sets the state of the dropdown by using a function in the expression to work out the latitude and longitude of the selected city and the distance between them. The distance is shown in a `text-field`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-distance-apart.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-34cdIrfKMEk4HmN3eBiOo-20240919-070527.PNG" size="70" position="center" caption="Function to calculate distance" alt="Function to calculate distance"}
:::
::::
:::::

:::CodeblockTabs
distance.jigx

```yaml
title: distanceApart
description: |
  The distanceApart function takes the longitude and latitude coordinates of two cities and calculates the straight-line distance between them, as the crow flies.
type: jig.default
icon: dog-jump

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
          
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

datasources:
  majorCities:
    type: datasource.static
    options:
      data:

        - "id": 1
          "name": "Atlanta"
          "state": "GA"
          "long": -84.388
          "lat": 33.749

        - "id": 2
          "name": "Austin"
          "state": "TX"
          "long": -97.7431
          "lat": 30.2672

        - "id": 3
          "name": "Boston"
          "state": "MA"
          "long": -71.0589
          "lat": 42.3601

        - "id": 4
          "name": "Chicago"
          "state": "IL"
          "long": -87.6298
          "lat": 41.8781

        - "id": 5
          "name": "Dallas"
          "state": "TX"
          "long": -96.797
          "lat": 32.7767

        - "id": 6
          "name": "Denver"
          "state": "CO"
          "long": -104.9903
          "lat": 39.7392

        - "id": 7
          "name": "Detroit"
          "state": "MI"
          "long": -83.0458
          "lat": 42.3314
      
        - "id": 8
          "name": "Houston"
          "state": "TX"
          "long": -95.3698
          "lat": 29.7604
      
        - "id": 9
          "name": "Las Vegas"
          "state": "NV"
          "long": -115.1398
          "lat": 36.1699

        - "id": 10
          "name": "Los Angeles"
          "state": "CA"
          "long": -118.2437
          "lat": 34.0522

        - "id": 11
          "name": "Miami"
          "state": "FL"
          "long": -80.1918
          "lat": 25.7617

        - "id": 12
          "name": "Minneapolis"
          "state": "MN"
          "long": -93.265
          "lat": 44.9778

        - "id": 13
          "name": "New York"
          "state": "NY"
          "long": -74.006
          "lat": 40.7128

        - "id": 14
          "name": "Orlando"
          "state": "FL"
          "long": -81.3792
          "lat": 28.5383
      
        - "id": 15
          "name": "Philadelphia"
          "state": "PA"
          "long": -75.1652
          "lat": 39.9526

        - "id": 16
          "name": "Phoenix"
          "state": "AZ"
          "long": -112.074
          "lat": 33.4484
      
        - "id": 17
          "name": "San Antonio"
          "state": "TX"
          "long": -98.4936
          "lat": 29.4241
      
        - "id": 18
          "name": "San Diego"
          "state": "CA"
          "long": -117.1611
          "lat": 32.7157

        - "id": 19
          "name": "San Francisco"
          "state": "CA"
          "long": -122.4194
          "lat": 37.7749

        - "id": 20
          "name": "Seattle"
          "state": "WA"
          "long": -122.3321
          "lat": 47.6062

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.field-row
          options:
            children:      
              - type: component.dropdown
                instanceId: fromCity
                options:
                  label: From
                  data: =@ctx.datasources.majorCities
                  item:
                    type: component.dropdown-item
                    options:
                      title: =@ctx.current.item.name & ' (' & @ctx.current.item.state & ')'
                      value: =@ctx.current.item.id
                  onChange: 
                    type: action.set-state
                    options:
 # Use an expression and call the JavaScript file and functions in the file and set the result in a state.
# Provide the values to be used in the function by referencing the dropdown component.                    
                      state: =@ctx.solution.state.distance
                      value: =$round($jsfunctions.distanceApart(@ctx.components.fromCity.state.selected.long, @ctx.components.fromCity.state.selected.lat, @ctx.components.toCity.state.selected.long, @ctx.components.toCity.state.selected.lat), 0)
    
              - type: component.dropdown
                instanceId: toCity
                options:
                  label: To
                  data: =@ctx.datasources.majorCities
                  item:
                    type: component.dropdown-item
                    options:
                      title: =@ctx.current.item.name & ' (' & @ctx.current.item.state & ')'
                      value: =@ctx.current.item.id
                  onChange: 
                    type: action.set-state
                    options:
                      state: =@ctx.solution.state.distance
# Use an expression and call the JavaScript file and functions in the file and set the result in a state.
# Provide the values to be used in the function by referencing the dropdown component.                                                                                
                      value: =$round($jsfunctions.distanceApart(@ctx.components.fromCity.state.selected.long, @ctx.components.fromCity.state.selected.lat, @ctx.components.toCity.state.selected.long, @ctx.components.toCity.state.selected.lat), 0)
    
        - type: component.text-field
          instanceId: distance
          when: =@ctx.components.distance.state.value = 'NaN' ? false:true
          options:
            label: Distance (in Miles)
# Show the value set by the js function set in the state.            
            value: =@ctx.solution.state.distance
            style:
              isDisabled: true
```

jsfunctions.js

```javascript
export function distanceApart(from_long, from_lat, to_long, to_lat) {
  // Function to convert degrees to radians
  function toRadians(degrees) {
      return degrees * Math.PI / 180;
  }

  // Radius of the Earth in miles
  var R = 3958.8;

  // Difference in coordinates
  var dLat = toRadians(to_lat - from_lat);
  var dLon = toRadians(to_long - from_long);

  // Current lat and long in radians
  var lat1 = toRadians(from_lat);
  var lat2 = toRadians(to_lat);

  // Haversine formula
  var a = Math.sin(dLat / 2) * Math.sin(dLat / 2) +
      Math.sin(dLon / 2) * Math.sin(dLon / 2) * Math.cos(lat1) * Math.cos(lat2);
  var c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
  var distanceBetweenPoints = R * c;

  return distanceBetweenPoints;
}

```
:::

:::::ExpandableHeading
### Days to next state holiday

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-zdFI128LpCKcf65Goy_tI-20240919-070950.PNG" size="70" position="center" caption="Function calculating dates" alt="Function calculating dates"}
:::

:::VerticalSplitItem
The **daysUntil** function calculates the number of days remaining from today's date until a specified future date provided in the YYYY-MM-DD format. It returns the number of days remaining.

Use a `dropdown` to select holiday. When a selection is made the `onChange` sets the state of the dropdown by using a function in the expression to work out the number of days to the date of the holiday. The number of days is shown in a `text-field`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-days-until.jigx).

:::
::::

:::CodeblockTabs
holidays.jigx

```yaml
title: daysUntil
description: |
  The daysUntil function calculates the number of days remaining from today's date until a specified future date provided in the YYYY-MM-DD format. It returns the number of days remaining.
type: jig.default
icon: dog-play-bring-disc

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

datasources:
  holidays: 
    type: datasource.static
    options:
      data:
      - "name": "New Year's Day"
        "date": "2024-01-01"
        "description": "Celebration of the first day of the new year."

      - "name": "Valentine's Day"
        "date": "2024-02-14"
        "description": "A day to celebrate love and affection between intimate partners."

      - "name": "St. Patrick's Day"
        "date": "2024-03-17"
        "description": "A cultural and religious celebration held on the anniversary of Saint Patrick's death."
    
      - "name": "Easter"
        "date": "2024-03-31"
        "description": "A Christian holiday celebrating the resurrection of Jesus Christ from the dead."
      
      - "name": "Memorial Day"
        "date": "2024-05-27"
        "description": "A federal holiday in the United States for honoring and mourning the military personnel who have died in the performance of their military duties."

      - "name": "Independence Day"
        "date": "2024-07-04"
        "description": "A federal holiday in the United States commemorating the Declaration of Independence."
      
      - "name": "Labor Day"
        "date": "2024-09-02"
        "description": "A federal holiday in the United States to honor and recognize the American labor movement."

      - "name": "Halloween"
        "date": "2024-10-31"
        "description": "A celebration observed in many countries on the eve of the Western Christian feast of All Hallows' Day."

      - "name": "Thanksgiving"
        "date": "2024-11-28"
        "description": "A national holiday in the United States celebrating the harvest and other blessings of the past year."

      - "name": "Christmas"
        "date": "2024-12-25"
        "description": "An annual festival commemorating the birth of Jesus Christ observed primarily on December 25."

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.dropdown
          instanceId: holiday
          options:
            label: Select holiday
            data: =@ctx.datasources.holidays
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.date
            onChange: 
              type: action.set-state
              options:
                state: =@ctx.solution.state.daysUntil
# Use an expression and call the JavaScript file and functions in the file and set the result in a state.
# Provide the values to be used in the function by referencing the dropdown component.                                                                                                
                value: =$jsfunctions.daysUntil(@ctx.components.holiday.state.value)
        - type: component.text-field
          instanceId: days
          when: =@ctx.components.days.state.value = 'NaN' ? false:true
          options:
            label: Days to go
# Show the value set by the js function set in the state.            
            value: =@ctx.solution.state.daysUntil
```

jsfunctions.js

```javascript
export function daysUntil(targetDate) {
  if (!targetDate) {
    return NaN;
  }

  // Get today's date
  const today = new Date();
  const target = new Date(targetDate);

  // Set the target year to this year
  target.setFullYear(today.getFullYear());

  // If the target date has already passed this year, set it to next year
  if (target < today) {
    target.setFullYear(today.getFullYear() + 1);
  }

  // Calculate the difference in time
  const timeDifference = target - today;

  // Convert the time difference to days
  const daysDifference = Math.ceil(timeDifference / (1000 * 60 * 60 * 24));

  return daysDifference;
}
```
:::
:::::

:::::ExpandableHeading
### Work days left in a month

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
&#x20;The **workdaysLeftInMonth** function calculates the number of workdays (Monday to Friday) remaining in the month from a given date. This function is useful in business applications where the number of remaining workdays from a specific date is important for scheduling, project management, or payroll processing.

A `date-picker` is used to select the current date. An expression with the function is used to calulate the number of days and show it in a `text-field`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-work-days.jigx).

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Pva5AwlWD10wNpLtoKIJv-20240919-071234.PNG" size="70" position="center" caption="Function calulating dates" alt="Function calulating dates"}
:::
::::

:::CodeblockTabs
work-days-month.jigx

```yaml
title: workdaysLeftInMonth
description: |
  The workdaysLeftInMonth function calculates the number of workdays (Monday to Friday) remaining in the month from a given date.
  
  This function is useful in business applications where the number of remaining workdays from a specific date is important for scheduling, project management, or payroll processing.
type: jig.default
icon: dog-sit

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.date-picker
          instanceId: date
          options:
            label: Date
            initialValue: =$now()
        - type: component.text-field
          instanceId: daysRemaining
          when: =@ctx.components.daysRemaining.state.value != 'NaN'
          options:
            label: Work days left for this month
# Use an expression and call the JavaScript file and functions in the file 
# Provide the values to be used in the function by referencing the date component's.                                                                                                           
            value: =$jsfunctions.workdaysLeftInMonth(@ctx.components.date.state.value)
            style:
              isDisabled: true
```

jsfunctions.js

```javascript
export function workdaysLeftInMonth(date) {
  if (!date) {
    return NaN;
  }

  const inputDate = new Date(date);
  const currentYear = inputDate.getFullYear();
  const currentMonth = inputDate.getMonth();
  
  // Get the last day of the current month
  const lastDayOfMonth = new Date(currentYear, currentMonth + 1, 0);

  let workdaysCount = 0;

  // Iterate through each day from the input date to the end of the month
  for (let day = inputDate.getDate(); day <= lastDayOfMonth.getDate(); day++) {
    const currentDate = new Date(currentYear, currentMonth, day);
    const dayOfWeek = currentDate.getDay();
    
    // Check if the current day is a weekday (Monday to Friday)
    if (dayOfWeek !== 0 && dayOfWeek !== 6) {
      workdaysCount++;
    }
  }

  return workdaysCount;
}
```
:::
:::::

:::::ExpandableHeading
### Next work day

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-T89tiGP1BRtcfVbTCfH4i-20240919-071417.PNG" size="70" position="center" caption="Function calulating dates" alt="Function calulating dates"}
:::

:::VerticalSplitItem
The **getNextBusinessDay** function calculates the next business day from a given date. It returns the next valid business day in the format "Month Day, Year".
A `date-picker` is used to select the current date. An expression with the function is used to calulate the number of days and shows it in a `text-field`.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-next-business-day.jigx).
:::
::::

:::CodeblockTabs
next-work-day

```yaml
title: getNextBusinessDay
description: |
  The getNextBusinessDay function calculates the next business day from a given date. It returns the next valid business day in the format "Month Day, Year".
  
  In a business application, this function can be used to determine the next available working day for scheduling meetings, processing orders, or planning project deadlines.
type: jig.default
icon: dog-sit-1

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.date-picker
          instanceId: date
          options:
            label: Date
            initialValue: =$now()
            onChange: 
              type: action.set-state
              options:
                state: =@ctx.solution.state.nextBusinessDay
# Use an expression and call the JavaScript file and functions in the file and set the result in a state.. 
# Provide the values to be used in the function by referencing the date component's.                                                                                                                       
                value: =$jsfunctions.getNextBusinessDay(@ctx.components.date.state.value)
        - type: component.text-field
          instanceId: result
          when: =@ctx.components.result.state.value = 'NaN' ? false:true
          options:
            label: Next business day
# Show the value set by the js function set in the state.            
            value: =@ctx.solution.state.nextBusinessDay
            style:
              isDisabled: true
```

jsfunction.js

```javascript
import { addDays, isWeekend, format } from 'date-fns';
export function getNextBusinessDay(date) {
  let nextDay = addDays(date, 1);
  while (isWeekend(nextDay)) {
    nextDay = addDays(nextDay, 1);
  }
  return format(nextDay, 'MMMM d, yyyy');
}
```
:::
:::::

## If conditions

:::::ExpandableHeading
### Format phone number

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-BIw_ynmL8VIQBmMbPevzB-20240919-071457.PNG" size="70" position="center" caption="Function to format numbers" alt="Function to format numbers"}
:::

:::VerticalSplitItem
The **formatPhoneNumber** function formats a 10-digit telephone number into the (XXX) XXX-XXXX format. It removes all non-digit characters, checks if the length is correct, and then formats the cleaned number accordingly.
This function is useful in applications that require consistent formatting of user input for telephone numbers, such as contact forms, user profiles, or customer service systems. It ensures that telephone numbers are displayed in a standardized and readable format.
The `value` property of the `text-field `uses an expression that calls the function.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-format-number.jigx).
:::
::::

:::CodeblockTabs
phone-number.jigx

```yaml
title: formatPhoneNumber
description: |
  The formatPhoneNumber function formats a 10-digit telephone number into the (XXX) XXX-XXXX format. It removes all non-digit characters, checks if the length is correct, and then formats the cleaned number accordingly.
  
  This function is useful in applications that require consistent formatting of user input for telephone numbers, such as contact forms, user profiles, or customer service systems. It ensures that telephone numbers are displayed in a standardized and readable format.
type: jig.default
icon: dog-sit-1

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.components.myForm.state.data

children:
  - type: component.form
    instanceId: myForm
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: phoneNumber
          options:
            label: Phone Number
            initialValue: '4253892293'
        - type: component.text-field
          instanceId: formattedPhone
          options:
            label: Formatted Phone Number
# Use an expression and call the JavaScript file and function in the file.
# Provide the values to be used in the function by referencing the phone number.             
            value: =$jsfunctions.formatPhoneNumber(@ctx.components.phoneNumber.state.value)
            style:
              isDisabled: true
```

jsfunction.js

```javascript
export function formatPhoneNumber(phoneNumber) {
  // Remove all non-digit characters
  const cleaned = ('' + phoneNumber).replace(/\D/g, '');
  
  //console.log(cleaned)
  //console.error(cleaned)
  //console.warn(cleaned)
  //console.trace(cleaned)
  //console.debug(cleaned)

  // Check if the input is of correct length
  if (cleaned.length !== 10) {
    return 'Invalid phone number';
  }

  // Format the cleaned number
  const part1 = cleaned.substring(0, 3);
  const part2 = cleaned.substring(3, 6);
  const part3 = cleaned.substring(6, 10);

  return `(${part1}) ${part2}-${part3}`;
}
```
:::
:::::

## Working with objects

:::::ExpandableHeading
### Get employee details

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The **getEmployeeInfo** function constructs a formatted string from an object that includes an employee's first name, last name, position, and email address.
The `value` property of the entity-field uses an expression that calls the function.

**Example:**
See the example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-javascript-expressions/js-format-string-object.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-JoQEp6Les6BrVKrp2oBmq-20240919-072252.PNG" size="70" position="center" caption="Function returning an object" alt="Function returning an object"}
:::
::::

:::CodeblockTabs
employee.jigx

```yaml
title: getEmployeeInfo
description: |
  The getEmployeeInfo function constructs a formatted string from an object that includes an employee's first name, last name, position, and email address.
type: jig.default
icon: dog-sit-1

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://miro.medium.com/v2/resize:fit:720/format:webp/1*M9cY0UHTbmlBfoPMCQwxYA.png
datasources:
  employee:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/employee
  
      query: |
        SELECT
          emp.id as empID,
          json_extract(emp.data, '$.firstName') as firstName,
          json_extract(emp.data, '$.lastName') as lastName,
          json_extract(emp.data, '$.position') as position,
          json_extract(emp.data, '$.department') as department,
          json_extract(emp.data, '$.email') as email,
          json_extract(emp.data, '$.phone') as phone
        FROM
            [default/employee] as emp
        WHERE 
          empID = @empId
        
      queryParameters:
        empId: 'f03307a9-e6ab-4d78-af54-5f79c4d46ca2'
        
      isDocument: true

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Function result
# Use an expression and call the JavaScript file and function in the file.
# Provide the values to be used in the function by referencing the datasource.                         
            value: =$jsfunctions.getEmployeeInfo(@ctx.datasources.employee)
```

jsfunction.js

```javascript
export function getEmployeeInfo(employee) {
  console.log(`Name: ${employee.firstName} ${employee.lastName}`);
  return `${employee.firstName} ${employee.lastName} is a ${employee.position} and can be reached at ${employee.email}`;
}

export function calculateLoanPayment(principal, annualRatePercent, years) {
  const annualRate = annualRatePercent / 100; // Convert percentage to decimal
  const monthlyRate = annualRate / 12;
  const numberOfPayments = years * 12; // Calculate the total number of payments

  return (principal * monthlyRate) / (1 - Math.pow(1 + monthlyRate, -numberOfPayments));
}
```
:::
:::::

