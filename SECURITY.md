# Security Policy & Sensitive Data Management

This document outlines the security practices for this repository to ensure sensitive information is protected from accidental exposure.

## What Information Must Never Be Pushed

The following types of sensitive data should **never** be committed to version control:
- **API Keys & Tokens**: e.g., AWS, OpenAI, Stripe, GitHub personal access tokens.
- **Private Keys**: e.g., SSH keys, SSL/TLS certificates (`.pem`, `.key` files).
- **Database Credentials**: e.g., usernames, passwords, connection strings.
- **Environment Variables**: Local configuration files like `.env`.
- **Personal Identifiable Information (PII)**: User data, emails, or phone numbers.

## Research Findings

### Common Vulnerabilities
Secrets are often exposed through:
- **Hardcoding**: Embedding keys directly in source code.
- **Accidental Commits**: Forgetting to exclude sensitive files like `.env`.
- **Commit History**: Sensitive data remains in the Git history even if the file is deleted in a later commit.
- **CI/CD Logs**: Secrets appearing in build or deployment logs.

### Risks Involved
- **Unauthorized Access**: Attackers can use leaked keys to access cloud resources or databases.
- **Data Breaches**: Exposure of user data leading to legal and financial consequences.
- **Financial Loss**: Unauthorized usage of paid APIs (e.g., cloud billing).
- **Reputational Damage**: Loss of trust from users and partners.

### Repository Types
- **Public Repository**: Visible to everyone on the internet. High risk for secret exposure.
- **Private Repository**: Restricted to authorized users. More secure, but still requires best practices (MFA, limited access).

## Best Practices

### Using Environment Variables
- Store sensitive configuration in a `.env` file locally.
- Use a library like `dotenv` to load these variables into your application.
- **Always** add `.env` to your `.gitignore` file.
- Distribute a `.env.example` file with placeholder values to show what variables are needed without sharing the actual secrets.

### Pre-commit Checks
- Use tools like `git-secrets` or `detect-secrets` to scan for patterns before committing.
- Manually review `git diff --cached` before every commit.
