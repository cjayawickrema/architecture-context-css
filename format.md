# [Standard Title]

## 1. Threat Context & Security Objective
The concrete security risk, exploit vector, or regulatory exposure this standard mitigates (e.g., unauthorized data exfiltration, lateral movement, credential harvesting).

## 2. Normative Guardrails (Hard Rules)
Absolute requirements phrased unambiguously:
* **Mandatory (Non-Negotiable):** Hard controls that must never be bypassed.
* **Conditional:** Requirements triggered only under specific criteria (e.g., handling PCI-DSS data, exposing external public endpoints).

## 3. Boundary & Scope Enforcement
* **Target Workloads:** Explicit systems, runtimes, and layers in scope (e.g., persistent data stores, API ingress, service mesh).
* **Exemptions:** Strictly defined scenarios where the rule does not apply (e.g., ephemeral local test containers, mock services).

## 4. Declarative Enforcement Criteria
Specific state rules that automated agents, linters, or IaC compilers must assert:
* Parameters that must evaluate to `true`/`enabled`.
* Configuration values that must match approved enterprise vaults, KMS keys, or identity brokers.
* Network postures, protocols, and minimum cryptographic ciphers required.

## 5. Explicitly Prohibited Anti-Patterns
Direct anti-patterns and unsafe configurations that constitute an immediate security block (e.g., plaintext credentials, disabled TLS verification, unencrypted storage fallbacks).