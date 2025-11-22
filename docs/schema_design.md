# Schema Design

This section illustrates the **database schema** used in the **Joblelo Platform** project. The system uses **PostgreSQL** hosted on **AWS RDS**

---

## Entity Relationship Diagram (ERD)

Below is the ER diagram representing the structure and relationships between the tables:

![aws](../assets/schema.png)

---

## Table Details

Below are detailed descriptions of each table and their respective fields.

---

### USERS

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each user. |
| **full_name** | VARCHAR | Full name of the user. |
| **email** | VARCHAR | User’s email address (must be unique). |
| **phone** | VARCHAR | User’s contact number. |
| **password** | VARCHAR | Hashed password using bcrypt. |
| **work_email** | VARCHAR | Work email of recruiter. |
| **city** | VARCHAR | City of user. |
| **state** | VARCHAR | State of user. |
| **country** | VARCHAR | Country of user. |
| **resume_url** | TEXT | URL of the uploaded resume. |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

### ROLES

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for the role. |
| **name** | VARCHAR | Role name — e.g., `Job Seeker`, `Employer`. |

---

### USER_ROLES

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each record. |
| **role_id** | INT (FK) | References `ROLES.id`. |
| **user_id** | INT (FK) | References `USERS.id`. |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

### COMPANIES

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each company. |
| **name** | VARCHAR | Company name. |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

### COMPANY_USER

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each record. |
| **company_id** | INT (FK) | References `COMPANIES.id`. |
| **user_id** | INT (FK) | References `USERS.id`. |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

### JOBS

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each job posting. |
| **company_id** | INT (FK) | References `COMPANIES.id`. |
| **created_by** | INT (FK) | References `USERS.id` (Employer who created the job). |
| **title** | VARCHAR | Job title. |
| **job_description** | TEXT | Detailed job description. |
| **salary** | VARCHAR | Salary or compensation details. |
| **city** | VARCHAR | City of job. |
| **state** | VARCHAR | State of job. |
| **country** | VARCHAR | Country of job. |
| **job_type** | ENUM | Type of job (e.g., Full-Time, Part-Time, Internship). |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

### APPLICATIONS

| Field | Data Type | Description |
|--------|------------|-------------|
| **id** | SERIAL (PK) | Unique identifier for each application. |
| **job_id** | INT (FK) | References `JOBS.id`. |
| **job_seeker_id** | INT (FK) | References `USERS.id`. |
| **status** | ENUM | Application status (`Applied`, `Accepted`, `Rejected`). |
| **created_at** | TIMESTAMPTZ | Record creation timestamp. |
| **updated_at** | TIMESTAMPTZ | Record update timestamp. |
| **deleted_at** | TIMESTAMPTZ | Soft delete marker. |

---

## Indexing Strategy

To enhance query performance for common operations like login, job search, and application tracking, selective single and composite indexes are implemented on frequently accessed columns.

| Table Name | Indexed Column(s) | Reason for Indexing | Use Case |
|-------------|------------------|---------------------|-----------|
| **users** | `email` | Ensures unique user login and faster authentication lookups. | Validate login credentials instantly using email. |
| **roles** | `name` | Speeds up role identification during authorization checks. | Quickly verify role type (Job Seeker, Employer, Admin). |
| **user_roles** | (`user_id`, `role_id`) *(Composite)* | Optimizes role-based permission checks. | Retrieve roles assigned to a specific user. |
| **companies** | `name` | Allows faster company searches and suggestions. | Find a company while posting or managing jobs. |
| **jobs** | (`location`, `job_type`) *(Composite)* | Improves search and filtering performance for job listings. | Display jobs filtered by title or company. |
| **applications** | (`job_id`, `job_seeker_id`) *(Composite)* | Prevents duplicate applications and speeds up lookups. | Check if a job seeker has already applied to a job. |
