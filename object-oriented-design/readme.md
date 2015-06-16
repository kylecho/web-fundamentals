#Foundation of Programming: Object-Oriended Design [Link](https://www.youtube.com/watch?v=M1grhaE_xs4&list=PLnxBrInqFEs41ueBVMW0WnumNhNO7xdxg)

#Understanding the Object Oriented Analysis and Design Process

1. Gather Requirements
2. Describe the app
3. Identify the main objects
4. Describe the Interactions
5. Create a Class Diagram

## GATHERING REQUIREMENTS

### Functional Requirements: what does it do?

* Features / Capabilities

### Non-Functional Requirements: what else?

* Help
* Legal
* Performance
* Support
* Security

### FUNCTIONAL REQUIREMENTS EXAMPLES

* System must display the heart rate, temperature and blood pressure of a patient connected to the patient monitor.
* Application must allow user to search by customer's last name, telephone number or order number.
* Program must allow receipts to be generated via email.
* Application must allow user to create 140-character message.
* Application must continue to function without network connection.
* System must automatically produce monthly Comparative Analysis (using current month and year-to-date as compared to same month last year and year-to-date last year) report by: Product (units sold and dollars), Product Category, Customer, Department, Region. Report must be in PDF format and automatically emailed to everyone in administrators group on first day of month.

### NON-FUNCTIONAL REQUIREMENTS EXAMPLES

* System must respond to searches within 2 seconds.
* Help desk available by telephone. Mon-Fri 8am-6pm.
* Comply with all relevant HIPAA regulations.
* Be available 99.99% of time during business hours.

### FURPS / FURPS+ (Checklist)

* Functional requirements
* Usability requirements
* Reliability requirements
* Performance requirements
* Supportability requirements

* + Design requirements, Implementation requirements, Interface requirements, Physical requirements

## INTRODUCTION TO UML (UNIFIED MODELING LANGUAGE)

It's not a programming language, it's a graphical notation.

```
+---------------+
| Bank Account  |
+---------------+
| accountNumber |
| balance       |
| dateOpened    |
| accountType   |
+---------------+
| open()        |
| close()       |
| deposit()     |
| withdraw()    |
+---------------+
```

## USE CASES

* Title : what is the goal?
* Actor : who desires it?
* Scenario : how is it accomplished?

### USE CASE: TITLE

### Short phrase, active verb

* **Register** new member
* **Transfer** funds
* **Purchase** items
* **Create** new page
* **Collect** late payments
* **Process** accounts

### USE CASE: ACTOR

* User
* Customer
* Member
* Administrator
* ACMESystem

### USE CASE: SCENARIO AS PARAGRAPH

* **Title**: Purchase items
* **Actor**: Customer

* **Scenario**: Customer reviews items in shopping cart. Customer provides payment and shipping information. System validates payment information and responds with confirmation of order and provides order number that Customer can use to check on order status. System will send Customer a confirmation of order details and tracking number in an email.

### USE CASE: SCENARIO AS STEPS

* **Title**: Purchase items
* **Actor**: Customer

* **Scenario**:

1. Customer chooses to enter the checkout process
2. Customer is shown a confirmation page for their order, allowing them to change quantities, remove items, or cancel
3. Customer enters his/her shipping address
4. System validates the customer address
5. Customer selects a payment method
6. System validates the payment details
7. System creates an order number that can be used for tracking
8. System displays a confirmation screen to the Customer
9. Email is sent to the Customer with order details

### USE CASE: SCENARIO ADDITIONAL DETAILS

* **Title**: Purchase items
* **Actor**: Customer

* **Scenario**: ...

* **Extensions**: Describe steps for out-of-stock situations
* **Extensions**: Describe steps for order never finalized
* **Precondition**: Customer has added at least one item to shopping cart

### USE CASE: SCENARIO ADDITIONAL DETAILS (FULLY DRESSED LIST)

* **Title**: Purchase items
* **Actor**: Customer
* **Secondary actor**: ...
* **Scenario**: ...
* **Description**: ...
* **Scope**: ...
* **Level**: ...
* **Extensions**: Describe steps for out-of-stock situations
* **Extensions**: Describe steps for order never finalized
* **Precondition**: Customer has added at least one item to shopping cart
* **Postcondition**: ...
* **Stakeholders**: ...
* **Technology list**: ...
* ...

