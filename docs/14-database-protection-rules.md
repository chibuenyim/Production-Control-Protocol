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