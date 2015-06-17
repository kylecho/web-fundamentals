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

```
(a) Customer removes out-of-stock item and continues.
(b) Customer cancels entire order.
...
```
* **Extensions**: Customer payment method rejected.

```
(a) ...
```

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

```
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
```

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

### IDENTIFYING OBJECTS

* Use Case Scenario: Customer confirms items in shopping cart. Customer provides payment and address to process sale. System validates payment and responds by confirming order, and provides order number that Customer can use to check on order status. system will send Customer a copy of order details by email.

### NOUN LIST

* Customer
* Item
* Shopping Cart
* Payment
* Address
* ~~Sale~~ : Same as Order. Remove.
* Order
* ~~Order Number~~ : Attribute of Order
* ~~Order Status~~ : Attribute of Order
* ~~Order Details~~ : Attribute of Order
* Email
* ~~System~~


### CONCEPTUAL OBJECT MODEL

```
+------------+   uses  +---------------+ contains+------------+
| Customer   |---------| Shopping Cart |---------| Payment    |
+------------+         +---------------+ 1     * +------------+
      |   places                                       |
      +-----------+                         +----------+
                  |                         |
                  |    +---------------+    |
+------------+    +----|     Order     +----+    +------------+           
| Item       |---------|               |         | Email      |
+------------+ paid by +---------------+         +------------+
                               |
                  +------------+
                  |
+------------+    |
| Address    |----+ 
+------------+

```

### IDENTIFYING RESPONSIBILITIES

* **Use Case Scenario**: Customer verifies items in shopping cart. Customer provides payment add address to process sale. System validates payment and responds by confirming order, and provides order number that Customer can use to check on order status. System will send Customer a copy of order details by email.

```
Verify items                         Confirm order

Provide payment and address          Provide order number

Process sale                         Check order status

Validate payment                     Send order details email

```

### ASSIGNING RESPONSIBILITIES

```

+------------+         +---------------+         +------------+  Verify items (a.)
| Customer   |---------| Shopping Cart |---------| Payment    |
+------------+         +---------------+         +------------+  Provide payment and address (b. c.)
      |                 a.Display totals                |
      +-----------+                         +-----------+        Process sale (d.)
                  |                         |
                  |    +---------------+    |                    Validate payment (e.)
+------------+    +----|     Order     |----+    +------------+
| Item       |---------|               |         | Email      |  Confirm order (f.)
+------------+         +---------------+         +------------+
b.Set payment details    d.Process order         j.Send email    Provide order number (g.)
e.Validate payment+------------+
                  |      f.Confirm order                         Check order status (h.)
+------------+    |      g.Get order number
| Address    |----+      h.Get status                            Send order details email (i. j.)
+------------+           i.Create order confirmation email
c.Set address details

```

### WORKING WITH "SYSTEM"

* **Use Case Scenario**: Customer verifies items in shopping cart. Customer provides payment add address to process sale. **System validates payment** and responds by confirming order, and provides order number that Customer can use to check on order status. **System will send Customer a copy of order details by email.**

System means "some part of our system". It is our job to find what part of our system should be responsible for that behaviour.

### AVOID GLOBAL MASTER OBJECTS

```

+------------+         +---------------+         +------------+
| Customer   |---------| Shopping Cart |---------| Item       |
+------------+         +---------------+         +------------+
      |                                                |
      +-----------+                         +----------+       
                  |                         |
                  |    +---------------+    |                  
+------------+    +----|    System     |----+    +------------+
| Item       |---------|               |---------| Order      |
+------------+         +---------------+         +------------+
                               |         
                  +------------+
                  |      Generate email         
+------------+    |      Create cart
| Email      |----+      Get order number           
+------------+           Validate payment
                         Add item to shopping cart
                         (etc)

```

### RESPONSIBILITIES SHOULD BE WELL DISTRIBUTED

```

+------------+         +---------------+         +------------+
| Customer   |---------| Shopping Cart |---------| Payment    |
+------------+         +---------------+         +------------+
      |                  Display totals                 |
      +-----------+                         +-----------+ 
                  |                         |
                  |    +---------------+    |                    
+------------+    +----|     Order     |----+    +------------+
| Item       |---------|               |         | Email      |  
+------------+         +---------------+         +------------+
Set payment details      Process order             Send email   
Validate payment  +------------+
                  |      Confirm order                         
+------------+    |      Get order number
| Address    |----+      Get status                            
+------------+           Create order confirmation email
Set address details

```

## OOP Using CRC Cards

### CRC CARDS

Each CRC Card represents one class:

```
+-------------------------------------------+
| Class name                                |
| ----------                                |
|                           |               |
| Responsibilities          | Collaborators |
|                           |               |
| ...                       | ...           |
|                           |               |
|                           |               |
|                           |               |
|                           |               |
|                           |               |
+-------------------------------------------+
```

One advantage of using CRC Cards is that you can freely move the card around to think about their relationships.

```
+-------------------------------------------+
| Payment                                   |
| ----------                                |
|                           |               |
| Store payment details     | Order         |
| Validate payment          |               |
|                           |               |
|                           |               |
|                           |               |
|                           |               |
|                           |               |
|                           |               |
+-------------------------------------------+
```

### CLASS DIAGRAM

```
+----------------------------------+
|              Product             |
+----------------------------------+
| - name: String = "New Product"   |  "-" represents that it is invisible
| - isActive: Boolean              |  "+" represents that it is visible
| - launchDate: Date               |  ":" represents the type of data
| - itemNumber: Integer            |
+----------------------------------+
| + getName(): String              |  ":" represents types that it returns
| + setActive(Boolean)             |
| + getProductDetails(): String    |
| + displayProduct()               |
| - formatProductDetails(): String |
+----------------------------------+
```

### AVOID BUILDING PLAIN DATA STRUCTURES

Do not start building classes first. Revisit UML and Use Cases and User Stories if you find your classes lack responsibilities.

```
+-----------------------+         +-----------------------+
|        Customer       |         |         Order         |
+-----------------------+         +-----------------------+
| customerID            |         | orderNumber           |
| customerName          |         | orderDate             |
| email                 |         | orderAmount           |
| address               |         | orderStatus           |
| phone                 |         | orderType             |
| company               |         | ...                   |
| firstPurchaseDate     |         |                       |
| customerContact       |         |                       |
| ...                   |         |                       |
+-----------------------+         +-----------------------+
|                       |         |                       |
+-----------------------+         +-----------------------+
```

### CONVERTING CLASS DIAGRAMS TO CODE

```
+-----------------------------+
|          Spaceship          |
+-----------------------------+
| + name: String              |
| - shieldStrength: Integer   |
|                             |
| ...                         |
+-----------------------------+
| + fire(): String            |
| + reduceShields(Integer)    |
|                             |
| ...                         |
+-----------------------------+
```

### SIMPLE CLASS IN JAVA

```
public class Spaceship {
	
  // instance variables
  public String name;
  private int shieldStrength;

  // methods
  public String fire() {
      return "Boom!";
  }

  public void reduceShields(int amount) {
      shieldStrength -= amount;
  }

}
```

### SIMPLE CLASS IN C'#'

```
public class Spaceship {
	
  // instance variables
  public String name;
  private int shieldStrength;

  // methods
  public String fire() {
      return "Boom!";
  }

  public void reduceShields(int amount) {
      shieldStrength -= amount;
  }

}
```

### SIMPLE CLASS IN VB.NET

```
Publiuc Class Spaceship

  ` instance variables
  Public Name As String
  Private ShieldStrength As Date

  ` methods
  Public Function Fire() As String
      Return "Boom!"
  End Function

  Public Function ReduceShields(Amount as Integer)
      ShieldStrength -= Amount
  End Function

End Class
```

### SIMPLE CLASS IN RUBY

```
class Spaceship

  # instance variables
  @name
  @shield_strength

  # methods
  def fire
      return "Boom!"
  end

  def reduce_shields(amount)
      shield_strength -= amount
  end

end
```

### SIMPLE CLASS IN OBJECTIVE-C

```
@interface Spaceship : NSObject {    @implementation Spaceship
    @public
    NSString *name;                  -(NSString *) fire {
    @private                             return @"Boom!";
    int shieldStrength;              }
}
                                     -(void) reduceShields: (int)amount {
// method declarations                   shieldStrength -= amount;
-(NSString *) fire;                  }
-(void) reduceShields:(int)amount;   @end

@end

           interface                          implementation

```

## Exploring Object Lifetime

### INSTANTIATION

```
          Java    Customer fred = new Customer();

            C#    Customer fred = new Customer();

        VB.NET    Dim fred As New Customer

          Ruby    fred = Customer.new

           C++    Customer *fred = new Customer();

   Objective-C    Customer *fred = [[Customer alloc] init];

```

### CONSTRUCTOR

```
+-----------------------------+
|          Spaceship          |   Spaceship excelsior = new Spaceship();
+-----------------------------+
|   name: String              |
|   shieldStrength: Integer   |            object: excelsior
|                             |          +-------------------+
|                             |          | name: null        |
+-----------------------------+          | shieldStrength: 0 |
|   fire(): String            |          +-------------------+
|   reduceShields(Integer)    |
|                             |
|                             |
+-----------------------------+
```

### CONSTRUCTOR EXAMPLE

```
public class Spaceship {
	                                Spaceship excelsior = new Spaceship();
	// instance variables
	public String name;                       object: excelsior
	private int shieldStrength;            +---------------------+
                                         | name: Unnamed Ship  |
	// constructor method                  | shieldStrength: 100 |
	public Spaceship() {                   +---------------------+
		  name = "Unnamed ship";
		  shieldStrength = 100;
	}




	// other methods omitted

}
```

### CONSTRUCTORS IN UML

```
+-----------------------------+
|          Spaceship          |
+-----------------------------+
|   name: String              |
|   shieldStrength: Integer   |
|                             |
|                             |
+-----------------------------+
|   Spaceship()               |
|                             |
|   fire(): String            |
|   reduceShields(Integer)    |
+-----------------------------+
```

### CONSTRUCTOR EXAMPLE 2 (OVERLOADING, WITH PARAM)

```
public class Spaceship {
	                                Spaceship excelsior = new Spaceship("Excelsior 2");
	// instance variables
	public String name;                       object: excelsior
	private int shieldStrength;            +---------------------+
                                         | name: Excelsior 2   |
	// constructor method                  | shieldStrength: 200 |
	public Spaceship() {                   +---------------------+
		  name = "Unnamed ship";
		  shieldStrength = 100;
	}
  // overloaded constructor
  public Spaceship(String n) {
      name = n;
      shieldStrength = 200;
  }
	// other methods omitted

}
```

### MULTIPLE CONSTRUCTORS IN UNL

```
+-----------------------------+
|          Spaceship          |
+-----------------------------+
|   name: String              |
|   shieldStrength: Integer   |
|                             |
|                             |
+-----------------------------+
|   Spaceship()               |
|   Spaceship(String)         |
|   fire(): String            |
|   reduceShields(Integer)    |
+-----------------------------+
```

### DESTRUCTORS / FINALIZERS

* Called when an object is being deleted / deallocated / released
* Use for releasing resources

## Using Static or Shared Members

```
+-----------------------------+    +-------------------------------------------------------+
|       SavingsAccount        |    |                         0.85%                         |
+-----------------------------+    |                                                       |
|   accountNumber             |    |  +-------------+   +-------------+   +-------------+  |
|   balance                   |    |  |             |   |             |   |             |  |
|   interestRate // static    |    |  | A7652       |   | B2311       |   | S2314       |  |
|                             |    |  | $500        |   | $50000      |   | $7500       |  |
+-----------------------------+    |  |             |   |             |   |             |  |
|   deposit()                 |    |  |             |   |             |   |             |  |
|   withdraw()                |    |  |             |   |             |   |             |  |
|                             |    |  | deposit()   |   | deposit()   |   | deposit()   |  |
|                             |    |  | withdraw()  |   | withdraw()  |   | withdraw()  |  |
+-----------------------------+    |  +-------------+   +-------------+   +-------------+  |
                                   |      joeAcct          aliceAcct          samAcct      |
                                   |                                                       |
                                   +-------------------------------------------------------+

```
Here `interestRate` variable is a class level variable. 


### CREATING STATIC VARIABLES

```
public class SavingsAccount {
	
	// instance variables                       ' VB.NET - shared variables
	public String accountNumber;                Public Shared interestRate As Float
	private Money balance;
	// static variables                         # Ruby - class level variables
	public static float interestRate;           @@interestRate






	// other code omitted

}

```

### USE THE NAME OF THE CLASS TO ACCESS

* `SavingsAccount.interestRate` // 0.85

* `joeAcct.accountNumber` // A7652

* `aliceAcct.accountNumber` // B2311

* `samAcct.accountNumber` // S2314

### CREATING STATIC METHODS

```
public class SavingsAccount {
	
	// instance variables omitted

	// public (accessible) static variable
	public static float interestRate;

	// public static methods
	public static setInterestRate(float r) {
      // add code to log any change
      interestRate = r;
	}
	public static getInterestRate() {
      return interestRate;
	}

	// other code omitted
}

```

Change to private

```
public class SavingsAccount {                     SavingsAccount.setInterestRate(0.9);
	
	// instance variables omitted

	// changed to private
	private static float interestRate;

	// public static methods
	public static setInterestRate(float r) {
      // add code to log any change
      interestRate = r;
	}
	public static getInterestRate() {
      return interestRate;
	}

	// other code omitted
}

```

### SHOWING STATIC MEMBERS IN UML

Class level, static, or shared members are represented using underline in UML.

```
+-----------------------------+
|       SavingsAccount        |
+-----------------------------+
|   accountNumber             |
|   balance                   |
|   interestRate              |
|   ------------              |
|                             |
+-----------------------------+
|   deposit()                 |
|   withdraw()                |
|   getInterestRate()         |
|   -----------------         |
|   setInterestRate()         |
|   -----------------         |
|                             |
+-----------------------------+  
```

## Identifying Inheritance Situations

Even if you don't know inheritance, you have used it all the time.

### INHERITANCE DESCRIBES AN "IS A" RELATIONSHIP

* A car **is a** vehicle.
* A bus **is a** vehicle.
* ~~A car **is a** bus.~~

* An employee **is a** person.
* A customer **is a** person.
* ~~A customer **is a** shopping cart.~~

* A checking account **is a kind of** bank account.
* A savings account **is a type of** bank account.

* A Bentley Continental GT **is a** car **is a** vehicle.

* A Pomeranian **is a** dog **is a** mammal **is an** animal.

### IDENTIFYING INHERITANCE

Say we have entities of:

* Customer
* Bank
* Manager
* Checking Account
* Bank Account
* Savings Account
* Teller

* Bank Account **is a** bank - No it is not.
* Checking Account **is a** Bank Account.
* Savings Account **is a** Bank Account.

"Is A" should identify inheritance.

In UML, inheritance relationship is represented by open arrow that looks like:

```
Subclass or Child class           Super class or Parent class
+------------------+              +--------------+
| Checking Account | ----------|> | Bank Account |
+------------------+              +--------------+

```

### EXAMPLE

Say we have Album, Book, and Movie. They all share title, price, purchase(), and download(). Since they share many attributes and behaviours, we can create a Super class named "Product" with shared attributes and behaviours.

* Album can inherit everything but artist attribute.
* Book can inherit everything but author attribute.
* Movie can inherit everything but director attribute.

### FRAMEWORK INHERITANCE EXAMPLE FROM JAVA

```
+-------------+
| Object      |   Super Class / Parent Class
+-------------+
       ^
       |
+-------------+
| Component   |
+-------------+
       ^
       |
+-------------+
| Container   |
+-------------+
       ^
       |
+-------------+
| Window      |
+-------------+
       ^
       |
+-------------+
| Dialog      |
+-------------+
       ^
       |
+-------------+
| FileDialog  |   Sub Class / Child Class
+-------------+
```
