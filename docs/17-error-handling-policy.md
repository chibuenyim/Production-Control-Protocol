# 17. Error Handling Policy

Generic errors are strictly prohibited.

Errors must always be:

• Specific
• Actionable
• Helpful
• Context-aware

Bad:

```
Something went wrong
```

Good:

```
Payment failed: Your card was declined by the issuing bank.

Please try another card or contact your bank.

Error Code: PAY-102
```