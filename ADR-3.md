# ADR 3 – Data Architecture (Separate Tenant Complaint Collections + Shared Users Collection)

## Context and problem statement
The system needs to organise complaint data clearly across multiple sectors (Bank, Airline, Telecom). The design must support filtering by tenant, assigning complaints to support engineers, and showing complaint status updates in real-time.

## Decision drivers

1) Clear separation of organisation data

2) Simple queries for help desk and support inbox

3) Reduce risk of cross-tenant data access

4) Match the system workflow (status + assignment + messages)

## Considered options

1) One complaints collection with a tenantId field and queries like where("tenantId","==",...)

2) Separate complaint collections per tenant (complaints_bank, complaints_airline, complaints_telecom)

3) Separate Firestore databases per tenant (very complex)

## Decision outcome
Separate complaint collections per tenant were used: complaints_bank, complaints_airline, and complaints_telecom, while user profiles are stored in a shared users collection. A helper function complaintsCollectionName(tenantId) selects the correct tenant collection.

## Consequences
Tenant separation becomes clearer and it is easier to query the correct data for each organisation. However, it increases repetition in rules and requires consistent handling across all tenant collections.

## Pros and cons of the options

* One complaints collection

Pros: Simple structure and fewer rules

Cons: Requires tenant filtering everywhere and careful rule conditions

* Separate collections (chosen)

Pros: Clear separation, simpler tenant queries, easier to explain in documentation

Cons: More repeated rules and code must choose correct collection

* Separate databases

Pros: Strong isolation

Cons: Too much complexity for this project
