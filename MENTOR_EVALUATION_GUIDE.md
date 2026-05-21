# Mentor Evaluation Guide

Use this file to evaluate student progress in the Antigravity 2.0 MERN + Next.js Full-Stack Course.

---

## Evaluation philosophy

Do not evaluate only the final UI.

Evaluate whether the student can:

```txt
Plan
Build
Review
Test
Secure
Deploy
Document
Explain
```

The project is successful only if the student understands it.

---

## Evaluation flow

Use this order:

1. Check GitHub repository structure.
2. Read README.
3. Open live frontend.
4. Open backend health URL.
5. Test demo credentials.
6. Test user flow.
7. Test admin flow.
8. Check docs.
9. Check QA reports.
10. Ask technical questions.
11. Ask AI usage questions.
12. Ask one bug/debugging question.

---

## Final project scoring

Total: **100 points**

| Area | Points |
|---|---:|
| Planning and specifications | 10 |
| Design analysis and UI quality | 12 |
| Frontend implementation | 15 |
| Backend implementation | 15 |
| Full-stack integration | 12 |
| Authentication and authorization | 8 |
| Testing and QA | 10 |
| Deployment | 8 |
| README and documentation | 7 |
| Code ownership and explanation | 3 |

---

## Red flags

A project should not pass if:

```txt
1. Student cannot explain the code.
2. README claims features that do not work.
3. Admin APIs are not protected on backend.
4. `.env` or secrets are committed.
5. Live link is broken.
6. Backend health URL is missing.
7. Demo credentials do not work.
8. No testing evidence exists.
9. App only works with mock data but claims backend integration.
10. Student says “AI built it” but cannot explain decisions.
```

---

## Required final project checks

| Check | Pass condition |
|---|---|
| GitHub repo | Clean structure, public/accessible |
| README | Live links, demo credentials, features, setup |
| Frontend | Live URL loads |
| Backend | Health endpoint works |
| Auth | Register/login works |
| User flow | Main submission/order/booking works |
| Admin flow | Resource management and status update work |
| Authorization | Customer blocked from admin route/API |
| Database | Data persists |
| Mobile | Main pages usable |
| QA | Browser/API/authorization reports present |
| Security | No secrets committed |
| Deployment | Smoke test completed |
| Explanation | Student can explain architecture and one bug |

---

## Suggested interview questions

### General

1. What problem does this project solve?
2. Who are the users?
3. What are the main features?
4. What was out of scope?

### Frontend

1. How did you structure the frontend?
2. What reusable components did you create?
3. How did you handle loading/error/empty states?
4. How did you make it responsive?

### Backend

1. How did you structure the backend?
2. What are the main models?
3. How does the API flow from route to database?
4. How did you validate requests?

### Auth/security

1. How does login work?
2. How is the password protected?
3. How is admin access protected?
4. Why is frontend route protection not enough?

### Integration

1. How does frontend call backend?
2. How do you send the JWT token?
3. What integration bug did you face?
4. How did you debug CORS/API issues?

### AI usage

1. How did you use Antigravity?
2. What did Antigravity do well?
3. What did you manually review?
4. How did you avoid blindly accepting generated code?

---

## Module progress tracker

| Module | Evidence required | Status |
|---|---|---|
| Intro | Reflection | Pending |
| NotebookLM | Study guide/quiz/flashcards | Pending |
| Setup | Mini project + screenshots | Pending |
| Spec-first | Project docs | Pending |
| Architecture | Architecture docs | Pending |
| Skills | `SKILL.md` files | Pending |
| Figma-to-code | Design docs | Pending |
| Frontend | Pages/components/routes | Pending |
| Backend | APIs/models/auth | Pending |
| Integration | Full-stack flow | Pending |
| Testing | QA reports | Pending |
| Deployment | Live links/smoke test | Pending |
| Final assignment | Complete project | Pending |
| Portfolio | Case study/interview prep | Pending |
| Security | Security checklist/review | Pending |

---

## Feedback format

Use this format:

```md
# Mentor Feedback

## Overall verdict
Pass / Conditional pass / Needs major fixes

## Strong points
-

## Must-fix issues
1.
2.
3.

## Recommended improvements
-

## Questions student must answer
1.
2.
3.

## Final decision
-
```
