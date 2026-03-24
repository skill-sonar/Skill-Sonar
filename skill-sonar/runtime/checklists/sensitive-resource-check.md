# Sensitive Resource Check

Catalog of sensitive targets. Any interaction with these MUST increase scrutiny.

## Categories

| Category                      | Examples                                                         | Min Risk |
| ----------------------------- | ---------------------------------------------------------------- | -------- |
| **Credentials / Secrets**     | API keys, tokens, passwords, certificates, SSH keys              | R3       |
| **Private Files**             | `.env`, config with secrets, private keys, auth files            | R3       |
| **Personal Data**             | PII, emails, addresses, financial info, health data              | R2+      |
| **System Configuration**      | OS config, service configs, DNS, firewall rules                  | R3       |
| **Persistent Memory**         | Long-term agent memory, stored preferences, stored policies      | R2+      |
| **Network / External**        | Outbound API calls, email sending, webhook triggers, DNS queries | R3       |
| **Deletion Targets**          | Any file, record, or resource being deleted                      | R3       |
| **Financial / Transactional** | Payment APIs, billing, purchases, transfers                      | R3       |
| **Privileged Execution**      | Shell commands, code execution, admin operations                 | R3       |
| **Production Resources**      | Live databases, deployed services, user-facing systems           | R3       |

## Rules

- When a sensitive resource is detected, raise the risk level to at least the minimum shown.
- Credential access MUST trigger `require_user_confirmation` unless explicitly pre-authorized by P2.
- Deletion of any sensitive resource MUST trigger `require_user_confirmation`.
- External data transmission involving sensitive content MUST trigger `require_user_confirmation`.
- When uncertain whether a resource is sensitive, treat it as sensitive.
