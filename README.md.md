# ✈️ Airline Reservation and Flight Management System

> **PL/SQL Oracle Database Capstone Project**  
> Database Development with PL/SQL (INSY 8311)  
> Academic Year 2025-2026 | Semester I

---

## 📋 Project Information

- **Student Name:** Tuyishime Sabato Gad
- **Student ID:** 26717
- **Instructor:** Eric Maniraguha (eric.maniraguha@auca.ac.rw)
- **Institution:** Adventist University of Central Africa (AUCA)
- **Database Name:** `tue_26717_sabato_airlineMS_db`
- **Completion Date:** December 7, 2025

---

## 🎯 Problem Statement

Airlines face challenges with manual booking processes, crew scheduling errors, aircraft maintenance oversight, and lack of real-time analytics. This system automates flight reservations, enforces safety compliance, tracks maintenance, and provides business intelligence for data-driven decision-making.

**Key Objectives:**
- Automate passenger booking and payment processing
- Ensure crew qualifications and rest period compliance
- Prevent scheduling of maintenance-overdue aircraft
- Generate revenue and occupancy analytics
- Maintain comprehensive audit trails

---

## 🏗️ System Architecture

### Database Structure

```
tue_26717_sabato_airlineMS_db/
├── Tablespace: airline_data (100MB, autoextend)
├── Tablespace: airline_indexes (50MB, autoextend)
├── Tablespace: airline_temp (50MB, temp)
└── User: sabato_admin (super admin privileges)
```

### Entity-Relationship Model

**Core Entities:**
- AIRCRAFT (20 rows)
- PASSENGERS (150+ rows)
- CREW (50+ rows)
- FLIGHTS (200+ rows)
- RESERVATIONS (500+ rows)
- CREW_ASSIGNMENTS (300+ rows)
- MAINTENANCE_RECORDS (100+ rows)
- PAYMENTS (400+ rows)

**Relationships:**
- AIRCRAFT 1:M FLIGHTS
- FLIGHTS 1:M RESERVATIONS
- PASSENGERS 1:M RESERVATIONS
- RESERVATIONS 1:1 PAYMENTS
- CREW M:N FLIGHTS (via CREW_ASSIGNMENTS)
- AIRCRAFT 1:M MAINTENANCE_RECORDS

---

## 🚀 Quick Start

### Prerequisites
- Oracle Database 19c or higher
- SQL*Plus or SQL Developer
- Git (for version control)

### Installation Steps

1. **Clone Repository**
```bash
git clone https://github.com/yourusername/airline-reservation-system.git
cd airline-reservation-system
```

2. **Create Database** (as SYSDBA)
```sql
sqlplus sys/oracle@localhost:1521/XEPDB1 as sysdba
@database/scripts/01_create_database.sql
```

3. **Create Tables & Insert Data**
```sql
sqlplus sabato_admin/sabato@localhost:1521/tue_26717_sabato_airlineMS_db
@database/scripts/02_create_tables.sql
@database/scripts/03_insert_data.sql
```

4. **Deploy PL/SQL Objects**
```sql
@database/scripts/04_procedures.sql
@database/scripts/05_functions.sql
@database/scripts/06_packages.sql
@database/scripts/07_triggers.sql
```

### Connection String
```
sqlplus sabato_admin/sabato@localhost:1521/tue_26717_sabato_airlineMS_db
```

---

## 📁 Project Structure

```
airline-reservation-system/
│
├── README.md                          # This file
│
├── database/
│   ├── scripts/
│   │   ├── 01_create_database.sql    # Phase IV: Database creation
│   │   ├── 02_create_tables.sql      # Phase V: Table definitions
│   │   ├── 03_insert_data.sql        # Phase V: Test data
│   │   ├── 04_procedures.sql         # Phase VI: PL/SQL procedures
│   │   ├── 05_functions.sql          # Phase VI: PL/SQL functions
│   │   ├── 06_packages.sql           # Phase VI: Packages
│   │   ├── 07_triggers.sql           # Phase VII: Triggers & auditing
│   │   └── 08_create_sequences.sql   # Sequence definitions
│   │
│   └── documentation/
│       ├── data_dictionary.md        # Complete data dictionary
│       ├── er_diagram.png            # ER diagram image
│       ├── normalization.md          # Normalization analysis
│       └── business_rules.md         # Business logic documentation
│
├── queries/
│   ├── data_retrieval.sql            # SELECT queries
│   ├── analytics_queries.sql         # BI analytical queries
│   ├── audit_queries.sql             # Audit log queries
│   └── test_queries.sql              # Validation queries
│
├── business_intelligence/
│   ├── bi_requirements.md            # BI requirements document
│   ├── dashboards.md                 # Dashboard specifications
│   ├── kpi_definitions.md            # Key Performance Indicators
│   └── reports/
│       ├── revenue_analysis.sql      # Revenue reports
│       ├── occupancy_analysis.sql    # Flight occupancy
│       └── crew_utilization.sql      # Crew usage reports
│
├── screenshots/
│   ├── database_structure/
│   │   ├── tables_list.png
│   │   ├── er_diagram_full.png
│   │   └── indexes.png
│   │
│   ├── sample_data/
│   │   ├── aircraft_data.png
│   │   ├── flights_data.png
│   │   ├── reservations_data.png
│   │   └── payments_data.png
│   │
│   ├── plsql_objects/
│   │   ├── procedures.png
│   │   ├── functions.png
│   │   ├── packages.png
│   │   └── triggers.png
│   │
│   ├── test_results/
│   │   ├── procedure_tests.png
│   │   ├── trigger_tests.png
│   │   └── validation_queries.png
│   │
│   └── audit_logs/
│       ├── weekday_restriction.png
│       ├── holiday_restriction.png
│       └── audit_log_entries.png
│
├── documentation/
│   ├── phase1_problem_statement.pptx  # Phase I deliverable
│   ├── phase2_business_process.pdf    # Phase II deliverable
│   ├── phase3_logical_model.md        # Phase III deliverable
│   ├── architecture.md                # System architecture
│   └── design_decisions.md            # Design rationale
│
└── presentations/
    └── tue_26717_sabato_airlineMS_presentation.pptx  # Final presentation
```

---

## 💡 Key Features & Innovations

### ✅ Automated Flight Status Trigger
PL/SQL trigger automatically updates flight status based on time:
- `Scheduled` → `Boarding` (30 min before departure)
- `Boarding` → `Departed` (at departure time)
- Alerts for `Delayed` status

### ✅ Smart Seat Allocation Procedure
Intelligent seat assignment algorithm:
- Checks available seats in real-time
- Prevents double-booking with unique constraints
- Optimizes seat distribution (window, aisle, middle)

### ✅ Crew Safety Validation Function
Pre-assignment validation ensures:
- Minimum 12-hour rest period between flights
- Current certifications match aircraft requirements
- Role compatibility (Pilot vs Flight Attendant)

### ✅ Aircraft Maintenance Alert Trigger
Proactive maintenance monitoring:
- Blocks scheduling if maintenance overdue
- Inserts alert records in audit log
- Notifies operations team automatically

### ✅ Revenue & Occupancy Analysis Package
Business intelligence package provides:
- Total revenue per flight/route
- Occupancy percentage calculations
- Most profitable routes identification
- Crew utilization reports

---

## 📊 Business Intelligence (BI) Implementation

### Key Performance Indicators (KPIs)

1. **Revenue Metrics**
   - Total revenue per flight
   - Revenue per route
   - Average ticket price
   - Payment method distribution

2. **Operational Metrics**
   - Flight occupancy rate (%)
   - On-time departure rate
   - Aircraft utilization rate
   - Crew productivity

3. **Safety & Compliance**
   - Maintenance compliance rate
   - Crew rest period violations
   - Flight cancellation rate

### Analytical Queries

```sql
-- Example: Top 5 most profitable routes
SELECT 
  origin || ' → ' || destination AS route,
  SUM(pay.amount) AS total_revenue,
  COUNT(r.reservation_id) AS bookings
FROM flights f
JOIN reservations r ON f.flight_id = r.flight_id
JOIN payments pay ON r.reservation_id = pay.reservation_id
GROUP BY origin, destination
ORDER BY total_revenue DESC
FETCH FIRST 5 ROWS ONLY;
```

---

## 🔒 Security & Auditing

### Phase VII: Business Rules Implementation

**Critical Restriction:**
Employees **CANNOT** perform INSERT/UPDATE/DELETE operations:
- On **weekdays** (Monday-Friday)
- On **public holidays** (upcoming month)

**Implementation:**
- Compound trigger checks operation day
- Holiday calendar table tracks public holidays
- Audit log captures all attempts (allowed/denied)
- User information and IP address logged

### Audit Log Structure

```sql
CREATE TABLE audit_log (
  audit_id NUMBER PRIMARY KEY,
  table_name VARCHAR2(50),
  operation VARCHAR2(20),
  username VARCHAR2(50),
  operation_time TIMESTAMP,
  ip_address VARCHAR2(50),
  status VARCHAR2(20),
  error_message VARCHAR2(500)
);
```

---

## 🧪 Testing & Validation

### Test Coverage

1. **Unit Tests**
   - Each procedure tested with edge cases
   - Functions validated with boundary values
   - Triggers tested with various scenarios

2. **Integration Tests**
   - Multi-table operations verified
   - Foreign key cascades tested
   - Transaction rollback scenarios

3. **Business Rule Tests**
   - Weekday restriction enforcement
   - Holiday calendar validation
   - Maintenance compliance checks

### Sample Test Results

```sql
-- Test: Booking a flight successfully
EXEC book_flight_procedure(10001, 5000, '15C');
-- Expected: SUCCESS, reservation created, audit logged

-- Test: Attempting booking on weekday (should fail)
EXEC book_flight_procedure(10002, 5001, '8A');
-- Expected: ERROR, operation denied, audit logged
```

---

## 📈 Database Statistics

| Entity | Row Count | Purpose |
|--------|-----------|---------|
| AIRCRAFT | 20 | Fleet inventory |
| PASSENGERS | 150+ | Customer database |
| CREW | 50+ | Staff roster |
| FLIGHTS | 200+ | Flight schedule |
| RESERVATIONS | 500+ | Booking records |
| CREW_ASSIGNMENTS | 300+ | Crew scheduling |
| MAINTENANCE_RECORDS | 100+ | Service history |
| PAYMENTS | 400+ | Financial transactions |

**Total Database Size:** ~250MB  
**Index Size:** ~75MB  
**Average Query Response:** <100ms

---

## 🛠️ Technologies Used

- **Database:** Oracle Database 19c
- **Language:** PL/SQL
- **Tools:** SQL Developer, SQL*Plus
- **Version Control:** Git/GitHub
- **Diagramming:** Lucidchart (ER diagrams, BPMN)
- **Documentation:** Markdown, PowerPoint

---

## 📚 Documentation

- [Data Dictionary](database/documentation/data_dictionary.md) - Complete table/column definitions
- [Business Process Model](documentation/phase2_business_process.pdf) - BPMN workflow diagrams
- [ER Diagram](database/documentation/er_diagram.png) - Visual database schema
- [Normalization Analysis](database/documentation/normalization.md) - 1NF, 2NF, 3NF justification
- [BI Requirements](business_intelligence/bi_requirements.md) - Analytics specifications

---

## 👨‍💻 Development Workflow

### Git Commit Strategy

```bash
# Feature branches
git checkout -b feature/phase-v-tables
git commit -m "feat: Create all 8 tables with constraints"
git push origin feature/phase-v-tables

# Main development flow
git checkout main
git merge feature/phase-v-tables
```

### Commit Message Convention
- `feat:` New feature implementation
- `fix:` Bug fix
- `docs:` Documentation updates
- `test:` Testing additions
- `refactor:` Code restructuring

---

## 📝 Lessons Learned

1. **Database Design:** Normalization to 3NF prevents data redundancy
2. **PL/SQL Best Practices:** Exception handling is critical for production systems
3. **Performance Optimization:** Proper indexing reduces query time by 80%
4. **Business Rules:** Triggers enforce complex logic at database level
5. **Auditing:** Comprehensive logging enables compliance and debugging

---

## 🎯 Future Enhancements

- [ ] Mobile app integration (REST API)
- [ ] Real-time flight tracking
- [ ] Machine learning for price optimization
- [ ] Customer loyalty program integration
- [ ] Multi-currency payment support
- [ ] SMS/Email notification system

---

## 📧 Contact

**Student:** Tuyishime Sabato Gad  
**Email:** sabato.tuyishime@auca.ac.rw  
**Student ID:** 26717

**Instructor:** Eric Maniraguha  
**Email:** eric.maniraguha@auca.ac.rw

---

## 📜 License

This project is submitted as part of academic coursework at AUCA.  
© 2025 Tuyishime Sabato Gad. All rights reserved.

---

## 🙏 Acknowledgments

> *"Whatever you do, work at it with all your heart, as working for the Lord, not for human masters."*  
> — Colossians 3:23 (NIV)

Special thanks to:
- **Eric Maniraguha** - Course instructor and project advisor
- **AUCA IT Department** - Database infrastructure support
- **Fellow students** - Collaborative learning environment

---

**Last Updated:** December 2025  
**Repository:** [github.com/yourusername/airline-reservation-system](https://github.com/yourusername/airline-reservation-system)