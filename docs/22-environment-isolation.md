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