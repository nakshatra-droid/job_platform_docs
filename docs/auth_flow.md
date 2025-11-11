# Authentication and Authorization Flow — Job Portal System

---

## **Authentication & Authorization Flow**

```mermaid
flowchart TD
    %% External Entities
    U[User (Job Seeker / Recruiter)]
    FE[Frontend (React / Web UI)]
    BE[Backend API]
    DB[(PostgreSQL Database)]
    JWT[Auth Token (JWT)]
    
    %% Registration
    U -->|Register: full_name, email, phone, password| FE
    FE -->|POST /register| BE
    BE -->|Hash password & validate input| BE
    BE -->|Insert user record| DB
    DB -->|User Created (is_verified = false)| BE
    BE -->|Send verification link or OTP| U
    
    %% Verification
    U -->|Click verification link / enter OTP| FE
    FE -->|POST /verify| BE
    BE -->|Update is_verified = true| DB
    BE -->|Return success response| FE
    
    %% Login
    U -->|Login: email + password| FE
    FE -->|POST /login| BE
    BE -->|Validate credentials (check hash)| DB
    BE -->|Fetch user roles from USER_ROLES| DB
    BE -->|Generate JWT with user_id & role info| JWT
    JWT --> FE
    FE -->|Stores token (localStorage / cookie)| FE
    
    %% Authorization Flow
    FE -->|Access Protected Route (with JWT)| BE
    BE -->|Verify JWT Signature & Expiry| BE
    BE -->|Decode Role info| BE
    
    BE -->|Role = Job Seeker → Allow job apply endpoints| BE
    BE -->|Role = Recruiter → Allow job posting endpoints| BE
    
    BE -->|Access granted / denied response| FE
```