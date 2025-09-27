# ER Diagram Workshop

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
<img width="769" height="508" alt="image" src="https://github.com/user-attachments/assets/46e1f98e-3385-4776-ad15-041cc6195582" />


### Entities and Attributes

| Entity    | Attributes (PK, FK) | Notes |
|-----------|----------------------|-------|
| Member    | member_id (PK), name, gender, dob, email, membership_type, start_date | Represents gym members who register for programs. |
| Program   | program_id (PK), program_name, fee, duration, schedule | Represents the different fitness programs (e.g., Yoga, Zumba, Weight Training). |
| Trainer   | trainer_id (PK), trainer_name, trainer_gender, trainer_phone, trainer_email, expertise | Stores trainer information (e.g., contact details, expertise). |
| Session   | session_id (PK), date, time, trainer_id (FK), program_id (FK) | Represents individual time-bound classes. |
| Payment   | payment_id (PK), amount, payment_type, payment_date, member_id (FK), program_id (FK) | Records payments made by members for specific programs. |
| Attendance| attendance_id (PK), status, session_id (FK), member_id (FK) | Tracks attendance of members in specific sessions. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| enrolls_in   | M:N | Member (Total), Program (Partial) | A member can enroll in multiple programs; a program can have many members. |
| leads        | 1:M | Program (Total), Trainer (Partial) | Each program is led by one trainer, but a trainer may lead multiple programs. |
| registers    | M:N | Both Partial | A member can register for many sessions, and each session can have many members. |
| includes     | 1:M | Program (Total), Session (Total) | A program includes multiple sessions, but each session belongs to only one program. |
| has          | 1:M | Member (Total), Payment (Total) | A member can make many payments; each payment belongs to one program. |
| attends      | 1:M | Session (Total), Attendance (Total) | A session can have multiple attendance records. |

### Assumptions
- A member must enroll in at least one program.
- A program must be led by at least one trainer.
- Payments are tied to members and programs (not to trainers directly).
- Attendance is tracked at the session level.


---

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
<img width="725" height="517" alt="image" src="https://github.com/user-attachments/assets/4b613b28-4563-4e2e-894a-b7e211bdc0d6" />


### Entities and Attributes

| Entity       | Attributes (PK, FK) | Notes |
|--------------|----------------------|-------|
| Member       | member_id (PK), name, gender, dob, email | Represents library members. |
| Book         | book_id (PK), title, author, category | Represents books available for borrowing. |
| Borrowing    | borrow_id (PK), loan_date, return_date, fine_amount, member_id (FK), book_id (FK) | Tracks loans and returns of books. |
| Event        | event_id (PK), event_name, date, room_id (FK) | Cultural/library events. |
| Speaker      | speaker_id (PK), name, expertise | Guest speakers/authors at events. |
| Room         | room_id (PK), room_name, capacity, type | Rooms booked for events or study purposes. |
| Registration | registration_id (PK), member_id (FK), event_id (FK) | Records member registrations for events. |

### Relationships and Constraints

| Relationship  | Cardinality | Participation | Notes |
|---------------|-------------|---------------|-------|
| borrows       | M:N | Member (Total), Book (Partial) | A member can borrow many books; books can be borrowed multiple times. |
| registers_for | M:N | Both Partial | A member can register for many events; events can have many members. |
| hosts         | M:N | Event (Total), Speaker (Partial) | An event can have many speakers; a speaker can host multiple events. |
| booked_in     | 1:M | Room (Total), Event (Partial) | Each event takes place in one room; rooms can host many events. |
| incurs        | 1:M | Borrowing (Total), Fine (Partial) | Late returns generate fines. |

### Assumptions
- A book can only be borrowed by one member at a time.
- Events must be assigned to one room.
- Fines are calculated based on return_date vs. due_date.
- Some events may not have speakers, but most do.

---

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
<img width="702" height="522" alt="image" src="https://github.com/user-attachments/assets/4ccb442c-a484-4884-a8e6-7968893954c9" />
# C: Restaurant Table Reservation & Ordering

### Entities and Attributes

| Entity       | Attributes (PK, FK) | Notes |
|--------------|----------------------|-------|
| Customer     | customer_id (PK), name, phone, email | Represents restaurant customers. |
| Reservation  | reservation_id (PK), date, time, number_of_guests, customer_id (FK), waiter_id (FK) | Table reservations. |
| Waiter       | waiter_id (PK), waiter_name, waiter_phone | Waiters serving reservations. |
| Order        | order_id (PK), order_date, order_time, reservation_id (FK) | Orders placed during a reservation. |
| Dish         | dish_id (PK), dish_name, price, category_id (FK) | Food items in the menu. |
| Category     | category_id (PK), category_name | Categories like starter, main, dessert. |
| Bill         | bill_id (PK), total_amount, service_charge, reservation_id (FK) | Bill generated for a reservation. |
| OrderDetails | order_id (FK), dish_id (FK), quantity | Junction table for the M:N relation between Order and Dish. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| reserves     | 1:M | Customer (Total), Reservation (Partial) | A customer can make many reservations. |
| serves       | 1:M | Waiter (Partial), Reservation (Total) | Each reservation is assigned to one waiter. |
| places       | 1:M | Reservation (Total), Order (Partial) | A reservation can place many orders. |
| contains     | M:N | Order (Total), Dish (Partial) | Orders can contain many dishes; dishes can appear in many orders. |
| belongs_to   | 1:M | Category (Total), Dish (Total) | Each dish belongs to one category. |
| billed       | 1:1 | Reservation (Total), Bill (Total) | Each reservation generates one bill. |

### Assumptions
- Every reservation must be linked to one customer and one waiter.
- Each reservation generates exactly one bill.
- Orders are tied to reservations (walk-ins are treated as reservations too).
- Each dish belongs to exactly one category.


---
