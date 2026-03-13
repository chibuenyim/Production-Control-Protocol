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