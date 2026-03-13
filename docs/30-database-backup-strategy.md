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