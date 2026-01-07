ADR 1 – Architecture Style (Serverless Web Architecture)

Context and problem statement
The Complaint Management System needs to support multiple user roles (consumer, help desk, support), user login, complaint submission, and live status updates. The project also has limited time, so building and deploying a full backend server would make the system more complex.

Decision drivers

Simple architecture that is quick to implement

Low maintenance (no server management)

Works well with real-time updates

Suitable for coursework scope and timeframe

Considered options

Traditional 3-tier architecture: React frontend + Node/Express backend + database

Serverless architecture: React frontend + Firebase services (Auth + Firestore)

Hybrid: React frontend + Firebase + optional API using Cloud Functions (future)

Decision outcome
A serverless architecture was chosen using React (Vite) for the frontend and Firebase (Auth + Firestore) for backend services. Cloud Functions can be treated as an API layer in the design, but the core prototype works using Firebase SDK.

Consequences
The system is easier to build and deploy because there is no backend server to maintain. Real-time updates are supported by Firestore listeners. However, security must be enforced through Firestore Security Rules because the client connects directly to the database.

Pros and cons of the options

Traditional 3-tier

Pros: Full control of business logic, clear separation

Cons: More time to build and maintain, extra deployment work

Serverless (chosen)

Pros: Fast development, scalable, less maintenance

Cons: Requires careful security rules and structured data access

Hybrid

Pros: More control if needed later

Cons: Adds complexity for a coursework prototype