# Task 2 — Entities, Attributes, and Relationships

## 1. Entities

The system is modeled around **5 strong entities**:

| # | Entity | Purpose |
|---|--------|---------|
| 1 | **CUSTOMER** | Stores personal/contact details of every customer who rents a vehicle |
| 2 | **VEHICLE** | Represents every vehicle in the rental inventory |
| 3 | **BOOKING** | The central transaction — links a customer to a vehicle for a specific date range |
| 4 | **PAYMENT** | Records money paid against a booking (supports multiple installments) |
| 5 | **RETURN** | Records the closure of a booking when the vehicle is returned |

---

## 2. Attributes

### 2.1 CUSTOMER

| Attribute | Type | Description |
|-----------|------|-------------|
| **CustomerID** (PK) | INT | Unique system-generated identifier |
| Name | VARCHAR(100) | Customer's full name |
| CNIC | VARCHAR(15) | National identity number (UNIQUE) |
| Phone | VARCHAR(15) | Contact number |
| Email | VARCHAR(100) | Email address |
| Address | VARCHAR(255) | Residential or business address |

### 2.2 VEHICLE

| Attribute | Type | Description |
|-----------|------|-------------|
| **VehicleID** (PK) | INT | Unique vehicle identifier |
| Make | VARCHAR(50) | Manufacturer (Toyota, Honda, Suzuki, etc.) |
| Model | VARCHAR(50) | Model name (Corolla, Civic, etc.) |
| Year | INT | Manufacturing year |
| LicensePlate | VARCHAR(20) | Government-issued plate (UNIQUE) |
| RentalRate | DECIMAL(10,2) | Rental price per day |
| *Status* | VARCHAR(20) | **Derived** — Available / Rented / Maintenance |

### 2.3 BOOKING

| Attribute | Type | Description |
|-----------|------|-------------|
| **BookingID** (PK) | INT | Unique booking identifier |
| CustomerID (FK) | INT | Reference to CUSTOMER |
| VehicleID (FK) | INT | Reference to VEHICLE |
| StartDate | DATE | Rental start date |
| EndDate | DATE | Planned end date |
| Status | VARCHAR(20) | Active / Completed / Cancelled |
| *TotalDays* | INT | **Derived** — EndDate − StartDate |
| *TotalAmount* | DECIMAL(10,2) | **Derived** — TotalDays × RentalRate |

### 2.4 PAYMENT

| Attribute | Type | Description |
|-----------|------|-------------|
| **PaymentID** (PK) | INT | Unique payment identifier |
| BookingID (FK) | INT | Reference to BOOKING |
| Amount | DECIMAL(10,2) | Payment amount |
| PaymentDate | DATE | Date of payment |
| Method | VARCHAR(20) | Cash / Card / Bank Transfer / Online |

### 2.5 RETURN

| Attribute | Type | Description |
|-----------|------|-------------|
| **ReturnID** (PK) | INT | Unique return identifier |
| BookingID (FK) | INT | Reference to BOOKING (UNIQUE — 1:1) |
| ReturnDate | DATE | Actual return date |
| Condition | VARCHAR(50) | Excellent / Good / Damaged |
| LateFee | DECIMAL(10,2) | Fee applied if returned after EndDate |

> **Derived attributes** are shown with dashed ovals in the ERD and are computed at query-time rather than stored physically.

---

## 3. Relationships

| # | Relationship | Between | Cardinality | Participation | Business Meaning |
|---|--------------|---------|-------------|---------------|------------------|
| 1 | **Makes** | Customer ↔ Booking | 1 : N | Customer: Partial, Booking: Total | One customer can make many bookings; every booking belongs to exactly one customer |
| 2 | **For** | Booking ↔ Vehicle | N : 1 | Booking: Total, Vehicle: Partial | A vehicle can have many bookings over time; each booking is for exactly one vehicle |
| 3 | **Has Payment** | Booking ↔ Payment | 1 : N | Booking: Partial, Payment: Total | A booking can have multiple installment payments; each payment belongs to one booking |
| 4 | **Ends With** | Booking ↔ Return | 1 : 1 | Booking: Partial, Return: Total | Each booking ends with exactly one return record (or zero if still active) |

---

## 4. Summary Counts

- **5 Entities** (in basic ERD) → **10 Entities** with EER subclasses
- **27 Attributes** (5 PKs + 3 derived + 19 simple) → **39 Attributes** with EER subclass attributes
- **4 Relationships**

---

## 5. EER Extensions (Specialization)

The basic ERD is extended into an EERD with two **disjoint, total** specializations:

### 5.1 CUSTOMER Specialization
- **Individual Customer** — adds: DOB, Gender
- **Corporate Customer** — adds: CompanyName, TaxID, ContactPerson

### 5.2 VEHICLE Specialization
- **Car** — adds: SeatingCapacity, Transmission, FuelType
- **Bike** — adds: EngineCC, BikeType
- **Truck** — adds: LoadCapacity, NumAxles

Both specializations are:
- **Disjoint (d)** — a customer or vehicle belongs to exactly one subclass
- **Total participation** — every superclass instance MUST be classified into a subclass
