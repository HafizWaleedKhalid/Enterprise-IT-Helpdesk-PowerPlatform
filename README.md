# 🏗️ Enterprise IT Helpdesk System

**Platform:** Microsoft Power Platform and Microsoft Dataverse  
**Developer:** Hafiz Waleed Khalid  
**Status:** 🟡 In Progress — Week 4 of 8

---

## 📋 Project Overview

A fully functional, enterprise-grade IT support ticket management system — built from scratch on Microsoft Power Platform and Dataverse.

This is not a tutorial copy. Every design decision, table structure, security model, and automation is planned and built following real enterprise standards — the same way a consulting firm woul[...] 

---

## 🎯 What This Project Demonstrates

- Dataverse data modeling and relational database design
- Custom table creation with proper naming conventions
- Relationships — Lookup, One-to-Many, Many-to-Many
- Power Apps — Canvas and Model Driven App development
- Power Automate — automated ticket assignment and notifications
- Power BI — live management dashboard
- Enterprise security roles and row-level access control
- ALM — solution deployment from Dev to Test to Production

---

## 🗂️ Project Structure

```
Enterprise-IT-Helpdesk-PowerPlatform/
│
├── 📁 screenshots/
│   ├── Week1-Environment-Setup.png
│   ├── Week1-Contact-Table-Columns.png
│   ├── Week2-ITTicket-Columns.png
│   ├── Week2-Category-Data.png
│   ├── Week3-Security.png
│   └── placeholder.md
│
├── 📁 data-model/           (planned — file not present in this branch)
│   └── IT-Helpdesk-DataModel.md
│
├── 📁 docs/                 (planned — file not present in this branch)
│   └── solution-design.md
│
└── README.md
```

---

## 📊 Build Progress

| Week | Milestone | Status |
|------|-----------|--------|
| Week 1 | Environment Setup and Architecture Design | ✅ Complete |
| Week 2 | Data Modeling in Dataverse | ✅ Complete |
| Week 3 | Security Roles and Access Control | ✅ Complete |
| Week 4 | Power Apps UI — Canvas and Model Driven | 🔄 In Progress |
| Week 5 | Power Automate Flows and Business Logic | ⏳ Coming Soon |
| Week 6 | Power BI Reporting and Dashboard | ⏳ Coming Soon |
| Week 7 | ALM and Deployment to Production | ⏳ Coming Soon |
| Week 8 | Final Review and Documentation | ⏳ Coming Soon |

---

## 🗄️ Data Model

### Tables Being Built

| Table | Type | Purpose |
|-------|------|---------|
| IT Ticket | Custom | Core record — every support request |
| Category | Custom | Controlled list — Hardware, Software, Network |
| Contact | Standard | Employees who raise tickets |
| Account | Standard | Departments or organizations |

### Key Relationships

| From Table | To Table | Relationship Type |
|------------|----------|-------------------|
| IT Ticket | Contact | Many tickets → One employee |
| IT Ticket | Category | Many tickets → One category |
| IT Ticket | Contact (Assigned To) | Many tickets → One IT staff member |

---

## 🔐 Security Model Summary

The system uses a structured, team-based security model to enforce data privacy and operational roles.

| Team | Business Unit | Security Role | Access Level (on IT Tickets) |
| :--- | :--- | :--- | :--- |
| **General Employees Team** | General Staff | IT Helpdesk Employee | **User**: Create, Read, Update own tickets only |
| **IT Support Team** | IT Department | IT Helpdesk IT Staff | **Organisation**: Read and Update all tickets |
| **IT Management Team** | IT Department | IT Helpdesk IT Manager | **Organisation**: Full Create, Read, Update, Delete access |

This structure makes it clear that you didn't just create roles, but designed a complete, logical system where each team's permissions match their job function perfectly.

![Business Units hierarchy](screenshots/Week3-BusinessUnits.png)  
*Business Units hierarchy — root org and child business units.*

![Teams and assigned members](screenshots/Week3-Teams.png)  
*Teams and assigned members — mapping to Business Units and Security Roles.*

---

## 🏛️ Architecture Decisions

| Decision | Choice Made | Reason |
|----------|-------------|--------|
| Environment | Separate Dev environment | Never build in Production |
| Table naming | PascalCase — IT_Ticket | Enterprise naming convention |
| Data type for Category | Lookup field | Prevents free-text errors and data integrity issues |
| Solution type | Custom solution | Never build in Default Solution |
| IT Ticket | 11 columns including 3 Lookups | Core helpdesk record |
| Category | Custom table with 4 data rows | Prevents free text category errors |
| hw_TicketStatus | Global Choice | Reusable across tables, updates everywhere |
| hw_TicketPriority | Global Choice | Reusable across tables, updates everywhere |
| Employees | Reuse Contact table | Already built by Microsoft |
| Employee Role | User level access | Cannot see other employees tickets |
| IT Staff Role | Organisation level Read and Update | Full visibility needed for IT work |
| IT Manager Role | Full CRUD Organisation level | Complete system control |
| Security Role: Employee | IT Helpdesk Employee (User level Create/Read/Update on own tickets) | Employees should only manage their own tickets and never see colleague's data. |
| Security Role: IT Staff | IT Helpdesk IT Staff (Organisation level Read/Update) | IT staff need full visibility of all tickets to resolve issues efficiently. |
| Security Role: IT Manager | IT Helpdesk IT Manager (Organisation level Full CRUD) | Managers require complete control for oversight, reporting, and system administration. |
| Business Units | IT Department and General Staff under the root org0709eaea | Mirrors the company org chart to enforce data isolation between departments. |
| Teams | IT Support Team, IT Management Team, General Employees Team | Allows for efficient, group-based permission management, eliminating the need for per-user role assignment. |

---

## 📝 Lessons Learned

*(Updated weekly — real observations from building this project)*

**Week 1:**
- Always create a separate Developer environment before touching anything
- Standard tables like Account and Contact already exist in Dataverse — no need to rebuild them
- Environment region affects data residency — important for enterprise clients
- Lookup field is Dataverse's name for Foreign Key
- Unique Identifier is Dataverse's name for Primary Key
- Choice field = small fixed list, Lookup field = growing list with its own table
- Power Platform tools all share one Dataverse backbone

**Week 2:**
- Schema Name locks permanently after first save — always finalize Display Name before saving
- Two Lookups to Contact table is normal and correct (Raised By and Assigned To)
- Always add data to target table before creating Lookup
- Every table gets automatic system columns — Created By, Modified By, Status (statecode), etc.
- Two columns named Status is normal — hw_Status is ours, statecode is system
- Always create fresh Global Choice with hw_ prefix — not existing system choices
- Canvas card view is unreliable — always use full Columns list view

**Week 3:**
- Security designed before building any app
- Row Level Security — same screen, different data per user type
- **Business Units must be created before assigning to Users or Teams**
- **Each Team requires an Administrator (e.g., yourself) to be saved**
- **Security Roles are assigned to Teams, not directly to individual users**
- Access Teams for temporary external access
- One Team addition = instant correct permissions for any new staff member

---

## 📸 Screenshots

### Week 1 — Environment Setup and Architecture Design
![Week 1 - Environment Setup](screenshots/Week1-Environment-Setup.png)
*Waleed Dev Environment successfully created — Type: Developer, Status: Ready, Dataverse: Enabled*

### Week 1 — Contact Table Columns in Dataverse
![Week 1 - Contact Table](screenshots/Week1-Contact-Table-Columns.png)
*Real Dataverse table showing Lookup (Foreign Key) and Unique Identifier (Primary Key) fields*

### Week 2 — IT Ticket Table Columns
![Week 2 Columns](screenshots/Week2-ITTicket-Columns.png)
*IT Ticket table with all 11 columns built in Dataverse*

### Week 2 — Category Table Data
![Week 2 Category](screenshots/Week2-Category-Data.png)
*Category table with 4 records — Hardware, Software, Network, Access Request*

### Week 3 — Security Model Design
![Week 3 Security](screenshots/Week3-Security.png)
*Complete security architecture — Security Roles,
Business Units, Teams, and Column Security Profiles
designed for IT Helpdesk System*

![Week 3 - Business Units](screenshots/Week3-BusinessUnits.png)  
*Business Units hierarchy — created under the root org to enforce data isolation.*

![Week 3 - Teams](screenshots/Week3-Teams.png)  
*Teams and assigned members — shows Team membership and assigned security roles.*

*(Screenshots added at the end of each week)*

---

## 🔗 Connect

| Platform | Link |
|----------|------|
| **GitHub Profile** | [github.com/HafizWaleedKhalid](https://github.com/HafizWaleedKhalid) |
| **LinkedIn** | [linkedin.com/in/hafiz-waleed-khalid-0b17842b8](https://linkedin.com/in/hafiz-waleed-khalid-0b17842b8) |

---

*Last Updated: July 2026*  
*This repository is updated weekly as each phase completes.*
