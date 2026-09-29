# Team Contract — CSC207 Software Design

## 1. Purpose of this Contract
This contract establishes the shared expectations, operational protocols, and mutual commitments for our team during CSC207 (Software Design). It is designed to promote individual accountability, engineering rigor, transparent collaboration, and professional communication throughout the term as we work on in-class activities, tutorials, two-stage tests, and the collaborative development of our Java desktop application.

---

## 2. Team Norms and Expectations

### a) Communication
* **Primary Communication Platform:** WeChat (dedicated private group chat named `CSC207-Team`).
* **Response Latency Expectations (Observable & Measurable):**
  * **Daily Standard:** Every team member must acknowledge or respond to messages within **12 hours** at all times.
  * **Critical Submission Windows (within 48 hours of any course milestone):** Members must respond within **2 hours**.
* **Communication Etiquette:** All technical debates must remain objective, respectful, and grounded in course concepts (SOLID principles, Clean Architecture boundary separation, design patterns) rather than personal preferences.

### b) Attendance & Punctuality
* **Mandatory Sessions:** Members agree to attend all weekly lecture activities, labs/tutorials, and team-specific synchronous standups.
* **Internal Weekly Sync:** One scheduled 45-minute synchronous sync per week (Day/Time: [e.g., Sunday 8:00 PM EDT on WeChat Voice Call]).
* **Advance Absence Protocol (Specific & Observable):**
  * In cases of illness or extenuating circumstances, notify the team via the WeChat group at least **4 hours prior** to the scheduled meeting.
  * Absent members must post an asynchronous status update within **12 hours** of the missed meeting answering:
    1. *What was completed since the last sync?*
    2. *What is blocked or delayed?*
    3. *What is the target deliverable for the next 48 hours?*
* **Punctuality Benchmark:** Members must arrive within **5 minutes** of the agreed start time. Arriving more than 10 minutes late without advance notice is tracked as an unexcused tardiness.

### c) Task Allocation & Decision Making
* **Work Tracking:** All project tasks, feature implementations, and use cases will be managed via GitHub Issues and GitHub Projects board. Each issue must have an explicit assignee, clear scope, and an estimated completion date.
* **Architectural Decisions:** Core design decisions (e.g., Entities, Use Case interactor boundaries, Controller/Presenter interfaces, external libraries) will be decided through consensus.
* **Tie-Breaking Rule:** If consensus cannot be reached within **24 hours**, a majority vote will be held. In the event of a tie, the team will consult our lab TA or course instructor during office hours.

---

## 3. Version Control & Git Push Standards (CSC207 Protocol)

To prevent merge conflicts, broken builds, and repository corruption, all members must strictly enforce the following Git workflow.

### a) Zero Direct Commits to `main`
* Direct commits or pushes to the `main` branch are **strictly prohibited**.
* The `main` branch must at all times remain deployable, stable, and pass all local Maven builds (`mvn test`).
* All development work must be done on isolated topic/feature branches and merged only via Pull Requests (PRs).

### b) Semantic Branch Naming
Branch names must reflect the associated issue and follow standard prefixes:
* `feature/<issue-num>-<short-description>` (e.g., `feature/14-signup-use-case`)
* `bugfix/<issue-num>-<short-description>` (e.g., `bugfix/22-fix-nullpointer-presenter`)
* `test/<issue-num>-<short-description>` (e.g., `test/31-add-user-entity-tests`)
* `refactor/<issue-num>-<short-description>` (e.g., `refactor/19-extract-dao-interface`)

### c) Step-by-Step Feature Push Workflow
Every developer must follow this standardized terminal sequence:

1. **Synchronize Base:** Update your local `main` before branching:
   ```bash
   git switch main
   git pull origin main
   ```

2. **Branch Creation:**
   ```bash
   git switch -c feature/<issue-num>-<feature-name>
   ```

3. **Local Build & Test Verification:**
   Before staging any files, compile and run the full test suite locally:
   ```bash
   mvn clean test
   ```
   *Never push code that fails local compilation or causes unit test failures.*

4. **Inspect Tracking Status:**
   ```bash
   git status
   ```
   Ensure no untracked local metadata or build artifacts are caught.

5. **Atomic Commits:**
   Avoid indiscriminate staging (`git add .`). Prefer explicit file additions:
   ```bash
   git add src/main/java/path/to/File.java src/test/java/path/to/Test.java
   ```
   Commit messages must use the imperative present tense, start with a verb, and clearly state the purpose:
   ```bash
   git commit -m "Implement validation logic in SignupInteractor"
   ```

6. **Publishing Branch to Remote:**
   ```bash
   git push -u origin feature/<issue-num>-<feature-name>
   ```

7. **Syncing Updates Before Opening a PR:**
   If `main` has progressed on the remote while working, re-integrate changes locally first:
   ```bash
   git switch main
   git pull origin main
   git switch feature/<issue-num>-<feature-name>
   git merge main
   mvn test
   git push origin feature/<issue-num>-<feature-name>
   ```

### d) .gitignore & Secret Protection Rules
* **Never commit generated or environment-specific files:**
  * Build outputs: `target/`, `*.class`, `*.jar`
  * IDE directories: `.idea/`, `*.iml`, `.vscode/`
  * OS metadata: `.DS_Store`, `Thumbs.db`
* **Zero-Secret Policy:** Never commit plain-text API keys, passwords, database credentials, or GitHub Personal Access Tokens (PAT). Any sensitive values must be injected via environment variables or loaded from an untracked local configuration file.

### e) Pull Requests & Code Review Protocols
* **PR Template Requirements:** Every PR must link to its issue (e.g., `Closes #14`) and provide:
  * What feature/fix does this PR introduce?
  * Which Clean Architecture layers are affected?
  * Testing confirmation (JUnit test results and manual UI test notes).
* **Approval Gates:** Each PR requires at least two (2) peer approvals before merging.
* **Review SLA:** Assigned reviewers must inspect code, run tests, and leave feedback or approve within 24 hours.
* **Forbidden Git Operations:**
  * Running `git push --force` or `git push -f` on `main` or shared remote branches is strictly forbidden.
  * Do not rewrite shared remote history with `git reset --hard`; use `git revert` if a merged commit must be undone.

---

## 4. Evaluation Criteria (Observable, Measurable, Specific)

These criteria will directly govern our mid-term and end-of-term peer and self-evaluations:

| Dimension | Observable & Measurable Benchmark (Exceeds / Meets) | Unacceptable Performance (Below Standard) |
| :--- | :--- | :--- |
| **Meeting Reliability & Punctuality** | Attends $\ge 90\%$ of scheduled syncs; arrives within 5 minutes; provides $\ge 4$ hours notice for absences. | Misses meetings without notice; late by $>15$ minutes on more than two occasions. |
| **Responsiveness** | Responds to WeChat messages within 12 hours under all regular circumstances. | Unreachable for $>12$ hours without advance announcement ("ghosting"). |
| **Version Control Hygiene** | Follows feature branch workflows; writes imperative commit messages; pushes zero broken builds or IDE files. | Commits directly to main; executes force push; pushes code that fails `mvn test`. |
| **Code Review Rigor** | Thoroughly reviews peer PRs within 24 hours; tests code locally; checks Clean Architecture boundaries. | Approves PRs blindly without reading/testing; ignores review requests for $>48$ hours. |
| **Delivery & Testing** | Completes assigned issues 48h before external deadlines; includes JUnit 5 tests covering happy/edge cases. | Pushes incomplete code at or after the deadline; leaves tasks untested for peers to fix. |

---

## 5. Conflict Resolution Matrix

When technical, workflow, or interpersonal disagreements occur, the team will follow a 3-step escalation path:

1. **Step 1: Internal Synchronous Dialogue (Within 24 Hours)**  
   The team will schedule an informal WeChat voice call or in-person discussion dedicated solely to addressing the blocker or division of labor objectively.
2. **Step 2: Formal Written Notice & Cure Period (Within 48 Hours)**  
   If a member repeatedly misses deadlines, fails to communicate within 12 hours, or violates Git protocol, the team will post a formal written summary in the WeChat group outlining the exact unmet expectation and setting a 48-hour cure window.
3. **Step 3: Teaching Team Escalation (After 48 Hours Unresolved)**  
   If the issue remains unresolved after the cure window, the team will immediately contact our Assigned Lab TA and Course Instructor via the course email (`csc207-2026-09@cs.toronto.edu`), providing documented evidence (chat screenshots, GitHub commit logs, unreviewed PRs) for mediation.

---

## 6. Accountability & Peer Evaluation Statement

* All team members acknowledge that course grades for the Team Project include an individual scaling factor determined by peer evaluations, commit history, and TA observations.
* Failure to satisfy the expectations agreed to in this contract will directly result in lower peer evaluation scores.
* All peer evaluations submitted by members of this team will be factual, fair, and based strictly on the observable benchmarks set forth in Section 4.

---

## 7. Signatures & GitHub Affirmation

By signing below and approving the Pull Request that merges this file into `main`, each member acknowledges that they have read, understood, and agreed to be bound by these terms throughout the semester.

| Full Legal Name | UTORid | GitHub Username | Date Signed |
| :--- | :--- | :--- | :--- |
| Kehan Li | likehan6 | @[github-handle-1] | 2026-09-29 |
| [Student 2 Full Name] | [utorid02] | @[github-handle-2] | 2026-09-29 |
| [Student 3 Full Name] | [utorid03] | @[github-handle-3] | 2026-09-29 |
