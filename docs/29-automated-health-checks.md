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