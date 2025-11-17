# Unit Test Plan – Joblelo Job Platform

## 1. Introduction
This document provides the **Unit Testing Plan** for the **Joblelo Job Platform**, a job portal supporting two roles: **Job Seekers** and **Recruiters**.

The project consists of:

- **Frontend:** React (Vite) + Tailwind + Axios  
- **Backend:** Node.js + Express + Sequelize + PostgreSQL  

Unit testing ensures that every component, API route, and service behaves correctly before deployment and integration.

---

## 2. Objectives
The main goals of unit testing are:

- Verify correctness of **every function, component, and service**.
- Identify bugs early in the development process.
- Maintain a **stable, scalable, and clean codebase**.
- Prevent regressions from new updates.
- Support **mandatory CI/CD testing** for all commits and PRs.

---

## 3. Scope

### Included

### Frontend (React + Tailwind)
- UI Components (Header, HeroSection, Cards, Modals)
- Pages (Landing, Login, Register, Dashboard)
- Context (AuthContext)
- API Layer (Axios services)
- Custom hooks
- Utility functions (validators, formatters)

### Backend (Node + Express + Sequelize)
- Controllers (user, job, application)
- Services (business logic)
- Middlewares (auth, role)
- Routes (`/auth`, `/jobs`, `/applications`)
- Utility functions (`ApiError`, `ApiResponse`, `asyncHandler`)
- Sequelize model interactions (mocked)

### Not Included
- AWS S3 uploads (mocked)
- Full E2E flow
- UI/UX design testing

---

## 4. Test Approach

### Frameworks
- **Jest** – main test runner (frontend + backend)
- **Supertest** – backend API route testing

### Frontend Focus Areas
- Component rendering & events  
- Form validation (positive & negative)  
- API calls via mocked Axios  
- Navigation & redirects  
- AuthContext behavior  

### Backend Focus Areas
- API endpoint responses  
- Positive & negative route testing  
- Authentication/authorization  
- Business logic in services  
- Database operations (mocked)  
- Error handling & utilities  

### Test Folder Structure
```
    frontend/src/tests/
    backend/src/tests/
```

---

## 5. Test Cases (Examples)

### Frontend Test Cases

| Module | Test Case | Type | Expected Result |
|--------|-----------|------|-----------------|
| Header | Renders logo and login button | Positive | Elements visible |
| HeroSection | Renders heading & image | Positive | Correct UI output |
| LoginPage | Valid login | Positive | Navigate to dashboard |
| LoginPage | Incorrect credentials | Negative | Show error message |
| RegisterPage | Missing fields | Negative | Show validation error |
| JobsPage | Renders jobs from API | Positive | Display job cards |
| JobsPage | No jobs available | Negative | Show “No jobs found” |
| AuthContext | Logout | Positive | Clears auth state |
| Axios Service | GET /jobs | Positive | Returns mocked list |

---

### Backend Test Cases

| Module | Test Case | Type | Expected Result |
|--------|-----------|------|-----------------|
| Health Route | GET /health | Positive | 200 + `{status: "ok"}` |
| AuthController | Register user | Positive | 201 success |
| AuthController | Duplicate email | Negative | 409 conflict |
| AuthController | Login valid email/password | Positive | Cookie + 200 |
| AuthController | Wrong password | Negative | 401 unauthorized |
| JobController | Recruiter creates job | Positive | 201 created |
| JobController | Missing token | Negative | 401 unauthorized |
| ApplicationController | Apply for job | Positive | 201 success |
| ApplicationController | Apply twice | Negative | 400 error |
| Auth Middleware | Valid token | Positive | Calls `next()` |
| Auth Middleware | Invalid token | Negative | 401 |
| Utils | validateEmail() | Positive | returns boolean |
| Utils | validateEmail("abc") | Negative | returns false |

---

## 6. Test Schedule

| Activity | Responsibility | When |
|----------|---------------|------|
| Write unit tests | Myself | During each feature |
| Run tests locally | Myself | Before every commit & PR |
| Fix failing tests | Myself | Immediately |
| CI/CD test execution | GitHub Actions | On push & PR |
| Final review | Mentors | Before submission |

---

## 7. Responsibility
I am responsible for:

- Writing and updating unit tests  
- Ensuring test coverage  
- Maintaining stability after changes  

Mentors will verify tests during the final review.

---

## 8. Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Not enough time for tests | Medium | Write tests parallel to development |
| Incorrect mocking of Axios/DB | High | Use Jest mocks consistently |
| Low test coverage | Medium | Monitor coverage reports |
| Tests breaking after code changes | High | Update tests with every change |
| Complex business logic | Medium | Move logic to service layer |

---

## 9. Tools

| Tool | Purpose |
|------|---------|
| Jest | Core testing framework |
| React Testing Library | Component tests |
| Supertest | API route testing |
| Jest Mocks / Sequelize Mock | DB mocking |
| ESLint + Prettier | Code quality |
| GitHub Actions | **Mandatory** CI/CD test automation |
| Axios | Mockable API client |

---

## 10. Commands

### Frontend
```
npm test
npm run test:coverage
```

### Backend
```
npm test
npm run test:coverage
```

### CI/CD
#### Runs automatically on:
- Every push  
- Every pull request  
- Before merging to `develop` or `main`

---

## 11. Summary
This Unit Test Plan ensures the **Joblelo Job Platform** remains stable, accurate, and reliable by enforcing strict testing standards, including:

- Positive + Negative tests  
- Mocked API & database tests  
- Mandatory CI/CD automation  

This plan will guide testing throughout the entire development lifecycle.
