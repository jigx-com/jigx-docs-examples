---
title: Create an app using REST APIs
slug: b2BB-hello
createdAt: Tue Apr 30 2024 08:11:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri May 10 2024 12:35:50 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
By integrating external REST APIs into your Jigx solutions, you can significantly enrich your apps with a wide range of data and functionality from various external sources, enhancing the overall user experience.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZsPx4oKIP0ciydTeJ9bqY_rest-hello4.gif" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZsPx4oKIP0ciydTeJ9bqY_rest-hello4.gif" size="86" width="314" height="630" position="center" caption}
:::
::::

## &#x20;REST concepts

- How to define the GET, PUT, PUSH, and DELETE REST operations in Jigx functions.
- How to define the REST parameters, headers, continuation, and body in the functions.
- How to configure input and output transforms in functions.
- How Jigx automatically syncs the IDs for new customers created in REST API to theJigx local data provider. (tempId to Id - useful when the app is offline).
- How to convert images into a format that is acceptable for REST and for Jigx.
- How to get the image metadata using output transform.
- How to reference the data in jigs (screens) and call the functions in actions.&#x20;

## What is created

In this section, a REST API is used to create a customer Jigx app that allows you to:

| **Functions & Jigs**                                                                                | **Functionality description**                                                                                                                               |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [List customers (GET)](<./Create an app using REST APIs/List customers _GET_.md>)                   | View a list of customers by status.                                                                                                                         |
| [Delete customer (DELETE)](<./Create an app using REST APIs/Delete customer _DELETE_.md>)           | Delete customers by swiping left.                                                                                                                           |
| [Create customer (POST)](<./Create an app using REST APIs/Create customer _POST_.md>)               | Capture new customers in a form.                                                                                                                            |
| [Update customer details (PUT)](<./Create an app using REST APIs/Update customer details _PUT_.md>) | Update customer details by swiping left on the list and selecting view, which populates a form with the customer's details with an update button.           |
| [List & View customers (GET)](<./Create an app using REST APIs/List _ View customers _GET_.md>)     | Return a list of customers in batches (`continuation`) and view customer details where addresses and phone are complex REST structures (`jsonProperties`).  |
| [List product images (GET)](<./Create an app using REST APIs/List product images _GET_.md>)         | View customer details, locations, and product images in a composite jig.                                                                                    |
| [Upload product images (POST)](<./Create an app using REST APIs/Upload product images _POST_.md>)   | Upload product images for the customer.                                                                                                                     |

## High-level steps

The REST data provider is used in Jigx to integrate with REST. In this section, we follow these high-level steps:

1. Identify the REST API to be used as your data source.&#x20;
2. Define a REST Service in a Jigx function in Jigx Builder.
3. Configure REST Authentication (if required).&#x20;
4. Define data operations in the function, such as GET, POST, PUT, and DELETE. For each operation, create a new function to specify the endpoint, required headers, URL parameters, input and output transforms, continuation, and body content if applicable.&#x20;
5. Reference the Jigx functions in jigs.
6. Publish your solution
7. Test the Data Provider.

:::hint{type="success"}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and REST API, which can help you integrate similar solutions into your projects more effectively.&#x20;
:::

