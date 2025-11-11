# Schema Design

This section illustrates the **database schema** used in the **Job Platform** project. The system uses **PostgreSQL** hosted on **AWS RDS**

---

## Entity Relationship Diagram (ERD)

Below is the ER diagram representing the structure and relationships between the tables:

```mermaid
---
config:
  layout: dagre
---
erDiagram

    ROLES {
        SERIAL id PK
        VARCHAR name
    }

    USER_ROLES {
        SERIAL id PK ""
        INT role_id FK ""
        INT user_id FK ""
        TIMESTAMPTZ created_at ""
        TIMESTAMPTZ updated_at ""
        TIMESTAMPTZ deleted_at ""
    }

    USERS {
        SERIAL id PK ""
        VARCHAR full_name ""
        VARCHAR email ""
        VARCHAR phone ""
        VARCHAR password ""
        BOOLEAN is_verified ""
        TEXT address ""
        TEXT resume_url ""
    }

    COMPANIES {
        SERIAL id PK ""
        VARCHAR name ""
        TIMESTAMPTZ created_at ""
        TIMESTAMPTZ updated_at ""
        TIMESTAMPTZ deleted_at ""
    }

    COMPANY_USER {
        SERIAL id PK ""
        INT company_id FK ""
        INT user_id FK ""
        TIMESTAMPTZ created_at ""
        TIMESTAMPTZ updated_at ""
        TIMESTAMPTZ deleted_at ""
    }

    JOBS {
        SERIAL id PK ""
        INT company_id FK ""
        INT created_by FK ""
        VARCHAR title ""
        TEXT job_description ""
        VARCHAR salary ""
        VARCHAR location ""
        ENUM job_type ""
        TIMESTAMPTZ created_at ""
        TIMESTAMPTZ updated_at ""
        TIMESTAMPTZ deleted_at ""
    }

    APPLICATIONS {
        SERIAL id PK ""
        INT job_id FK ""
        INT job_seeker_id FK ""
        ENUM status ""
        TIMESTAMPTZ created_at ""
        TIMESTAMPTZ updated_at ""
        TIMESTAMPTZ deleted_at ""
    }

    USERS ||--o{ COMPANY_USER : "is linked to company"
    COMPANIES ||--o{ COMPANY_USER : "has company users"
    COMPANIES ||--o{ JOBS : "owns job listings"
    USERS ||--o{ JOBS : "creates job listings"
    JOBS ||--o{ APPLICATIONS : "receives applications"
    USER_ROLES }o--|| USERS : ""
    ROLES ||--o{ USER_ROLES : ""

```