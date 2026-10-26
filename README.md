# Hotel Management System (MySQL)

## Project Overview

Hotel Management System is a MySQL database project designed to manage customer details, room information, bookings, and payments. It uses SQL queries to retrieve booking details, check room availability, and summarize payments for hotel operations.

**Database:** `HotelManagement`  
**Technology:** MySQL 8.0+  
**Tool:** MySQL Workbench  
**Core tables:** 4

## Project Aim

The main aim of the Hotel Management System is to organize hotel customer, room, booking, and payment information in a relational database. The project demonstrates how SQL can support everyday hotel tasks such as checking reservations, viewing room availability, and tracking payments.

## Objectives

- Store and manage customer details.
- Maintain room numbers, room types, and room prices.
- Record customer bookings with check-in and check-out dates.
- Record payments associated with bookings.
- Retrieve booking information using SQL joins.
- Check rooms that are not booked on a selected date.
- Summarize payments for each booking.
- Demonstrate SQL concepts such as primary keys, foreign keys, indexes, views, stored procedures, and triggers.

## Database Tables

| Table | Purpose |
|---|---|
| `Customers` | Stores customer names, phone numbers, and email addresses. |
| `Rooms` | Stores room numbers, room types, and prices. |
| `Bookings` | Connects customers to rooms and stores check-in/check-out dates. |
| `Payments` | Stores payment amounts, dates, and payment methods for bookings. |

## Important Attributes

### 1. Customers
- `customer_id` — Primary Key (PK), auto-increment
- `customer_name`
- `phone`
- `email`

### 2. Rooms
- `room_id` — Primary Key (PK), auto-increment
- `room_number` — Unique
- `room_type`
- `price`

### 3. Bookings
- `booking_id` — Primary Key (PK), auto-increment
- `customer_id` — Foreign Key (FK) referencing `Customers`
- `room_id` — Foreign Key (FK) referencing `Rooms`
- `check_in`
- `check_out`

### 4. Payments
- `payment_id` — Primary Key (PK), auto-increment
- `booking_id` — Foreign Key (FK) referencing `Bookings`
- `amount`
- `payment_date`
- `payment_method`

PK means Primary Key, and FK means Foreign Key.

## Entity Relationships

- `Customers` → `Bookings`: One-to-many (1:N). One customer can have multiple bookings.
- `Rooms` → `Bookings`: One-to-many (1:N). A room can appear in multiple bookings over time.
- `Bookings` → `Payments`: One-to-many (1:N). A booking can have multiple payment records.

The foreign keys ensure that bookings refer to existing customers and rooms, and payments refer to existing bookings. The current schema does not itself prevent overlapping bookings for the same room.

## Main SQL Analyses

- Display customer booking details by joining `Customers`, `Bookings`, and `Rooms`.
- Find rooms not booked on a specified date.
- Summarize the total amount paid for each booking.
- List customer, room, and booking information using `JOIN`.
- Identify bookings that have no payment records using `LEFT JOIN`.
- Review room prices and payment totals for basic management reporting.

## SQL Concepts Used

- `CREATE DATABASE` and `CREATE TABLE`
- Primary keys, foreign keys, `AUTO_INCREMENT`, and `UNIQUE`
- `INSERT`, `SELECT`, and `WHERE`
- `JOIN` and `LEFT JOIN`
- `GROUP BY` and aggregate functions such as `SUM()`
- Indexes
- Views
- Stored procedures
- Triggers and validation using `SIGNAL SQLSTATE`

## Views

- `CustomerBookingDetails` — Shows customer contact information, room details, and booking dates.
- `AvailableRooms` — Shows rooms that are not booked today.
- `BookingPaymentSummary` — Shows booking details and the total amount paid.

The `AvailableRooms` view checks availability for the current date only. It is not a complete date-range reservation check.

## Stored Procedures

- `GetCustomerBookings` — Retrieves booking details for a selected customer ID.
- `CheckAvailableRooms` — Lists rooms not booked on a specified date.
- `GetBookingPaymentDetails` — Shows the total payment recorded for a selected booking ID.

## Triggers

- `CheckRoomPrice` — Rejects inserted rooms with a price less than or equal to zero.
- `CheckBookingDates` — Rejects inserted bookings when the check-out date is not after the check-in date.
- `CheckPaymentAmount` — Rejects inserted payments with an amount less than or equal to zero.

These triggers validate `INSERT` operations only. Corresponding update triggers would be needed to apply the same checks to updates.

## How to Run the Project

1. Install MySQL Server 8.0 or later.
2. Open MySQL Workbench and connect to your MySQL server.
3. Create or select the database:

   ```sql
   CREATE DATABASE HotelManagement;
   USE HotelManagement;
   ```

4. Run the `CREATE TABLE` statements for `Customers`, `Rooms`, `Bookings`, and `Payments` in order.
5. Insert sample data. Insert customers and rooms before bookings, then insert payments after bookings.
6. Create the indexes, views, stored procedures, and triggers. Run each object-creation statement only once.
7. Execute the queries and inspect the results.

To verify the tables:

```sql
USE HotelManagement;
SHOW TABLES;
```

To view sample records:

```sql
SELECT * FROM Customers;
SELECT * FROM Rooms;
SELECT * FROM Bookings;
SELECT * FROM Payments;
```

To list the views and triggers:

```sql
SHOW FULL TABLES WHERE Table_type = 'VIEW';
SHOW TRIGGERS FROM HotelManagement;
```

## Limitations

- The project uses a simplified hotel database schema.
- The sample data is for demonstration and may not represent real hotel records.
- The `AvailableRooms` view checks availability for today only.
- The schema does not automatically prevent overlapping bookings for the same room and date range.
- The payment summary reports amounts recorded; it does not calculate every possible extra charge, discount, tax, or refund.
- The project stores and queries records; it does not include a customer-facing booking website or application.

## Future Enhancements

- Add guest check-in and check-out status.
- Prevent overlapping bookings for the same room and date range.
- Add booking status, cancellation, and refund details.
- Calculate total room charges based on the number of nights.
- Track outstanding balances, taxes, discounts, and additional services.
- Build a dashboard or front-end application connected to the database.
- Add update-validation triggers and audit logs.

## Conclusion

The Hotel Management System demonstrates how MySQL can organize customer, room, booking, and payment information in a relational database. It combines database relationships with practical queries, views, stored procedures, indexes, and triggers to support basic hotel-management tasks. It is a suitable beginner SQL project and can be extended with more complete reservation and billing features.
