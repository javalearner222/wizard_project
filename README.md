# Overview

This project is a Java-based telecommunication application designed to manage customer information, their selected plans, billing details, and service subscriptions. The application ensures accurate billing and service management based on the customer's chosen plan and services.

## Table of Contents
- [Features](#features)
- [Database Structure](#database-structure)
- [Java Classes and Methods](#java-classes-and-methods)
  - [Customer Class](#customer-class)
  - [Plan Class](#plan-class)
  - [BillingDetails Class](#billingdetails-class)
  - [ServiceSubscription Class](#servicesubscription-class)
  - [DataGenerator Class](#datagenerator-class)
- [Usage](#usage)
- [Workflow](#workflow)
- [License](#license)

## Features
- **Customer Management**: Store and manage customer details, including their assigned plans.
- **Plan Management**: Define various plans with specific service offerings.
- **Billing Management**: Track and generate bills based on the customer's plan and service usage.
- **Service Subscription Management**: Allow customers to subscribe to additional services and track their usage.
- **Data Generation**: Populate the database with random data for testing purposes.

## Database Structure
The application uses the following database tables:

### Customers Table
- `customer_id` (Primary Key)
- `first_name`
- `last_name`
- `phone_number` (Unique)
- `email`
- `address`
- `plan_id` (Foreign Key referencing Plans table)
- `current_service_count` (Tracks how many additional services the customer has subscribed to)

### Plans Table
- `plan_id` (Primary Key)
- `plan_name`
- `monthly_cost`
- `data_limit`
- `call_minutes`
- `included_services` (List of services included in the plan)

### BillingDetails Table
- `bill_id` (Primary Key)
- `customer_id` (Foreign Key referencing Customers table)
- `billing_date`
- `amount_due`
- `payment_status` (e.g., Paid, Pending, Overdue)

### ServiceSubscription Table
- `customer_id` (Foreign Key referencing Customers table)
- `service_name`
- `service_cost`
- `subscription_date`
- `service_status` (e.g., Active, Inactive)

## Java Classes and Methods

### Customer Class
The `Customer` class manages customer details and their interactions with the plan and service subscriptions.

**Attributes:**
- `customerId`
- `firstName`
- `lastName`
- `phoneNumber`
- `email`
- `address`
- `plan` (Object of type `Plan`)
- `serviceSubscriptions` (List of `ServiceSubscription` objects)
- `currentServiceCount`

**Methods:**
- `subscribeService(ServiceSubscription service)`: Subscribes to a new service if allowed by the plan.
- `generateBill()`: Generates a bill based on the customer's plan and subscribed services.
- `makePayment(double amount)`: Updates the payment status of the latest bill.

### Plan Class
The `Plan` class defines the details of a telecommunication plan.

**Attributes:**
- `planId`
- `planName`
- `monthlyCost`
- `dataLimit`
- `callMinutes`
- `includedServices` (List of services included in the plan)

**Methods:**
- `updatePlanDetails(String planName, double monthlyCost, int dataLimit, int callMinutes)`: Updates the details of the plan.
- `addService(String serviceName)`: Adds a new service to the list of included services.

### BillingDetails Class
The `BillingDetails` class manages the billing details of a customer.

**Attributes:**
- `billId`
- `customerId`
- `billingDate`
- `amountDue`
- `paymentStatus`

**Methods:**
- `calculateBillAmount()`: Calculates the total amount due based on the plan and subscribed services.
- `updatePaymentStatus(String status)`: Updates the payment status of the bill.

### ServiceSubscription Class
The `ServiceSubscription` class represents a service that a customer has subscribed to.

**Attributes:**
- `serviceName`
- `serviceCost`
- `subscriptionDate`
- `serviceStatus`

**Methods:**
- `updateServiceStatus(String newStatus)`: Updates the status of the service subscription.
- `calculateServiceCost()`: Calculates the cost of the subscribed service.

### DataGenerator Class
The `DataGenerator` class provides utility methods to generate random data for testing.

**Methods:**
- `generateRandomCustomer()`: Generates a random customer.
- `generateRandomPlan()`: Generates a random plan.
- `generateRandomServiceSubscription()`: Generates a random service subscription.
- `generateRandomBillingDetails(Customer customer)`: Generates random billing details for a customer.

## Usage
1. **Setup**: Configure your database and ensure the tables are set up according to the provided structure
2. **Data Population**: Use the `DataGenerator` class to populate the database with random customers, plans, service subscriptions, and billing details.
3. **Operations**: Use the `Customer` class methods to subscribe to services and generate bills according to the rules of the selected plan.
4. **Billing**: The application will automatically calculate and generate billing details based on plan usage and service subscriptions.

## Workflow
1. **Customer Creation**: Generate or manually create customers and assign them plans.
2. **Service Subscription**: Use the `subscribeService()` method in the `Customer` class to subscribe to services.
3. **Bill Generation**: Use the `generateBill()` method to create a bill based on the customer's plan and service subscriptions.
4. **Payment**: Use the `makePayment()` method to update the payment status of a bill.

## License
This project is licensed under the Apache License, Version 2.0.
