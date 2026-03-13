# 23. Database Access Protection

AI systems must not have write access to production databases.

Architecture:

```
Primary Database (write)

       │

Read Replica (AI read-only)
```