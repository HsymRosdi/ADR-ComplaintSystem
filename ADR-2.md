ADR 2 – Security Architecture (RBAC + Tenant-Based Access via Firestore Rules)

Context and problem statement
The system stores sensitive complaint information. It must ensure that users can only access data they are allowed to see. For example, consumers should only see their own complaints, help desk should manage complaints for their organisation, and support engineers should only see tickets assigned to them.

Decision drivers

Protect sensitive complaint data

Prevent cross-tenant access (Bank vs Airline vs Telecom)

Enforce security even if the UI is changed

Use Firebase features properly

Considered options

Frontend-only security (hiding pages using React routing)

Database-level security using Firestore Security Rules

Backend-controlled security via a custom API server

Decision outcome
Security is enforced using Firestore Security Rules with role-based access control (RBAC) and tenant-based access control. The system reads each user’s role and tenant from users/{uid} and applies rules on complaint documents.

Consequences
Security is applied at the database level, meaning unauthorised users cannot access data even if they manipulate the UI. The downside is that rules can be harder to write and debug, and mistakes can block valid users if not tested properly.

Pros and cons of the options

Frontend-only security

Pros: Easy to implement

Cons: Not secure (users can bypass UI)

Firestore Rules (chosen)

Pros: Strong security enforced by Firebase

Cons: More complex and needs careful testing

Backend-controlled security

Pros: Centralised control

Cons: Requires extra server/API development