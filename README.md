# Vehicle Rental Management System

A PostgreSQL database project for the **Database Systems** course at **The University of Lahore**, prepared for **Ms. Ambreen Akmal**.

## Project Overview

The Vehicle Rental Management System (VRMS) manages the full rental lifecycle for a vehicle rental business. It stores customers, vehicles, bookings, payments, and returns, while supporting availability checks, customer rental history, return processing, late fees, and revenue reporting.

## Repository Structure

```text
Vehicle-Rental-Management-System/
|-- README.md
|-- docs/
|   |-- 01_Project_Proposal.md
|   |-- 02_ER_Analysis.md
|   `-- Project_Documentation.docx
|-- diagrams/
|   |-- ERD.png
|   `-- EERD.jpeg
|-- sql/
|   |-- 01_schema.sql
|   |-- 02_sample_data.sql
|   |-- 03_joins.sql
|   `-- 04_features.sql
`-- screenshots/
    |-- 1 FEATURES.png
    |-- 2 FEATURES.png
    |-- ...
    |-- 10 FEATURES.png
    `-- DCL.png
```

## Deliverables

| Task | Description | File / Folder |
|------|-------------|---------------|
| Phase I | Project proposal | `docs/01_Project_Proposal.md` |
| Phase I | Entities, attributes, and relationships | `docs/02_ER_Analysis.md` |
| Phase I | ERD and EERD diagrams | `diagrams/` |
| Phase I | Schema creation | `sql/01_schema.sql` |
| Phase I | Sample data | `sql/02_sample_data.sql` |
| Phase I | Join queries | `sql/03_joins.sql` |
| Phase II | 10 functional SQL features with DDL, DML, and DCL | `sql/04_features.sql` |
| Phase II | pgAdmin output screenshots | `screenshots/` |
| Final | Complete project documentation | `docs/Project_Documentation.docx` |

## Phase 2 Features

1. Register a new customer
2. Add a new vehicle to inventory
3. Create a new booking
4. Search / filter available vehicles
5. View customer rental history
6. Record a payment
7. Update vehicle status
8. Process a vehicle return with late fee
9. Cancel / delete a booking
10. Generate revenue report by vehicle

## SQL Command Categories Covered

- **DDL:** `CREATE TABLE`, `ALTER TABLE`, `CREATE VIEW`, `CREATE INDEX`
- **DML:** `INSERT`, `SELECT`, `UPDATE`, `DELETE`, `JOIN`, `GROUP BY`
- **DCL:** `CREATE ROLE`, `GRANT`, `REVOKE`

## How to Run in pgAdmin

1. Open **pgAdmin 4** and connect to PostgreSQL.
2. Create a database named `vehiclerentaldb`.
3. Open Query Tool for `vehiclerentaldb`.
4. Run the SQL files in this order:
   - `sql/01_schema.sql`
   - `sql/02_sample_data.sql`
   - `sql/03_joins.sql`
   - `sql/04_features.sql`

If `04_features.sql` is run more than once, the DCL role may already exist. Run this first if needed:

```sql
DROP ROLE IF EXISTS rental_clerk;
```

## Group Members

| Name |
|------|
| Muhammad Usman Tariq |
| Fazal Shahbaz |
| Fahad Zubair |

## Course Info

- **Course:** Database Systems
- **Section:** B
- **Instructor:** Ms. Ambreen Akmal
- **Institution:** The University of Lahore
- **DBMS:** PostgreSQL 15+
- **Tool:** pgAdmin 4
