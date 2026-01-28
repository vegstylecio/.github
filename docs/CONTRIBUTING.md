# Contributing to VegStyle CIO

First off, thank you for considering contributing to VegStyle. 
VegStyle is not just software; it is a mission to accelerate animal advocacy through accessible, free, and secure technology.

This document serves as the global contribution hub for all repositories under the [VegStyle CIO Organization](https://github.com/vegstylecio). 

## 📜 Code of Conduct

We are committed to fostering a welcoming and respectful community. We expect all contributors to uphold a high standard of professional and ethical conduct. This includes, but is not limited to:

* **Respectful Dialogue:** Engage in constructive discussions. Disagreements are opportunities for growth, not conflict. Focus on ideas, not individuals.
* **Empathy and Understanding:** Strive to understand different perspectives and experiences. Provide and accept feedback gracefully.
* **Inclusive Language:** Use inclusive language that respects all individuals, regardless of background, identity, or **species**. We advocate for the compassionate treatment of all sentient beings and expect language that reflects this understanding.
* **Harassment-Free Environment:** We do not tolerate harassment in any form. This includes offensive comments, personal attacks, or discriminatory behavior.

Violations of the Code of Conduct will result in appropriate action, as determined by the project maintainers.

## 🏗️ Engineering Culture & Standards

We strive for enterprise-grade quality in an open-source non-profit context. All contributors are expected to align with our core engineering pillars.

### 1. Architecture (Clean Architecture)
We follow the **Clean Architecture** principles (by Robert C. Martin).
* **Dependency Rule:** Dependencies must point inwards. The domain layer must never depend on the data or presentation layers.
* **Separation of Concerns:** Business logic is isolated from UI, Database, and Frameworks.
* **Goal:** Framework independence, testability, and UI independence.

### 2. Test-Driven Development (TDD)
We treat tests as a first-class citizen.
* **Red-Green-Refactor:** Ideally, write the failing test before the implementation.
* **Coverage:** We aim for high coverage, especially in the Domain and Data layers.
* **Regressions:** No code is merged if it breaks existing tests.

### 3. Security First
* **No Secrets:** Never commit API keys or credentials.
* **Dependencies:** Keep dependencies updated and audited.
* **Privacy:** Design features with user privacy and data minimization in mind.

---

## 🚀 Development Workflow

To maintain stability across our repositories, we enforce a strict **Gitflow-inspired** workflow with **Branch Protection Rules**.

👉 **You MUST read our [Internal Development Workflow Guide](WORKFLOW.md) before opening any Pull Request.**

Key Rules:
* Base branch for PRs is always `dev`.
* **Linear History** is enforced (Squash/Rebase).
* **Signed Commits** are required.
* **Conventional Commits** format is mandatory for commit messages.

---

## ⚖️ Licensing & Copyright

* **License:** All our projects are licensed under the **GNU Affero General Public License v3.0 (AGPL v3)**.
* **Copyright:** Contributors retain ownership of their code but grant VegStyle CIO a perpetual license to use it under AGPL v3.
* **Headers:** All new files must include the standard project copyright header.

---

## 📞 Getting Help

* **Security Vulnerabilities:** Do NOT open an issue. See [SECURITY.md](../SECURITY.md).
* **General Questions:** Open a Discussion in the relevant repository.
* **Private Inquiries:** Contact `info@vegstyle.org.uk`.

Thank you for coding with compassion. 🌱
