---
name: security-audit
description: Use when reviewing code that handles auth, payments, user data, or external APIs. Security-focused checklist.
---

## When to activate

- Code touches authentication or authorization (login, tokens, sessions, guards)
- Code handles payments or financial data
- Code processes user input that reaches a database or external API
- Code exposes new API endpoints
- Code handles file uploads or external file access

## Checklist

### Authentication & Authorization
- [ ] Auth guards/middleware on all protected routes
- [ ] Token validation (expiry, signature, audience)
- [ ] Role/permission checks match business rules
- [ ] No privilege escalation paths (user A accessing user B's data)
- [ ] Session management (invalidation, rotation)

### Input Validation
- [ ] All user inputs validated and sanitized
- [ ] SQL injection prevented (parameterized queries / ORM)
- [ ] XSS prevented (output encoding, CSP headers)
- [ ] Command injection prevented (no shell interpolation of user input)
- [ ] Path traversal prevented (no user-controlled file paths)

### Data Protection
- [ ] No secrets in code (API keys, passwords, tokens)
- [ ] Sensitive data not logged (passwords, tokens, PII)
- [ ] CORS configured correctly (not wildcard on authenticated endpoints)
- [ ] Rate limiting on public endpoints
- [ ] HTTPS enforced

### API Security
- [ ] Request size limits configured
- [ ] Webhook signatures validated
- [ ] External API calls use timeouts
- [ ] Error messages don't leak internals (stack traces, DB structure)

## Output

For each finding: `file:line` — vulnerability type — impact — recommended fix.
Classify as CRITICAL (exploitable now) or IMPORTANT (defense gap).
