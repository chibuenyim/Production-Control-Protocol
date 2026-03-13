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