# 🚀 MASTER ENGINEERING & AI OPERATIONS PROTOCOL

```
=========================
ALWAYS LAST CONTROL
=========================
```

This document defines the **mandatory operating framework** for:

* Engineering work
* AI-assisted development
* Deployment operations
* Production protection
* System verification

The protocol ensures that all system changes are:

• Logical
• Safe
• Controlled
• Verifiable
• Reversible

**No step may be skipped.**

---

# 1. Mandatory Engineering Workflow

Every task must follow this exact sequence:

1. Investigation
2. Root Cause Analysis
3. End-to-End Fix Plan
4. Approval Gate
5. Implementation
6. Implementation Recap
7. Deployment Approval
8. Deployment
9. Human User Simulation Verification

Skipping steps is **not allowed**.

---

# 2. Investigation Phase

Before any change is made:

• Study the issue thoroughly
• Inspect logs and monitoring data
• Review database state
• Trace the code execution path
• Confirm the issue is reproducible

No fix should be attempted without **complete understanding of the problem**.

---

# 3. Root Cause Analysis

Identify the **actual root cause**, not the symptom.

Root cause documentation must include:

Problem
Root Cause
Affected Components
System Impact

Example:

```
Problem: Checkout fails when users attempt payment

Root Cause: Webhook signature verification mismatch

Affected Components:
payment-service
webhook-handler

Impact:
Users cannot complete payments
```

---

# 4. End-to-End Fix Plan

Before coding begins, a complete fix plan must be presented including:

• Root cause explanation
• Proposed solution
• Files to modify
• Affected systems
• Database impact
• UX impact
• Risks
• Rollback strategy

The plan must be **reviewed and approved before implementation begins**.

---

# 5. Approval Gate

Implementation may only begin when:

• The fix plan has been reviewed
• Explicit approval has been given

This prevents uncontrolled code changes.

---

# 6. Implementation Phase

After approval:

• Implement the solution
• Follow clean architecture principles
• Avoid shortcuts or temporary fixes

All changes must prioritize:

• Stability
• Maintainability
• Scalability
• User experience

---

# 7. Implementation Recap

After implementation is completed, provide a recap including:

Code Changes
Files modified or added

Logic Changes
Updated system behavior

Database Changes
Schema updates or migrations

Configuration Changes
Environment variables or configuration updates

Risk Notes
Potential side effects requiring monitoring

Deployment **must not occur before the recap is reviewed**.

---

# 8. Deployment Approval

Deployment may only occur **after recap approval**.

---

# 9. Deployment Strategy

Production deployments must ensure:

• Zero downtime
• Full system backup before deployment
• Zero user data loss
• Deployment verification

---

# 10. Approved Deployment Methods

Approved methods:

• rsync
• git pull on server
• tarball deployment

Deployment must guarantee:

• full file integrity
• build parity with local version
• rollback capability

---

# 11. Automated Server Control

Use **Paramiko** for:

• automated SSH authentication
• remote command execution
• deployment scripting
• automated verification

---

# 12. Secure Deployment Process

Deployment sequence:

1. Upload tarball segments
2. Reassemble archive on server
3. Extract files
4. Verify file integrity
5. Compare with local build output
6. Perform intelligent cleanup
7. Restart services if required

Goal:

```
100% deployment parity
zero file loss
```

---

# 13. Required Deployment Files

Every deployment must include the full application stack.

Backend

• API routes
• services
• middleware
• utilities

Frontend

• frontend source files
• compiled production build

Configuration

• next.config
• tailwind.config
• postcss.config
• environment templates
• build configuration files

Assets

• public directory
• images
• fonts
• static assets

Database Layer

• Prisma schema
• migrations
• Prisma client

---

# 14. Database Protection Rules

Database operations are **high-risk**.

The following command must **never run without explicit approval**:

```
prisma db push --force-reset
```

This command can destroy production data.

Safe migration method:

```
prisma migrate deploy
```

---

# 15. Human User Simulation (Mandatory)

After deployment, the system must be tested **exactly like a real user**.

Verification includes:

Visual Page Checks
Navigate pages and verify UI rendering.

Browser Console Inspection
Inspect:

• JavaScript errors
• network request failures
• runtime exceptions

Functional Testing
Verify:

• login
• dashboards
• forms
• payments
• admin functionality

Every page must be **fully error-free**.

---

# 16. Test Credentials

For deep verification retrieve credentials from:

```
C:\Users\chibu\Claude-Projects\Key\live keys.md
```

Test both:

• User account
• Admin account

---

# 17. Error Handling Policy

Generic errors are strictly prohibited.

Errors must always be:

• Specific
• Actionable
• Helpful
• Context-aware

Bad:

```
Something went wrong
```

Good:

```
Payment failed: Your card was declined by the issuing bank.

Please try another card or contact your bank.

Error Code: PAY-102
```

---

# 18. Database-Driven Error System

Error messages should be:

• stored in the database
• customizable by administrators
• dynamically rendered

Benefits:

• localization
• customizable messaging
• easier debugging

---

# 19. Anti-Hardcoding Policy

Hardcoding creates fragile systems.

Never hardcode:

• API URLs
• error messages
• feature flags
• roles or permissions
• environment values
• system limits
• file paths

Instead use:

• environment variables
• database configuration
• centralized config files
• admin settings
• feature flags

---

# 20. Build & Caching Policy

Every new build must generate **new content hashes** when files change.

Static hashed assets:

Cache duration

```
1 year
```

Non-hashed assets:

```
24–48 hours
```

The build system must:

• detect source changes
• regenerate bundles
• invalidate caches properly

---

# 21. AI Development Safety Rules

AI agents must never:

• invent APIs
• fabricate database fields
• guess environment variables
• assume system behavior

If uncertain, the AI must:

• inspect the code
• request clarification
• verify assumptions

---

# 22. Environment Isolation

Production must be isolated from development.

Required environments:

```
local
development
staging
production
```

Deployment flow:

```
Local → Development → Staging → Production
```

AI must **never deploy directly to production**.

---

# 23. Database Access Protection

AI systems must not have write access to production databases.

Architecture:

```
Primary Database (write)

       │

Read Replica (AI read-only)
```

---

# 24. Secrets Protection

Production secrets must never exist in source code.

Secrets must be stored in secure secret managers and injected at runtime.

---

# 25. Feature Flag Safety

All new features must deploy **disabled by default**.

Example:

```
feature_new_dashboard = false
feature_new_payment_flow = false
```

Features are enabled gradually after verification.

---

# 26. Versioned Release Deployment

Deployments must use versioned releases.

Example structure:

```
/var/www/app

/releases
/shared
/current
```

Active version:

```
current → /releases/release-003
```

The web server always serves from:

```
/var/www/app/current
```

---

# 27. Safe Deployment Flow

Deployment steps:

1. Upload new release
2. Extract to releases folder
3. Install dependencies
4. Build application
5. Run migrations safely
6. Verify build integrity
7. Switch symlink

```
current → new-release
```

Switch time: milliseconds.

Users experience **zero downtime**.

---

# 28. Instant Rollback

Rollback command:

```
ln -sfn /var/www/app/releases/previous-release /var/www/app/current
```

Rollback time:

```
5–10 seconds
```

---

# 29. Automated Health Checks

After deployment run:

```
GET /
GET /api/health
GET /login
GET /dashboard
```

If any fail:

```
automatic rollback
```

---

# 30. Database Backup Strategy

Before every deployment:

```
pg_dump database > backup.sql
```

Store backups with timestamps.

Example:

```
/backups
2026-03-13-predeploy.sql
```

---

# 31. Deployment Logging

Each deployment must generate a record:

Deployment ID
Timestamp
Commit Hash
Status
Rollback Availability

Logs stored in:

```
/deployments/logs
```

---

# 32. Emergency Kill Switch

If a critical failure occurs:

```
ENABLE_MAINTENANCE_MODE=true
```

The server redirects all requests to a maintenance page.

---

# 33. Final System Principles

All system changes must prioritize:

• reliability
• transparency
• maintainability
• user experience

The system must always remain:

• logical
• stable
• configurable
• scalable
• user-friendly

And must never include:

• generic errors
• hardcoded logic
• unsafe deployments

---

✅ **FINAL RESULT**

This protocol creates a system with:

• controlled engineering workflow
• safe AI-assisted development
• zero-downtime deployment
• instant rollback capability
• strong production protection
• predictable system behavior

This framework is suitable for **serious SaaS production environments** and scales safely with AI-assisted engineering.