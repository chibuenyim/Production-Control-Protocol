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