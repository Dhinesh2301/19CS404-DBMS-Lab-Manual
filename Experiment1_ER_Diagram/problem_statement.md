# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="689" height="306" alt="image" src="https://github.com/user-attachments/assets/4bf4821e-8ab5-4084-afe5-5b15d3c47007" />


### Entities and Attributes

| Entity             | Attributes (PK, FK)                                                                      | Notes                                                                |
| ------------------ | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Member**         | MemberID **(PK)**, Name, MembershipType, StartDate                                       | Stores member details and registration info.                         |
| **Trainer**        | TrainerID **(PK)**, Name, Specialization, Phone                                          | Stores trainer details and expertise.                                |
| **Program**        | ProgramID **(PK)**, ProgramName, Duration                                                | Represents different fitness programs like Yoga, Zumba, etc.         |
| **Session**        | SessionID **(PK)**, SessionDate, AttendanceStatus, MemberID **(FK)**, TrainerID **(FK)** | Each session is attended by one member and conducted by one trainer. |
| **Payment**        | PaymentID **(PK)**, Amount, PaymentDate, PaymentType, MemberID **(FK)**                  | Records all payments made by members for memberships or sessions.    |
| **MemberProgram**  | MemberID **(FK)**, ProgramID **(FK)**                                                    | Resolves the M:N relationship between Members and Programs.          |
| **TrainerProgram** | TrainerID **(FK)**, ProgramID **(FK)**                                                   | Resolves the M:N relationship between Trainers and Programs.         |


### Relationships and Constraints

| Relationship          | Cardinality | Participation         | Notes                                                                         |
| --------------------- | ----------- | --------------------- | ----------------------------------------------------------------------------- |
| **Member – Program**  | M:N         | Total on both sides   | A member can join many programs; each program can have many members.          |
| **Trainer – Program** | M:N         | Total on both sides   | A trainer can conduct many programs; each program can have multiple trainers. |
| **Member – Session**  | 1:N         | Total on Member side  | A member can attend multiple sessions; each session belongs to one member.    |
| **Trainer – Session** | 1:N         | Total on Trainer side | A trainer can conduct many sessions; each session is handled by one trainer.  |
| **Member – Payment**  | 1:N         | Total on Member side  | A member can make many payments; each payment is linked to one member.        |


### Assumptions
-Each member has a unique MemberID and can participate in multiple programs.
-Each trainer has a unique TrainerID and can handle several programs and sessions.
-A session is always conducted by one trainer and attended by one member.
-Payments are made only by registered members and linked to either membership or session fees.
-Programs are predefined (e.g., Yoga, Zumba, Weight Training) with fixed durations.
-Attendance is recorded per session for tracking member participation.



# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="691" height="288" alt="image" src="https://github.com/user-attachments/assets/0c6c9e97-0f6a-4623-9e48-3b28daa67e8b" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| **Member** | MemberID **(PK)**, Name, Email, Phone | Each library member can borrow multiple books. |
| **Book** | BookID **(PK)**, Title, Author, Category | Stores information about each book and its genre (e.g., Love, Horror, Fantasy). |
| **Loan** | LoanID **(PK)**, LoanDate, ReturnDate, MemberID **(FK)**, BookID **(FK)** | Records book borrow and return details for each member. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| **Member – Loan** | 1:N | Total on Member side | A member can borrow many books; each loan belongs to one member. |
| **Book – Loan** | 1:N | Total on Book side | A book can be borrowed many times; each loan refers to one book. |
| **Book – Category** | 1:1 | Partial | Each book belongs to one category (e.g., Love, Horror, Fantasy). |

---

## Assumptions
- Each **member** has a unique `MemberID` and can borrow multiple books.  
- Each **book** has a unique `BookID` and can be borrowed multiple times by different members.  
- Each **loan** record connects one member with one borrowed book.  
- The **loan date** and **return date** are mandatory for tracking borrowing duration.  
- **Categories** (Love, Horror, Fantasy) are predefined for book classification.  
- A member must be registered before borrowing any book.  


# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*<img width="694" height="319" alt="image" src="https://github.com/user-attachments/assets/8efd0197-836b-4214-af13-bc89d2726a29" />

### Entities and Attributes
| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| **Customer** | CustomerID **(PK)**, Name, Email, Phone | Stores customer details for reservations and orders. |
| **Reservation** | ReservationID **(PK)**, Date, Time, CustomerID **(FK)**, TableID **(FK)** | Tracks customer table reservations with date and time. |
| **Table** | TableID **(PK)**, TableNumber, Capacity | Represents restaurant tables with their seating capacity. |
| **Bill** | BillID **(PK)**, Amount, ServiceCharge, TableID **(FK)** | Records billing details for each table’s order. |
| **Order** | OrderID **(PK)**, OrderTime, CategoryID **(FK)** | Represents a customer’s food order. |
| **Category** | CategoryID **(PK)**, Price | Defines dish categories and their prices. |
| **Dish** | DishID **(PK)**, Name, CategoryID **(FK)** | Represents dishes (e.g., Juice, Idly, Rice) available in the restaurant. |
| **Waiter** | WaiterID **(PK)**, Name, Phone | Stores waiter details who serve dishes and customers. |
| **OrderDish** | OrderID **(FK)**, DishID **(FK)** | Resolves M:N relationship between Orders and Dishes (each order can have multiple dishes). |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| **Customer – Reservation** | 1:N | Total on Customer side | A customer can make many reservations; each reservation is made by one customer. |
| **Reservation – Table** | 1:1 | Total on both sides | Each reservation is linked to one table; a table can be reserved once at a time. |
| **Table – Bill** | 1:1 | Total on Table side | Each table has one bill associated per service. |
| **Order – Dish** | M:N | Total on both sides | An order can include multiple dishes; a dish can belong to multiple orders (via OrderDish). |
| **Category – Dish** | 1:N | Total on Category side | Each category includes multiple dishes; each dish belongs to one category. |
| **Dish – Waiter** | 1:N | Total on Dish side | A waiter can serve many dishes; each dish is served by one waiter. |

---

## Assumptions
- Each **customer** has a unique `CustomerID` and can make multiple reservations.  
- Each **reservation** is tied to a specific table and customer at a given time.  
- Each **table** can accommodate a limited number of customers (based on capacity).  
- **Orders** contain one or more dishes, and dishes can appear in many orders.  
- Each **dish** belongs to one category (e.g., South Indian, Beverages).  
- **Waiters** are responsible for serving multiple dishes and handling orders.  
- **Bills** are generated per table after dining, including service charges.  


## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
