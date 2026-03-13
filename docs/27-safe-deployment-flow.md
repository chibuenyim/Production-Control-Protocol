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