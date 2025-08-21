# Regex expressions

By combining regular (regex) expressions in your JSONata expressions in Jigx Builder, you can create complex patterns to match specific strings of text. Regex expressions are a sequence of characters that define a search pattern. It is powerful when used in text processing to find, replace, or validate strings of text. Some common uses of regex include:

* Validating email addresses or phone numbers
* Extracting specific information from a text file or document
* Reformatting data to match a specific pattern or structure

## Examples and code snippets

The JSONata + regex examples below create validation for `text-fields` in a `form`.

## Phone number validation

**Expected results:** Between 9 and 13 numbers with no spaces, can include a symbol for dialing code, e.g., +271234556789.

{% columns %}
{% column %}
::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Wtp8QVXWi56sJFxTHuOb9\_phone-valid.PNG" size="84" position="center" caption="Valid phone number" alt="Valid phone number" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Wtp8QVXWi56sJFxTHuOb9\_phone-valid.PNG" width="800" height="435" darkWidth="800" darkHeight="435"} :::


{% endcolumn %}

{% column %}
&#x20;![Invalid phone number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/MVDIqg6Q2JFQU9-Rlw8OL_phone-invalid.PNG)


{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: telephone
  options:
    label: Telephone
    errorText: =$contains(@ctx.components.telephone.state.value , /^((\+|0{0,2})([0-9]){1,3})?[-.●\s]?\(?([0-9]{2,3})\)?[-.●\s]?([0-9]{3})[-.●\s]?([0-9]{4})$/) ? '' :'not a phone number'  
```

## Email validation

**Expected result:** [name@example.com](mailto:name@example.com)

{% columns %}
{% column %}
&#x20;![Valid email address](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NP-TE2sDghjEcBbxXZURF_email-valid.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid email address](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/47lx4W1RTiP8bQd4wCB_u_email-invalid.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: email
  options:
    label: Email
    errorText: =$contains(@ctx.components.email.state.value, /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/) ? '' :'not an email'      
```

## Credit card validation

**Expected result:** Typically 13-16 digits, with spaces or dashes optional, and includes checks for Visa, MasterCard, American Express, and Discover. E.g. 1111-1111-1111-1111 or 1111 1111 1111 1111.

{% columns %}
{% column %}
&#x20;![Valid  credit card number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/raKfpW2ipLxhcMuLFtEfW_valid-cc.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid  credit card number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/PPPDn3zEIyobdLqLSu6kL_invalid-cc.PNG)
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: credit-card
  options:
    label: Credit card
    errorText: =$contains(@ctx.components.credit-card.state.value, /^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}|6(?:011|5[0-9]{2})[0-9]{12}|3[47][0-9]{13})$/) ? '' :'not a credit card number'    
```

## ZIP/Postal code (US) validation

**Expected result:** 5-digit codes, e.g. 10036.

{% columns %}
{% column %}
&#x20;![Valid ZIP code](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0BGX8SwNKHVRWtvtVtvSY_valid-zip.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid ZIP code](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Jl5cVZIbKuq4R4lR1h2vB_invalid-zip.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: zip
  options:
    label: ZIP/ Postal code
    errorText: =$contains(@ctx.components.zip.state.value, /^\d{5}(-\d{4})?$/) ? '' :'not a ZIP/ Postal code'    
```

## Social Security Number (US) validation

**Expected result:** XXX-XX-XXXX

{% columns %}
{% column %}
&#x20;![Valid Social Security number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/G6AVB6tYoliWEBumc5Kjr_valid-ss.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid Social Security number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xN7CGa7nPUj-yEBFb2tlQ_invalid-ss.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: social-security-number
  options:
    label: Social security number
    errorText: =$contains(@ctx.components.social-security-number.state.value, /^\d{3}-\d{2}-\d{4}$/) ? '' :'not a social security number'    
```

## National Insurance Number (UK) validation

**Expected result:** AA123456C

{% columns %}
{% column %}
&#x20;![Valid National Insurance number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/znto1cjyTCMyE9avaFet0_valid-ni.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid National Insurance number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-H4t0H6dwa0tQhypYVM4__invalid-ni.PNG)
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: national-insurance-number
  options:
    label: National Insurance Number
    errorText: =$contains(@ctx.components.national-insurance-number.state.value, /^(?!BG|GB|NK|KN|TN|NT|ZZ)[A-CEGHJ-PR-TW-Z][A-CEGHJ-NPR-TW-Z]\d{2}(?:\s*\d{2}){2}\s*[A-D]$/) ? '' :'not a national-insurance-number'    
```

## US Date (DD/MM/YYYY) validation

**Expected result:** DD/MM/YYYY, e.g. 23/07/2024.

{% columns %}
{% column %}
&#x20;![Valid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BfJyiQNFhzO8EMVQXkC_m_valid-dd-mm-yyyy.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x02lJfwhDU681kClzh8qc_invalid-dd-mm-yyyy.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: us-date
  options:
    label: Date - DD/MM/YYYY
    errorText: =$contains(@ctx.components.us-date.state.value, /^(0[1-9]|[12][0-9]|3[01])\/(0[1-9]|1[0-2])\/(19|20)\d{2}$/) ? '' :'not a valid date (DD/MM/YYYY)'
```

## Date (MM/DD/YYYY) validation

**Expected result:** MM/DD/YYYY, e.g. 03/28/2023.

{% columns %}
{% column %}
&#x20;![Valid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/JOggsXvLB82nmQAdcVxDy_valid-mm-dd.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/d3dz8IUWb6Cs0MXT4g-Qa_invalid-mm-dd.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: date
  options:
    label: Date - MM/DD/YYYY
    errorText: =$contains(@ctx.components.date.state.value, /^(0[1-9]|1[0-2])\/(0[1-9]|[12][0-9]|3[01])\/(19|20)\d{2}$/) ? '' :'not a valid date (MM/DD/YYYY)'    
```

## Date (DD Month YYYY) validation

**Expected result:** DD Month YYYY, e.g. 25 July 2024.

{% columns %}
{% column %}
&#x20;![Valid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pxR29s8XaU71Yg1fvzv09_valid-month.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_PGk4cAZ_E5sq1F-grjWn_invalid-month.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: date-with-month
  options:
    label: Date - DD Month YYYY
    errorText: =$contains(@ctx.components.date-with-month.state.value, /^(0[1-9]|[12][0-9]|3[01])\s(?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)\s(19|20)\d{2}$/) ? '' :'not a valid date (DD Month YYYY)'    
```

## Date (yyyy/mm/dd) validation

**Expected result:** yyyy/mm/dd, e.g. 2024/08/30.

{% columns %}
{% column %}
&#x20;![Valid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/b-dLT9gj-atCGF4-2GbET_valid-yyyymmdd.PNG)&#x20;


{% endcolumn %}

{% column %}
&#x20;![Invalid date format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fr-WSmJFjbkE1QjFzeN-2_invalid-yyyymmdd.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: date-year-first
  options:
    label: Date - YYYY/MM/DD
    errorText: =$contains(@ctx.components.date-year-first.state.value, /^(19|20)\d{2}\/(0[1-9]|1[0-2])\/(0[1-9]|[12][0-9]|3[01])$/) ? '' :'not a valid date format (YYYY/MM/DD)'    
```

## Decimal validation

**Expected result:** 1234,00

{% columns %}
{% column %}
&#x20;![Valid decimal number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9LW6cC_1pPDevWNocl3pJ_valid-decimal.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid decimal number](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lkFIgHhVKEv-FmE0TBFuN_invalid-decimal.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: decimal
  options:
    label: Decimal number - 111,2
    errorText: =$contains(@ctx.components.decimal.state.value, /^[0-9]+([,.][0-9]{1,2})?$/) ? '' :'not a decimal number'    
```

## Time (H:MM AM/PM) validation

**Expected result:** H:MM AM/PM e.g. 12:15 AM or 08:45 PM

{% columns %}
{% column %}
&#x20;![Valid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7SYz1j770opjA65qRgbpX_valid-time-am.PNG)
{% endcolumn %}

{% column %}
&#x20;![Invalid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fKD528Sn3FIv4aMZBVGuX_invalid-time-am.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: time
  options:
    label: Time - HH:MM AM/PM
    errorText: =$contains(@ctx.components.time.state.value, /^((0?[1-9]|1[0-2]):[0-5][0-9] (AM|PM))$/) ? '' :'not a valid time format, use HH:MM AM/PM'    
```

## Time (MM:SS / or HH:MM) validation

**Expected result:** MM:SS / or HH:MM, e.g. 08:10.

{% columns %}
{% column %}
&#x20;![Valid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/78ig1l7uYyvJ9pV2ZKByi_valid-hhmm.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/eIH6pgBEAvFgfMkBRCC6N_invalid-hhmm.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: time-2
  options:
     label: Time - MM:SS / or HH:MM
     errorText: =$contains(@ctx.components.time-2.state.value, /^(?:(?:([01]?\d|2[0-3]):)?([0-5]?\d):)?([0-5]?\d)$/) ? '' :'not a valid time format, use MM:SS / or HH:MM'   
```

## Time in 24-hour format

**Expected result:** 01:00

{% columns %}
{% column %}
&#x20;![Valid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bpfR2Forp61sTD-4jmy9v_valid-24.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid time format](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Ur681lwZagDKy-J0fmxQz_invalid-24.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: time-3
  options:
    label: Time - 24 hour format
    errorText: =$contains(@ctx.components.time-3.state.value, /^([01]?[0-9]|2[0-3]):[0-5][0-9]$/) ? '' :'not a valid time format, use 24 hour format'    
```

## URL validation

**Expected result:** example.com or [http://example.com](http://example.com)

{% columns %}
{% column %}
&#x20;![Valid URL](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/kBs2eilNTa2FEBUawSeTH_valid-url.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid URL](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/478vm6U2BFe_sdihLOey-_invalid-url.PNG)
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-fiel
  instanceId: url
  options:
    label: URL
    errorText: =$contains(@ctx.components.url.state.value, /^((https?|ftp|file):\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/) ? '' :'not a valid url format'    
```

## ISBN validation

**Expected result:** 978-1-4302-1998-9

{% columns %}
{% column %}
&#x20;![Valid ISBN](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LJZqMS9Fg3dPLAzu0X9Nr_valid-isbn.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid ISBN](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/L6V4uAF0UpazHhgfBTdxf_invalid-isbn.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: isbn
  options:
    label: ISBN
    errorText: =$contains(@ctx.components.isbn.state.value, /((978[\--– ])?[0-9][0-9\--– ]{10}[\--– ][0-9xX])|((978)?[0-9]{9}[0-9Xx])/) ? '' :'not a valid ISBN format'    
```

## Strict Alpha Numeric validation

**Expected result:** JohnSmith

{% columns %}
{% column %}
&#x20;![Valid string -no spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bdn0isKFPTwR4pthDzlXI_valid-string-space.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid string -no spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UugX-AGkcahdXHnFo2iiq_invalid-string-space.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: string
  options:
    label: String - spaces not allowed
    errorText: =$contains(@ctx.components.string.state.value, /^[a-zA-Z0-9]+$/) ? '' :'not a valid string, spaces are not allowed'    
```

## Alpha Numeric with spaces allowed validation

**Expected result:** John Smith

{% columns %}
{% column %}
&#x20;![Valid string with spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KFr9CxuqV01zvjCSxxArS_valid-string.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid string with spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZobDaOJvNVS7fhQPqV8jw_invalid-string.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: string-2
  options:
    label: String - spaces allowed
    errorText: =$contains(@ctx.components.string-2.state.value, /^[a-zA-Z0-9\s]*$/) ? '' :'not a valid string, spaces are allowed'    
```

## validation of numbers and Spaces only

**Expected result:** 56575 76 6

{% columns %}
{% column %}
&#x20;![Valid numbers with spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mMUC0JaR-I9cRDEiSPCx8_valid-num-space.PNG)&#x20;
{% endcolumn %}

{% column %}
&#x20;![Invalid numbers with spaces](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nae9RyMC6R9FSxDM6khVK_invalid-num-space.PNG)&#x20;
{% endcolumn %}
{% endcolumns %}

```yaml
- type: component.text-field
  instanceId: number-spaces
  options:
    label: Number and spaces only
    errorText: =$contains(@ctx.components.number-spaces.state.value, /^[0-9\s]*$/) ? '' :'not a valid input, use number and spaces only'      
```
