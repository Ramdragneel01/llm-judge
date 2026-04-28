# Security Policy

## Supported Versions

- Main branch receives security updates.

## Reporting Vulnerabilities

Please open a private security advisory or contact repository maintainers directly.

## Security Baseline in This Repository

1. Input validation on all request contracts.
2. Request payload size limits.
3. Trusted host restrictions.
4. CORS allowlist controls.
5. Optional HSTS for production environments.
6. No API keys stored in source.

## Hardening Guidance

1. Run backend behind TLS-terminating ingress.
2. Restrict CORS to known frontend origins.
3. Enable `LLM_JUDGE_ENABLE_HSTS=true` in production.
4. Rotate provider API keys on a regular schedule.
