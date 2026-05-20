---
title: Database Scripts
slug: jQ3e-database-scripts
createdAt: Wed Mar 15 2023 12:32:13 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue May 21 2024 10:42:03 GMT+0000 (Coordinated Universal Time)
---

# Database Scripts

{% hint style="warning" %}
Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](https://docs.jigx.com/building-apps-with-jigx/data/data-providers/rest) instead. See [REST endpoints from Azure SQL](https://docs.jigx.com/building-apps-with-jigx/data/data-providers/microsoft-azure-sql) for more information.
{% endhint %}

The following Azure SQL scripts create the customer table and store the procedures used in the examples in this section. These scripts should be executed against an existing database in your Azure SQL environment.

## Create Customer Table

The following script creates a sample customer table in Microsoft Azure SQL.

{% code title="createCustomers.sql" fullWidth="true" %}
```sql
CREATE TABLE customers (
    id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
    first_name NVARCHAR(50) NOT NULL,
    last_name NVARCHAR(50) NOT NULL,
    email NVARCHAR(100) UNIQUE NOT NULL,
    phone_number NVARCHAR(15) UNIQUE,
    address_line1 NVARCHAR(100) NOT NULL,
    address_line2 NVARCHAR(100),
    city NVARCHAR(50) NOT NULL,
    state CHAR(2) NOT NULL DEFAULT 'WA',
    zip_code CHAR(5) NOT NULL,
    country NVARCHAR(50) NOT NULL DEFAULT 'USA'
);
```
{% endcode %}

## Insert sample records in the Customer table

The following script inserts sample customers into the table.

{% code title="insertCustomer.sql" fullWidth="true" %}
```sql
INSERT INTO customers (first_name, last_name, email, phone_number, address_line1, address_line2, city, zip_code)
VALUES
    ('John', 'Doe', 'john.doe@example.com', '206-555-0101', '123 Main St', 'Apt 4B', 'Seattle', '98101'),
    ('Jane', 'Smith', 'jane.smith@example.com', '360-555-0102', '456 Pine St', NULL, 'Bellevue', '98004'),
    ('Michael', 'Johnson', 'michael.johnson@example.com', '425-555-0103', '789 Oak St', NULL, 'Redmond', '98052'),
    ('Emily', 'Davis', 'emily.davis@example.com', '253-555-0104', '321 Elm St', 'Unit 3A', 'Tacoma', '98402'),
    ('William', 'Martinez', 'william.martinez@example.com', '509-555-0105', '654 Maple St', NULL, 'Spokane', '99201'),
    ('Elizabeth', 'Taylor', 'elizabeth.taylor@example.com', '206-555-0106', '987 Cedar St', NULL, 'Seattle', '98102'),
    ('David', 'Anderson', 'david.anderson@example.com', '360-555-0107', '147 Pineview Dr', NULL, 'Bellevue', '98005'),
    ('Nancy', 'Thomas', 'nancy.thomas@example.com', '425-555-0108', '369 Willow Ln', 'Apt 2C', 'Redmond', '98053'),
    ('Samantha', 'Jackson', 'samantha.jackson@example.com', '253-555-0109', '852 Spruce St', NULL, 'Tacoma', '98403'),
    ('Daniel', 'White', 'daniel.white@example.com', '509-555-0110', '681 Oakwood Ave', NULL, 'Spokane', '99202'),
    ('Sophia', 'Harris', 'sophia.harris@example.com', '206-555-0111', '408 Park Pl', 'Unit 1A', 'Seattle', '98103'),
    ('Christopher', 'Clark', 'christopher.clark@example.com', '360-555-0112', '246 Evergreen Dr', NULL, 'Bellevue', '98006'),
    ('Olivia', 'Lewis', 'olivia.lewis@example.com', '425-555-0113', '533 Pinecrest Ct', NULL, 'Redmond', '98054'),
    ('Joshua', 'Young', 'joshua.young@example.com', '253-555-0114', '129 Elmwood St', 'Apt 3B', 'Tacoma', '98404'),
    ('Mia', 'Walker', 'mia.walker@example.com', '509-555-0115', '926 Maplewood Rd', NULL, 'Spokane', '99203'),
    ('Matthew', 'Hall', 'matthew.hall@example.com', '206-555-0116', '734 Cedarwood Dr', NULL, 'Seattle', '98104'),
    ('Madison', 'Allen', 'madison.allen@example.com', '360-555-0117', '349 Pineview Ln', 'Apt 5C', 'Bellevue', '98007');
```
{% endcode %}

## Stored procedure for selecting a list of customers

The following script creates a store procedure that will return all the customers in the customer table.

{% code title="sp_GetAllCustomers.sql" fullWidth="true" %}
```sql
CREATE PROCEDURE sp_GetAllCustomers
AS
BEGIN
    SELECT
        id,
        first_name,
        last_name,
        email,
        phone_number,
        address_line1,
        address_line2,
        city,
        state,
        zip_code,
        country
    FROM
        customers;
END;
```
{% endcode %}

## Stored procedure for selecting one customer

The following script will create a store procedure to return a single customer record for the provided customer id.

{% code title="sp_GetCustomerById.sql" fullWidth="true" %}
```sql
CREATE PROCEDURE sp_GetCustomerById
    @CustomerId UNIQUEIDENTIFIER
AS
BEGIN
    SELECT
        id,
        first_name,
        last_name,
        email,
        phone_number,
        address_line1,
        address_line2,
        city,
        state,
        zip_code,
        country
    FROM
        customers
    WHERE
        id = @CustomerId;
END;
```
{% endcode %}

## Stored procedure for creating or updating a customer record

The following script creates a stored procedure that will add a new customer record if the customer id does not exist. It will update an existing customer if the id does exist.

{% code title="sp_InsertOrUpdateCustomer.sql" fullWidth="true" %}
```sql
CREATE PROCEDURE sp_InsertOrUpdateCustomer
    @CustomerId UNIQUEIDENTIFIER = NULL,
    @FirstName NVARCHAR(50),
    @LastName NVARCHAR(50),
    @Email NVARCHAR(100),
    @PhoneNumber NVARCHAR(15),
    @AddressLine1 NVARCHAR(100),
    @AddressLine2 NVARCHAR(100) = NULL,
    @City NVARCHAR(50),
    @ZipCode CHAR(5),
    @State CHAR(2) = 'WA',
    @Country NVARCHAR(50) = 'USA'
AS
BEGIN
    IF EXISTS (SELECT 1 FROM customers WHERE id = @CustomerId)
    BEGIN
        UPDATE customers
        SET
            first_name = @FirstName,
            last_name = @LastName,
            email = @Email,
            phone_number = @PhoneNumber,
            address_line1 = @AddressLine1,
            address_line2 = @AddressLine2,
            city = @City,
            state = @State,
            zip_code = @ZipCode,
            country = @Country
        WHERE
            id = @CustomerId;
    END
    ELSE
    BEGIN
        INSERT INTO customers (
            id,
            first_name,
            last_name,
            email,
            phone_number,
            address_line1,
            address_line2,
            city,
            state,
            zip_code,
            country
        )
        VALUES (
            @CustomerId,
            @FirstName,
            @LastName,
            @Email,
            @PhoneNumber,
            @AddressLine1,
            @AddressLine2,
            @City,
            @State,
            @ZipCode,
            @Country
        );
    END;
END;
```
{% endcode %}
