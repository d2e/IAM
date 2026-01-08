# Journey to be Expert in IAM

## Introduction

This guide provides a structured reading list for mastering IAM, OAuth tenant management, and Entitlement, with a specific focus on **Keycloak**. The recommendations are scored based on "Practical Impact" (how useful it is for implementation) and "Complexity" (how hard it is to digest).

## Recommended Reading Order

**Start Here** $\rightarrow$ **Foundational Concepts** $\rightarrow$ **Keycloak Specifics** $\rightarrow$ **Advanced Standards** $\rightarrow$ **Architectural Patterns**

---

## 1. Top Recommended Whitepapers & Guides

### A. The Foundation (Read First)

**Title:** NIST Special Publication 800-63C (Digital Identity Guidelines)

**Focus:** Federation and Assertions (The standard for how Identity Providers and Service Providers should talk).

**Why:** Before managing tenants, you must understand the "Federation Assurance Level" (FAL). It defines how secure your token passing needs to be.

**Key Takeaway:** Defines the rules for OIDC/SAML federation which is the backbone of multi-tenancy.

**Score:** 9/10 (Essential Theory).

### B. The Keycloak Bible (The Core)

**Title:** Keycloak Authorization Services Guide (Official Documentation)

**Focus:** Fine-grained entitlement management, UMA (User-Managed Access), and Policy Enforcement Points (PEP).

**Why:** This is the most "whitepaper-like" technical deep dive into how Keycloak handles entitlements (Permissions, Policies, Scopes) which is distinct from simple Role-Based Access Control (RBAC).

**Key Takeaway:** How to move authorization logic out of your code and into Keycloak.

**Score:** 10/10 (Critical for your specific request).

### C. The Architecture Strategy (The "How-To")

**Title:** "Multi-tenancy: Hub & Spoke vs. Single Org" (Concept from Okta/Auth0 Engineering Blogs)

**Focus:** Tenant Management Patterns.

**Why:** While vendor-specific, the concepts apply 100% to Keycloak. You need to decide: Do you create a Realm per Tenant (Keycloak standard) or One Realm with Groups (Logical separation)?

**Key Takeaway:** "Realm per Tenant" offers best isolation but highest resource cost.

**Score:** 8/10 (Architectural Strategy).

### D. The Advanced Standard (Read Last)

**Title:** User-Managed Access (UMA) 2.0 Profile of OAuth 2.0

**Focus:** Advanced Entitlement & Delegation.

**Why:** If your use case involves users sharing resources (e.g., "I want to give Bob read-access to my file"), this is the protocol Keycloak uses to implement it.

**Key Takeaway:** Decouples the Resource Server from the Authorization Server.

**Score:** 7/10 (High complexity, niche use case).

---

## 2. Scoring & Reading Order Matrix

| Order | Paper / Guide Title | Focus Area | Complexity | Practical Score |
|-------|-------------------|------------|------------|----------------|
| 1 | NIST SP 800-63C | Identity Standards | ⭐⭐⭐ | 9.0 |
| 2 | Keycloak Server Admin Guide (Realms) | Tenant Management | ⭐⭐ | 9.5 |
| 3 | Keycloak Authorization Services | Entitlement | ⭐⭐⭐⭐⭐ | 10.0 |
| 4 | OAuth 2.0 Threat Model (RFC 6819) | Security/Risk | ⭐⭐⭐⭐ | 8.5 |
| 5 | UMA 2.0 Grant for OAuth 2.0 | Deep Entitlement | ⭐⭐⭐⭐⭐ | 7.0 |

**Complexity:** ⭐ (Easy read) to ⭐⭐⭐⭐⭐ (Academic/Spec heavy).  
**Practical Score:** 1-10 (10 being "You need this to code/configure the solution").

---

## 3. Learning Path: From Zero to Architect

### Phase 1: Concepts & Multi-Tenancy (Week 1)

**Understand the "Realm" concept:** In Keycloak, a Realm is a tenant.

**Action:** Install Keycloak locally. Create two realms: Tenant-A and Tenant-B.

**Study OIDC & OAuth2:**
- **Read:** "The OAuth 2.0 Handbook".
- **Focus:** Differences between `client_credentials` (Service Accounts) and `authorization_code` (User Login).

### Phase 2: Entitlement & Authorization (Week 2)

**RBAC vs. ABAC:**
Learn how Keycloak Roles (RBAC) differ from Attributes (ABAC).

**Keycloak Authorization Services:**
- **Action:** Enable "Authorization" tab in a Keycloak Client.
- **Experiment:** Create a "Resource" (e.g., `/api/invoice`) and a "Policy" (e.g., Only users in Group 'Finance').
- **Test:** Use the Evaluate tool in Keycloak to see if User X can access Resource Y.

### Phase 3: Advanced Tenant Management (Week 3)

**Realm Management API:**
You cannot manually create realms for 1000 tenants. You must automate it.

**Action:** Write a script (Python/Bash) that calls Keycloak Admin API to:
- Create a new Realm.
- Create a Client.
- Set up Default Roles.

**Cross-Tenant Access:**
Research "Identity Brokering" (Tenant A users logging into Tenant B's app).

---

## 4. Summary Comparison Table

| Feature | RBAC (Role Based) | ABAC (Attribute Based) | Keycloak AuthZ Services |
|---------|------------------|----------------------|------------------------|
| **Primary Concept** | "User is an Admin" | "User is > 18 years old" | "User can view Resource X between 9-5 PM" |
| **Granularity** | Coarse (Low) | Medium | Very High |
| **Tenant Isolation** | Easy (Roles per Realm) | Complex (Attributes per user) | High (Policies per Resource) |
| **Performance** | Fast | Fast | Slower (Requires Policy Evaluation) |
| **Best Use Case** | Menu visibility, basic page access | Data filtering, regional access | Entitlement, Document sharing, API security |
| **Keycloak Capability** | Native / Default | Native (Mappers) | Requires "Authorization" feature enabled |

---

## Progress Tracking

This repository will track your progress through the learning phases:

### Phase 1: Concepts & Multi-Tenancy
- [ ] Install Keycloak locally
- [ ] Create multiple realms (Tenant-A, Tenant-B)
- [ ] Understand OAuth 2.0 flows (client_credentials vs authorization_code)
- [ ] Read NIST SP 800-63C

### Phase 2: Entitlement & Authorization  
- [ ] Study RBAC vs ABAC concepts
- [ ] Enable Authorization Services in Keycloak
- [ ] Create Resources and Policies
- [ ] Test authorization with Evaluate tool
- [ ] Read Keycloak Authorization Services Guide

### Phase 3: Advanced Tenant Management
- [ ] Learn Keycloak Admin API
- [ ] Automate realm creation with scripts
- [ ] Implement identity brokering
- [ ] Study UMA 2.0 for advanced entitlements

---

## Key Resources

### Official Documentation
- [Keycloak Authorization Services Guide](https://keycloak.org/docs/latest/authorization_services/)
- [NIST SP 800-63C Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63c.html)
- [OAuth 2.0 RFC 6749](https://tools.ietf.org/html/rfc6749)
- [UMA 2.0 Profile](https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html)

### Implementation Examples
- Code examples and scripts will be added as you progress
- Keycloak configuration templates
- Multi-tenant architecture patterns

---

*Start your Keycloak-focused IAM expertise journey with Phase 1, following the structured learning path above.*