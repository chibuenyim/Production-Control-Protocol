# 25. Feature Flag Safety

All new features must deploy **disabled by default**.

Example:

```
feature_new_dashboard = false
feature_new_payment_flow = false
```

Features are enabled gradually after verification.