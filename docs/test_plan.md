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
- Achieve a minimum **80%+ test coverage** across the code.

---

## 3. Scope

### Included

### Frontend (React + Tailwind)
- UI Components
- Pages
- Context 
- API Layer
- Custom hooks

### Backend (Node + Express + Sequelize)
- Controllers 
- Services 
- Middlewares 
- Routes
- Utility functions
- Sequelize model interactions

---

## 4. Test Approach

### Frameworks
- **Jest** – main test runner (frontend + backend)
- **Supertest** – backend API route testing

### Tools Versioning
To maintain consistency across the team:

- **Jest:** 29.x  
- **React Testing Library:** 14.x  
- **Supertest:** 6.x  
- **Node.js:** LTS  
- **Vite:** Latest stable  

### Environment Setup Notes
- Backend DB operations will be mocked (no real DB connection).  
- A **.env.test** file will contain safe values such as:  
  ```
  JWT_SECRET=testsecret
  DB_URL=test-db-url
  ```
- Axios requests in frontend tests will use mocked functions.  
- Sequelize models will be mocked in backend tests.

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
- Business logic 
- Database operations (mocked)  
- Error handling & utilities
- Negative cases such as:  
  - Invalid inputs  
  - Missing fields  
  - Unauthorized access  
  - Database failure scenarios   

### Test Data Strategy
Mock data will be used for all unit tests.  
Examples:

**User payload:**
```json
{
  "email": "test@example.com",
  "password": "Password@123"
}
```

**Mock API responses:**
```json
{
  "status": "success",
  "data": []
}
``` 

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
| ESLint | Code quality |
| GitHub Actions | CI/CD test automation |
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

## CI/CD
The CI/CD pipeline will run automatically on:

- Every push to the `main` branch  
- Every pull request targeting the `main` branch  

## Reporting
- Test results displayed in terminal  
- Coverage reports generated using Jest  
- CI/CD logs available in GitHub Actions  

---

## 11. Acceptance Criteria
For unit testing to be considered complete:

- Minimum **80%+ coverage** achieved  
- All unit tests pass with **no failures**  
- Negative test cases included  
- All DB/external services mocked  
- CI/CD pipeline must pass  
- No console errors or uncaught exceptions in tests  

---

## 12. Summary
This Unit Test Plan ensures the **Joblelo Job Platform** remains stable, accurate, and reliable by enforcing strict testing standards, including:

- Positive + Negative tests  
- Mocked API & database tests  
- Coverage targets  
- Test data strategy  
- CI/CD automation  
- Clear acceptance criteria  

