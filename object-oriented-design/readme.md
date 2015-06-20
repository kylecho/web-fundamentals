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

## INHERITANCE

A little difference in syntax for inheritance.

```
       Java  public class Album extends Product {  ...

         C#  public class Album : Product {  ...

     VB.NET  public Class Album Inherits Product  ...

       Ruby  class Album < Product   ...

        C++  class Album : public Product {  ...

Objective-C  @interface Album : Product {  ...

```

Overriding differ by languages. Some languages require keywords, others don't. Some languages require keywords both the Superclass and Subclass and so on.

### CALLING A METHOD IN THE SUPER / PARENT / BASE CLASS

```
       Java  super.doSomething();

         C#  base.doSomething();

     VB.NET  MyBase.doSomething()

       Ruby  super do_something

        C++  [super someMethod];

Objective-C  NamedBaseClass::doSomething();

```

## Using Abstract Classes

When you have a class that never gets instantiated, you call it **abstract class**. Some languages offer a keyword for abstract classes.

The language won't allow it to be instantiated, and you must inherit from it before instantiating an object.

* C'#' or Java - `abstract class BankAccount { ...`

* VB.NET - `Public MustInherit Class BankAccount ...`

Opposite word to **abstract class** is **concrete classes**. It can be instantiated.

## Using Interfaces

Interface in OOP means, something that is actually created very similar to a class but with no actual functionality, no actual code, no behaviour. It is really just a list of method signatures.

In Java, interface can be written as something like this:

```
interface Printable {
	
  // method signatures
  void print();
  void printToPDF(String filename);

}

```

### IMPLEMENTING INTERFACES

What's the point of this? The idea is that if we create a new class and then choose to use an interface then the term we use is implementing an interface, it is like signing a contract. What we do is create this class use the word implements to say we are supporting that we are promising to do something, we are promising to create methods with particular names. We have the freedom to do it anyway we want to but we are promising to do it. It's a contract that we are signing. And the point of contract is of course that you are never the only one to sign. With interfaces, the more classes implement the same interface the better. So I used the word implements here, I've signed the contract, then that means I have to provide those to methods in my class and some kind of implementation for them. Or I'll get a compile error. 

```
Class MyClass implements Printable {
	
    // method bodies
    public void print() {
        // provide implementation
    }

    public void printToPDF(String filename) {
        // provide implementation
    }

    // additional functionality...

}
```

### USING INTERFACES

```
// sometime later
while (genericObject in listOfObjects) {
	
	  if ( genericObject instanceOf Printable ) {
        // if it implements the interface, we can use it
    genericObject.print();
	  }

}

```

Interfaces in UML

```
+-----------------+
|  <<Interface>>  |
|    Printable    |
+-----------------+
| print()         |
| printToPDF()    |
+-----------------+
         ^
         .
         .   implementing: use an empty arrow and dotted line to represent it
         .
         .
+-----------------+
|     MyClass     |
+-----------------+
|                 |
|                 |
+-----------------+

```

## Using Aggregation and Composition

### AGGREGATION DESCRIBES A "HAS A" RELATIONSHIP

* A customer **has a** address.
* A car **has a** engine.
* A bank **has many** bank accounts.
* A university **has many** students.

```

+-----------------+             +-----------------+
|    Classroom    |<>-----------|     Student     |
+-----------------+ 1         * +-----------------+

                    aggregation

```

Aggregation is represented by an unfilled diamond at the end of the line.

```
                    filled diamond
+-----------------+ |           +-----------------+
|    Document     |<>-----------|       Page      |
+-----------------+             +-----------------+

                    composition
                 implies ownership

```

Composition shows the ownership. If I delete the document, the page is deleted too. On the other hand, even if Classroom object is deleted, Student object won't be deleted.

* Composition implies ownership
* Aggregation does not - Worth showing in the diagram

## Creating Sequence Diagrams

It can be used as a thinking tool to communicate the process with a business user.

```
+-----------------+             +--------------------+             +-----------------+
|    a Customer   |-------------|a Cart:Shopping Cart|-------------|      :Order     |
+-----------------+             +--------------------+             +-----------------+
         .                                .                                  .
         .          checkout              .                                  .
         .------------------------------->.           createNewOrder         .
         .                                .--------------------------------->.
         .              +----------------------------------------------------------------------+
         .              |loop |           .       addItem(item, quantity)    .                 |
         .              |_____/           .-------------------------------->+-+                |
         .              |                 .                                 | |                |
         .              |                 .             itemtotal           | |                |
         .              |                 .<. . . . . . . . . . . . . . . . +-+                |
         .              +----------------------------------------------------------------------+
         .                                .                                  .
         .                                .         calculateDiscount        .
         .                                .--------------------------------->.
         .                                .                                  .
         .                                .            finalizeSale          .
         .                                .-------------------------------->+-+
         .                                .                                 | |
         .                                .                total            | |
         .< . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . +-+                +---------+
         .                                .                                  .                 | Payment |
         .           submitPayment        .                                  .                 +---------+
         .------------------------------------------------------------------>. createPayment        .
         .                                .                                  .--------------------->.
         .                                .                                  .                      .
         .                                .                                  .      results         .
         .                                .    results                       .< . . . . . . . . . . X
         .< . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . ..
         .                                .                                  .
         .                                .                                  .
         .                                .                                  .

```

## Working with Advanced UML Diagrams

### UML DIAGRAMS

First four diagrams are the most common diagrams you will see and use. It's always about selecting the right diagram for the right need. It should be driven from a business problem.

* Class Diagram
* Use Case Diagram
* Object Diagram
* Secuence Diagram
* State Machine Diagram
* Activity Diagram - similar to procedural programming language. shows the decisions.
* Deployment Diagram
* Package Diagram
* Component Diagram
* Profile Diagram
* Communication Diagram
* Timing Diagram
* Composite Structure Diagram
* Interaction Overview Diagram

## Using UML tools

### UML TOOLS

* Diagramming Tools - Visio, OmniGraffle
* Web-based Diagramming - gliffy.com, creately.com, lucidchart.com
* Programming Tools: IDE based - Visual Studio, Eclipse with UMLTools
* Commercial Products - Altova UModel, Sparx Enterprise Architect, Visual Paradigm
* Open-Source - ArgoUML, Dia

[List of Unified Modeling Language tools](http://goo.gl/YAuOY)

## Introduction to Design Patterns

Design patterns are well tested solutions for common problems and issues we run into in software development. These are not business solutions. Design patterns don't deal with bank accounts and customer classes. They work at a different level than that. Think of them as best practices suggestions for how you might arrange your own classes and objects to accomplish a result.

They don't deal with questions like, "I need to create an email app for iPhone or I need to make a payroll system". Instead, they deal with more general issues. Say you are working through your class design and you realize that if one of you objects changes, it needs to let several other objects. You wonder if there's a good way to do that.

There are multiple ways you could deal with that but there is a well-tested proven approach that's been given the name above the observer design pattern, or another example.

Let's say you realize an object will be changed by a lot of other objects, but you needed to be able to undo the last change. Again, this could be done many different ways, but there is a memento design pattern that describes a simple proven approach.

Best practice is a for solving common software design problems that occur again and again across all kinds of applications from business apps to games.

### DESIGN PATTERNS

Design patterns became best known from the Design Patterns book by Erich Gramma, Richard Helm, Ralph Johnson, and John Vlissides. Often referred to as the "Gang of Four" or ("GoF") and you will see this referred to as the Gang of Four book published in the mid 90's. This book detailed 23 design patterns which were split into three groups.

#### 1st Group: Creational Patterns

These are approaches that deal with the creation of objects. Instead of you instantiating all objects very specifically and very explicitly, they give you more flexibility in how the objects were actually created.

* Abstract Factory
* Builder
* Factory Method
* Prototype
* Singleton


#### 2nd Group: Structural Patterns

Structural patterns deals more with how classes are actually designed, how things like inheritance and composition and aggregation can be used to provide extra functionality. 

* Adapter
* Bridge
* Composite
* Decorator
* Facade
* Flyweight
* Proxy

#### 3rd Group: Behavioral Patterns

Most of these design patterns are specifically concerned with communication between objects as the program is running.

* Chain of responsibility
* Command
* Interpreter
* Iterator
* Mediator
* Memento
* Observer
* State
* Strategy
* Template method
* Visitor

## The Singleton Pattern

Here is the problem it is designed to solve. We create a class and we know the class can be instantiated once or twice or thousand times, but what if you only want one object of that class. What if you want to restrict this. In fact you need it to there to be only one object of this class. What if this one object needs to represent the currently running application orr perhaps the current display, and having more than one instantiated object just doesn't make sense and could even lead to problems with the application.

There is actually quite a lot of situations whether should only be one object of a particular class. This may first sound like little an abstract class but remember an abstract class isn't allowed to be instantiated at all. So if we have only one, you might first think, why don't we just not create more than one. You could do that but it's not really enforcing anything you can't guarantee that behavior.

So instead, we can use the singleton design pattern.

### SINGLETON

* We want to ensure a class only has one instance
* We want one way of accessing it

### IMPLEMENTING A SINGLETON IN JAVA

```
public class MySingleton {
    // placeholder for current singleton object
    private static MySingleton __me = null;
    // private constructor - now no other object can instantiate
    private MySingleton() { }
    // this is how you ask for the singleton
        // do I exist?
        if ( __me == null ) {
            // if not, instantiate and store
            __me = new MySingleton();
        }
        return MySingleton;
    }

    // additional functionality
    public someMethod() { //... }
}
```

### USING A SINGLETON IN JAVA

```
// ask for the singleton
MySingleton single = Mysingleton.getInstance();

// use it
single.someMethod();


// or even just call directly
MySingleton.getInstance().someMethod();
```

## MEMENTO DESIGN PATTERN

* Handles "undo" in an object
* Does not violate encapsulation

```
+-------------+               +-------------+
|  Caretaker  |               |  Originator |
+-------------+               +-------------+
|             |               |    +-------+|
|             |               |    |memento||
|             |               |    +-------+|
+-------------+               +-------------+
```

## Object Oriented Design Principles

Good object orientation practices do not automatically get imposed. It is up to us. We might not have enforced rules but we do have guidelines, and we have principles that we can use.

Design principles are general principles, things to stay conscious of, and occasionally check back with as you create and iterate through your class design and building your software.

First, we will discover some general development principles. Then we will cover two sets of well-known object-oriented design principles. Grouped together under the acronyms SOLID and GRASP.

They use ideas as a starting point and give you some more guidelines so that you can ask "Did I design this class well?", and have a good answer to that question.

## Exploring General Development Principles

### GENERAL SOFTWARE DEVELOPMENT PRINCIPLES

* DRY: Don't Repeat Yourself
* YAGNI: You Ain't Gonna Need It

### EXAMPLE CODE SMELLS

* Long methods
* Very short (or long) identifiers
* Pointless comments
* God object
* Feature envy

## Introduction to SOLID Principles

#### **S**: Single Responsibility Principle

An object should have one reason to exist, one reason to change - one primary responsibility

#### **O**: Open / Closed Principle

Open for extension, but closed to modification. In other words, we do not change the existing code. When requirements change, we add new object that inherits, and add methods.

#### **L**: Liskov Substitution Principle

Derived classes must be substitutable for their base classes.

#### **I**: Interface Segregation Principle

Multiple specific interfaces are better than one general purpose interface. We are not talking about User Interface here. Because classes can choose from multiple smaller interfaces, no class should be foreced to support huge list of methods it doesn't need.

#### **D**: Dependency Inversion Principle

Depend on abstractions, not on concretions.

Instead of this:

```
             +-----------------+
             |      Store      |
             +-----------------+
                     / \
                   /     \
                 /         \
               /             \
             /                 \
           /                     \
         /                         \
+-----------------+        +-----------------+
| AudioFileReader |        | AudioFileWriter |
+-----------------+        +-----------------+
```

Do this:

```
             +-----------------+
             |      Store      |
             +-----------------+
                     / \
                   /     \
                 /         \
               /             \
             /                 \
           /                     \
         /                         \
+-----------------+        +-----------------+
|     Reader      |        |     Writer      |       layer of abstraction
+-----------------+        +-----------------+
        |                           |
        |                           |
        |                           |
+-----------------+        +-----------------+
| AudioFileReader |        | AudioFileWriter |
+-----------------+        +-----------------+
```

Benefits of having the layer of abstraction: It allows flexibility and substitution. However, if you have too many layers, it's likely you will violate YAGNI(You Ain't Gonna Need It) rule.

```
             +-----------------+
             |      Store      |
             +-----------------+
                     / \
                   /     \
                 /         \
               /             \
             /                 \
           /                     \
         /                         \
+-----------------+        +-----------------+
|     Reader      |        |     Writer      |       layer of abstraction
+-----------------+        +-----------------+
        |                           |      \
        |                           |         \
        |                           |            \
+-----------------+        +-----------------+    +-----------------+
| AudioFileReader |        | AudioFileWriter |    | MovieFileWriter |
+-----------------+        +-----------------+    +-----------------+

```

### SOLID

These aren't rules, these aren't dogma, SOLID can be viewed as a checklist. No need to memorize it, but revisit it.

* **S**: Single Responsibility Principle
* **O**: Open / Closed Principle
* **L**: Liskov Substitution Principle
* **I**: Interface SEgregation Principle
* **D**: Dependency Inversion Principle

## Introduction to GRASP Principle

GRASP tends to take a responsibility focus as in, who creates this object, who's in charge of how these objects talk to each other, who takes care of passing on messages received from a user interface.

SOLID and GRASP don't conflict with each other. They are not competing sets. You might choose to use one or both or neither.

### GRASP PRINCIPLES OF OBJECT-ORIENTED DESIGN

You may find GRASP a useful learning tool to keep in mind while drawing up UML diagrams to provide some techniques for figuring out the responsibilities of your objects.

#### General Responsibility Assignment Software Patterns

* Creator - Who is responsible for creating an object? Does one object contain another? The idea of composition.
* Controller - Don't connect UI elements directly to business objects. (problem: high coupling, low cohesion) MVC is an example using this.
* Pure Fabrication - When the behavior does not belong anywhere else, create a new class.
* Information Expert - Assign the responsibility to the class that has the information needed to fulfill it.
* High Cohesion - Cohesion: the level of that a class contains focused, related behaviors. God Object is high cohesion.
* Indirection - To reduce coupling, introduce an intermediate object.
* Low Coupling - Coupling: the level of dependencies between objects. Means to reduce the amount of required connections between objects.
* Polymorphism - Automatically correct behavior based on type. As opposed to: conditional logic that checks for particular types.
* Protected Variations - Protect the system for changes and variations. Identify the most likely points of change. Use multiple techniques: encapsulation, LSP, OCP

### OBJECT-ORIENTED LANGUAGES

```
+-------------+-------------+---------+---------+---------+----------+------------+
| Language    | Inheritance | Typing  | Call to | Private | Abstract | Interfaces |
|             |             |         | super   | Methods | Classes  |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| Java        | Single      | static  | super   | Yes     | Yes      | Yes        |
|             |             |         |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| C#          | Single      | static  | base    | Yes     | Yes      | Yes        |
|             |             |         |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| VB.NET      | Single      | static  | MyBase  | Yes     | Yes      | Yes        |
|             |             |         |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| Objective-C | Single      | static/ | super   | No      | No       | Protocols  |
|             |             | dynamic |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| C++         | Multiple    | static  | name of | Yes     | Yes      | Abstract   |
|             |             |         | class:: |         |          | Class      |
+-------------+-------------+---------+---------+---------+----------+------------+
| Ruby        | Mix-ins     | dynamic | super   | Yes     | n/a      | n/a        |
|             |             |         |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+
| JavaScript  | Prototype   | dynamic | n/a     | Yes     | n/a      | n/a        |
|             |             |         |         |         |          |            |
+-------------+-------------+---------+---------+---------+----------+------------+

```

## Additional Resources

* For the initial stage of determining requirements, if you do consulting work and need to be able to step into the world of client or company this book will be useful.

"SOFTWARE REQUIREMENTS" by Karl E. Wiegers, Joy Beatty

* For the world of Use Cases:

"Writing Effective Use Cases" by Alistair Cockburn

* For the more concise User Story format:

"USER STORIES APPLIED" by Mike Cohn

* For UML:

"UML DISTILLED" by Martin Fowler (also the author of "Refactoring")

* For Design Pattern:

"HEAD FIRST DESIGN PATTERNS"
