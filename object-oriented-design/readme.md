#Foundation of Programming: Object-Oriended Design [Link](https://www.youtube.com/watch?v=M1grhaE_xs4&list=PLnxBrInqFEs41ueBVMW0WnumNhNO7xdxg)

##Understanding the Object Oriented Analysis and Design Process

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

## Identifying the Actors

### External Systems / Organizations

* External data sources, web services, other corporate apps, tax reporting, backup systems

### Roles / Security Groups

* Visitor, member, administrator, owner

### Job Titles / Departments

* Manager, Payroll Administrator, Production Staff, Executive Team, Accounting

### Example: Expense Approval System

#### Two Actors

* Requester - Primary actor
* Approver - Secondary actor

## Identifying the Scenarios

Emphasize the goal of one encounter:

```
These are user focused goals            Too broad
-----------------------------------------------------------------------------------------------------
Purchase items                          Log in to application
Create new document                     Write book
Balance accounts                        Merge organizations

* Logging in might be a part of it. It's not a use case in itself.

```

### MULTIPLE SCENARIOS

* **Title**: Purchase items
* **Actor**: Customer
* **Scenario**: Customer reviews items in shopping cart. Customer provides payment and shipping information. System validates payment information and responds with confirmation of order and provides order number that Customer can use to check on order status. System will send Customer a confirmation of order details and tracking number in an email.

* **Extensions**: One or more items out of stock.

(a) Customer removes out-of-stock item and continues.
(b) Customer cancels entire order.
...

* **Extensions**: Customer payment method rejected.

(a) ...

### ACTIVE VOICE. OMIT NEEDLESS WORDS.

* **Not this**: The system is provided with the payment information and shipping information by the Customer.

* **This**: Customer provides payment and shipping information.

* **Not This**: The system connects to the external payment processor over HTTPS and uses JSON to submit the provided payment information to be validated, then waits for a delegated callback response.

* **This**: System validates payment information.

### FOCUS ON INTENTION

We should focus on intention not interface. We don't have anything like buttons, layouts, or animation in the use case.

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

### USE CASE PROMPTS

* Who performs system administration tasks?
* Who manages users and security?
* What happens if the system fails?
* Is anyone looking at performance metrics or logs?

## Diagramming Use Cases

```

                       +--------------------------------+
                       |        Knowledge Base          |
                       |                                |
   O                   |        ----------------        |
  ---  +---------------------+( Search Articles  )      |
   |    \              |        ----------------        |
  / \    \             |                                |
Visitor   \            |        ----------------        |              +-------------------+
           +-----------------+( View Article     )+-----+-------------+|    << actor >>    |
                       |        ----------------        |            / | Analytics System  |
                       |                                |           /  +-------------------+
   O   +----------------+       ----------------        |          /
  ---                  | \   +( Manage Users     )      |         /
   |                   |  \ /   ----------------        |        /
  / \                  |   X                            |       /
Contributor            |  / \   ----------------        |      /
                       | /   +( Create Article   )      |     /
                       |/       ----------------        |    /
                       /                                |   /
                      /|        ----------------        |  /
   O   +-------------+--------( View Analytics   )--------+
  ---                  |        ----------------        |
   |                   +--------------------------------+
  / \
Administrator


```

## Employing User Stories

### USER STORY

* As a ... (type of user)
* I want ... (goal)
* So that ... (reason)

### Examples

* As a Bank Customer
* I want to change my PIN online
* so that I don't have to go into a branch

* As a User
* I want to search by keyword
* so that I can find and read relevant articles 

* As a User
* I want to sort entries by date
* so that I can find the most recent content

* As a Reader
* I want to change the font and color scheme
* so that I can read in different lighting

* As a User
* I want to be prompted to save
* so that I don't lost any work

### USER STORIES AND USE CASE

```
+-----------------------------------------------------------------+
|         USER STORIES           |           USE CASES            |
+--------------------------------+--------------------------------+
| short - one index card         | long - a document              |
| one goal, no details           | multiple goals and details     |
| informal                       | casual to (very) formal        |
| "placeholder for conversation" | "record of conversation"       |
+--------------------------------+--------------------------------+

```

## Creating a Conceptual Model














