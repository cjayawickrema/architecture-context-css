# Relational Database Encryption at Rest

## 1. Threat Context & Security Objective
Mitigate the risk of unauthorized data exposure, physical media theft, and snapshot exfiltration. Unencrypted persistent storage volumes, automated snapshots, and transaction log archives expose sensitive enterprise data to out-of-band access if underlying host infrastructure or storage volumes are compromised or improperly decoupled.

## 2. Normative Guardrails (Hard Rules)
* **Mandatory (Non-Negotiable):** All managed relational database instances must enforce storage volume encryption at rest using customer-managed encryption keys (CMEK). Default, platform-managed provider keys are strictly prohibited.
* **Mandatory (Non-Negotiable):** Storage encryption must be enabled at instance creation time. Provisioning unencrypted instances with the intention of encrypting retroactively is prohibited.
* **Mandatory (Non-Negotiable):** Automated backups, point-in-time recovery logs, and manual snapshots must inherit the same customer-managed key configuration as the source instance.
* **Mandatory (Non-Negotiable):** Read replicas, standby instances, and cross-region replicas must be encrypted at rest using approved customer-managed keys authorized for their specific deployment regions.

## 3. Boundary & Scope Enforcement
* **Target Workloads:** All relational database instances (e.g., PostgreSQL, Aurora, MySQL) across development, test, staging, and production environments, including primary volumes, temporary tablespaces, and backup stores.
* **Exemptions:** Ephemeral, containerized databases executed strictly within isolated, local CI integration test runs (e.g., Testcontainers) where state is discarded upon process exit.

## 4. Declarative Enforcement Criteria
When automated agents, linters, or infrastructure-as-code manifests evaluate database configurations:
* Storage encryption enablement parameters (such as `storage_encrypted`) must evaluate to `true`.
* The key identifier attribute (such as `kms_key_id`) must bind directly to an approved enterprise customer-managed key reference (e.g., KMS Key ARN) and must not evaluate to `null`, `default`, or empty strings.
* Automated snapshot and replication configuration blocks must inherit the explicit encryption parameters from the parent cluster or instance definition.

## 5. Explicitly Prohibited Anti-Patterns
* Defining database resources with storage encryption explicitly disabled (`storage_encrypted = false`) or omitting the encryption attribute entirely.
* Enabling storage encryption while leaving the key identifier blank, which defaults volume encryption to cloud-provider-managed shared keys.
* Creating read replicas, database clones, or restore tasks that map to unencrypted targets or fallback storage classes.