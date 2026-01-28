# Internal Development Workflow Guide

This document outlines our internal development process, branching strategy, commit and pull request guidelines, release management, and the utilization of GitHub tools for our project. It aims to provide a comprehensive, easy-to-follow, and direct procedure for all team members.

-----

## 1\. Branching Strategy

We adopt a streamlined Gitflow-inspired branching model, emphasizing stability and traceability.

### The `main` Branch

  * **Purpose:** Contains only production-ready, stable, and thoroughly tested code. It represents the "live" version of the application.
  * **Protection:** Extremely protected. No direct pushes are allowed. All merges must occur via Pull Requests from `dev` (for new releases) or from hotfix branches (for urgent corrections).
  * **History:** Must maintain a linear history.

### The `dev` Branch

  * **Purpose:** The primary development and staging branch. All new features and bug fixes (excluding urgent hotfixes) converge here. It is the candidate for the next release.
  * **Synchronization:** Must be kept consistently updated with `main` (especially after hotfixes on `main` or new releases) to prevent divergences and conflicts. This is typically done by merging `main` into `dev` periodically.
  * **Protection:** Protected. No direct pushes are allowed. All merges must occur via Pull Requests from feature branches.
  * **History:** Must maintain a linear history.

### Feature Branches

  * **Naming Convention:** `feature/<feature-name>` (e.g., `feature/login-screen`) or `bugfix/<bug-description>` (e.g., `bugfix/price-calc-error`).
  * **Purpose:** Dedicated to the development of single functionalities or specific bug fixes. Each feature branch should resolve one problem or implement one feature.
  * **Origin:** Always create a feature branch from the latest **`dev`** branch.
  * **Destination:** Pull Requests from feature branches are always targeting **`dev`**.
  * **Lifespan:** Short-lived. Merge as soon as the feature is complete, tested, and reviewed.

### Release Branches

  * **Naming Convention:** `release/vX.Y.Z` (e.g., `release/v1.0.0`).
  * **Purpose:** Preparation for an upcoming release. It contains stable code derived from a tested beta tag on the `dev` branch. It allows `dev` to continue development of new features while the release is finalized.
  * **Origin:** Always create a release branch from the **specific commit of the final tested beta tag** on the `dev` branch.
  * **Destination:** Pull Requests from release branches are always targeting **`main`**. After merging into `main`, the release branch must also be merged back into **`dev`** to incorporate any last-minute fixes made during the release stabilization.
  * **Lifespan:** Short-lived. It is deleted after successfully merging into `main` and `dev`.

### Hotfix Branches

  * **Naming Convention:** `hotfix/<issue-description>` (e.g., `hotfix/prod-auth-error`).
  * **Purpose:** Urgent corrections for critical bugs found in production (`main`). The primary goal is to fix the production issue as quickly as possible.
  * **Origin:** Always create a hotfix branch from the **latest `main` branch**. This ensures the fix targets the exact code currently in production.
  * **Destination:**
    1.  First Pull Request: From `hotfix/<name>` to **`main`** (to deploy the urgent correction to production).
    2.  Second Pull Request: From `hotfix/<name>` to **`dev`** (to ensure the fix is also integrated into the ongoing development for future releases).
  * **Lifespan:** Very short-lived. Deleted after merging into `main` and `dev`.

-----

## 2\. Commit Guidelines

Maintaining a clean, readable, and meaningful Git history is crucial for collaboration and long-term code maintenance.

### Commit Message Standard

Each commit message should follow a clear standard:

  * **Concise Subject Line:** Maximum 50-72 characters, briefly describing the change. Start with an imperative verb (e.g., "Fix: Login bug", "Feat: Implement authentication", "Refactor: Duplicate code").
  * **Detailed Body (Optional):** A blank line, followed by a longer paragraph explaining the "why" of the change, its context, and its impact.
  * **Issue Reference:** If the commit resolves an issue, include `Fixes #<issue-number>` or `Closes #<issue-number>` to automatically close it upon merge.

### Linear History Requirement

  * All `dev` and `main` branches must maintain a **linear Git history**. This means we will avoid traditional merge commits which create non-linear "bubbles" in the history.
  * We will use **Squash Merge** or **Rebase Merge** to integrate Pull Requests into `dev` and `main`.

-----

## 3\. Pull Request (PR) Process

Pull Requests are the gateway for introducing code into the main branches, ensuring review, testing, and quality.

### PR from Feature to `dev`

  * **Origin:** `feature/<feature-name>` or `bugfix/<bug-name>`
  * **Destination:** `dev`
  * **Requirements:**
      * All tests (unit, widget, integration) must pass.
      * Code must be formatted (`flutter format .`) and analyzed (`flutter analyze`).
      * Clear PR description, with screenshots/videos if relevant.
      * Requires approval from at least one other team member.
  * **Merge Type:** Use **Squash Merge** (preferred for single features) or **Rebase Merge**.

### PR for Release (`release/vX.Y.Z` to `main`)

  * **Origin:** `release/vX.Y.Z` (the specific release branch created from the final tested beta tag).
  * **Destination:** `main`
  * **Requirements:**
      * All `dev` tests (and comprehensive beta tests) must have passed.
      * Clear release description outlining the new features and major bug fixes.
      * Requires final approval from relevant maintainers/leads.
  * **Merge Type:** Use **Squash Merge** or **Rebase Merge**.

### PR for Hotfix (`hotfix/<name>` to `main` then `dev`)

1.  **PR to `main` (Priority for Production Fix):**
      * **Origin:** `hotfix/<issue-description>`
      * **Destination:** `main`
      * **Purpose:** To quickly deploy the critical fix to the production environment.
      * **Requirements:** Rapid, targeted tests on the hotfix branch to verify the fix. Maintainer approval.
      * **Merge Type:** Squash Merge or Rebase Merge.
2.  **PR to `dev` (Backporting the Fix):**
      * **Origin:** `hotfix/<issue-description>`
      * **Destination:** `dev`
      * **Purpose:** To ensure the critical fix is also included in the `dev` branch, preventing the bug from resurfacing in future releases. This step is typically performed *after* the hotfix has been successfully merged and deployed to `main`.
      * **Requirements:** Verify compatibility with the latest `dev` code; all tests on `dev` should pass.
      * **Merge Type:** Squash Merge or Rebase Merge.

### Merge Types

  * **Squash Merge:** Combines all commits from the PR into a *single* meaningful commit on the destination branch. This is ideal for distinct features/bug fixes, keeping the main branches' history clean.
  * **Rebase Merge:** Reapplies the individual commits of the PR onto the destination branch's tip, as if they were developed directly on it. This maintains commit granularity while ensuring a linear history.
  * **Avoid Traditional Merge Commits:** These create a non-linear history and are explicitly not permitted on `main` or `dev`.

-----

## 4\. Release Management and Tagging

The release process is structured to ensure maximum stability in production and clear versioning.

### Release Cycle

1.  **Development on `dev`:** All new features and regular bug fixes are developed on feature branches and merged into `dev` via PRs.
2.  **Beta Preparation:** Once `dev` contains the features targeted for the next release and is deemed stable enough for initial testing.
3.  **Beta Tag Creation:** Create an annotated tag (e.g., `v1.0.0-beta.1`) on the **`dev` branch** to specifically identify this version for beta testing.
    ```bash
    git checkout dev
    git pull origin dev # Ensure local dev is up-to-date
    git tag -a v1.0.0-beta.1 -m "Release Candidate 1 for v1.0.0"
    git push origin v1.0.0-beta.1
    ```
4.  **Beta Testing:** Deploy and thoroughly test the build generated from this tag in a beta environment. Collect feedback and bug reports.
5.  **Beta Bug Fixes:** Any bugs found during beta testing must be resolved on new bugfix branches (created from `dev`) and merged back into `dev` (via PR). After fixes, create a new beta tag (`v1.0.0-beta.2`) and repeat the testing process until the version is stable.
6.  **Release Branch Creation:** Once the final beta version (e.g., `v1.0.0-beta.N`) is deemed stable and ready for production, create a dedicated **release branch** from that specific tag's commit.
    ```bash
    git fetch origin # Ensure all remote branches and tags are fetched
    git checkout -b release/v1.0.0 v1.0.0-beta.N
    git push -u origin release/v1.0.0
    ```
7.  **PR from Release to `main`:** Open a Pull Request from `release/v1.0.0` to **`main`**. This guarantees that only the code proven stable in beta testing is merged into production.
8.  **Merge into `main`:** Complete the merge of the PR (Squash or Rebase).
9.  **Official Tag Creation:** Create an official annotated tag (`v1.0.0`) on the **`main` branch** immediately after the successful merge.
    ```bash
    git checkout main
    git pull origin main # Ensure local main has the latest merge commit
    git tag -a v1.0.0 -m "Official Release v1.0.0"
    git push origin v1.0.0
    ```
10. **Merge Release Branch into `dev`:** If any last-minute hotfixes or changes were applied directly to the release branch (which should be avoided if possible but sometimes necessary), merge `release/v1.0.0` back into `dev` (via a PR from `release/v1.0.0` -\> `dev`). This ensures `dev` is fully synchronized with all changes that went into production.

### Tagging

* **Beta/Release Candidate Tags:** Used on `dev` to identify versions under test (e.g., `v1.0.0-beta.1`, `v1.0.0-rc.1`).
* **Official Release Tags:** Used on `main` to mark versions released to production (e.g., `v1.0.0`, `v1.0.1`).
* **Naming & Versioning:** All tags must strictly adhere to [Semantic Versioning (SemVer)](https://semver.org/):
* **Major (`X`.y.z):** Increment when you make incompatible API changes (**Breaking Changes**).
* **Minor (x.`Y`.z):** Increment when you add functionality in a backward-compatible manner (**New Features**).
* **Patch (x.y.`Z`):** Increment when you make backward-compatible bug fixes.

-----

## 5\. GitHub Tool Usage

We leverage native GitHub features to optimize our workflow and enhance collaboration.

### GitHub Projects

We utilize GitHub Projects (Boards) for:

  * **Roadmap Management:** Visualizing the progress of long-term epics and features.
  * **Bug Tracking Kanban:** Managing the flow of bug fixes (To Do, In Progress, Review, Done).
  * **Cross-Repository Tracking:** If we have separate backend repositories, we can link frontend and backend Issues to a single board for a holistic view of the work.
  * **Issue Triage:** Prioritizing and assigning tasks, ensuring clarity on who is working on what.

### GitHub Discussions

Discussions are the preferred forum for:

  * **Ideation and Brainstorming:** Proposing new ideas for features or architectural changes before they become formal Issues.
  * **Questions and Answers (Q\&A):** Asking general questions about the project, architecture, or workflow.
  * **General Feedback:** Gathering broad feedback on the project's direction.
  * **Announcements:** Sharing important updates with the team and wider community.

-----

## 6\. Branch Protection (GitHub Settings)

The following settings are applied to the `main` and `dev` branches to guarantee their stability and quality. These are configured in `Settings` \> `Branches` \> `Branch protection rules` on GitHub.

  * **For `main` and `dev` (Applied to their respective branch name patterns):**

      * `Require a pull request before merging`: **Enabled**. This is paramount to prevent direct pushes to the branch.
          * `Require approvals`: **Enabled**. Specifies the number of approving reviews required before a PR can be merged (e.g., 1 or 2).
          * `Require approval of the most recent reviewable push`: **Enabled**. This ensures that if new commits are pushed to a PR after it has been approved, new approvals are required for those additional changes.
      * `Require status checks to pass before merging`: **Enabled**. This ensures that all configured CI/CD checks (e.g., tests, linter) pass before a PR can be merged.
      * `Require conversation resolution before merging`: **Enabled**. Ensures all inline comments and discussions on a PR are resolved before it can be merged.
      * `Require linear history`: **Enabled**. This enforces the use of Squash Merge or Rebase Merge, ensuring a clean and linear commit history on the protected branch.
      * `Allow force pushes`: **Disabled**. This prevents anyone from overwriting the branch's history, which can lead to lost commits and confusion.
      * `Allow specified actors to bypass required pull requests`: **Disabled**. This is crucial to ensure that *all* changes, even from repository administrators, go through the defined Pull Request process. No one should be able to bypass these quality gates.

  * **Global Merge Options (Configured in Repository `Settings` \> `General` \> `Pull Requests`):**

      * `Allow merge commits`: **Disabled**. We do not allow traditional merge commits to maintain a linear history.
      * `Allow squash merging`: **Enabled**. This is our preferred method for merging feature and release PRs.
      * `Allow rebase merging`: **Enabled**. This is an alternative merge method that maintains individual commits in a linear fashion.
      * `Always suggest updating pull request branches`: **Enabled**. This helps developers keep their PR branches up-to-date with the base branch, reducing merge conflicts.
      * `Automatically delete head branches`: **Enabled**. This helps keep the repository clean by automatically deleting feature/hotfix/release branches after they have been successfully merged.
      * `Auto-close issues with merged linked pull requests`: **Enabled**. This automatically closes issues when a Pull Request referencing them is merged, keeping the issue tracker current.

-----

## 7\. General Best Practices

### Test Driven Development (TDD)

  * **Follow the Red-Green-Refactor cycle rigorously:**
    1.  **Red:** Write a failing test that defines a new piece of functionality or identifies a bug.
    2.  **Green:** Write the minimum amount of production code necessary to make the newly written test (and all existing tests) pass.
    3.  **Refactor:** Improve the design of the code (and tests) without changing its external behavior or making any tests fail.
  * **Write tests for every layer** (Domain, Data, Presentation) as described in our Clean Architecture guidelines.
  * **Test Coverage:** We strive for high test coverage to ensure code robustness, facilitate refactoring, and minimize the introduction of regressions.

### Clean Architecture

  * **Respect the Dependency Rule:** Inner layers must not depend on outer layers. All dependencies must flow only towards the innermost layers. This ensures that business rules are independent of UI, databases, and frameworks.
  * **Single Responsibility Principle (SRP):** Each class, module, or function should have one, and only one, reason to change. This leads to more maintainable and testable code.
  * **Inversion of Control (IoC) / Dependency Injection (DI):** Utilize a service locator (e.g., `get_it`) for managing and providing dependencies. This facilitates decoupling, makes components easier to test in isolation, and improves overall system flexibility.
  * **Clear Model Separation:** Clearly distinguish between data structures (e.g., Entities in the Domain layer, Models in the Data layer, and specialized objects for the Presentation layer) to prevent leakage of concerns between layers.
