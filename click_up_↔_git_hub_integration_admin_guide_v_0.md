# ClickUp ↔ GitHub Integration — **Admin Guide** (v0.1)

> **Audience:** Workspace admins / project leads who create and assign tasks, and link them to GitHub.
>
> **Goal:** Manually (no automations) link ClickUp tasks to GitHub Issues/Branches/PRs so progress is visible in both systems.

---

## 1) Prerequisites

- ClickUp **Workspace Admin** rights
- GitHub account with access to the target repository (maintainer or write)
- A Space/List in ClickUp dedicated to this project

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/1.png)

---

##

### 2.2 Connect your personal GitHub account

1. Go to **Workspace Settings → App Center / Integrations → GitHub**.
2. In the **Personal** section, click **Connect** and authorize ClickUp in GitHub.
3. Confirm that your GitHub username appears as **Connected**.

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/2.png)

### 2.3 Link repositories to your Workspace/Space

1. Still in **App Center → GitHub**, switch to the **Workspace** tab (next to Personal), click **Connect**, then click **Settings** to link repositories to your Space.
2. Select the repository (or multiple) you want to use with this Workspace.
3. Use the **Space** dropdown to select **which Space** should use each repository.
4. Click **Save**.

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/3.png)
![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/4.png)
![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/5.png)
![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/6.png)


> **Note:** If you’d like a repository to be available only in a specific **List**, you can optionally scope in that List’s settings later. Linking to the Space is sufficient for most teams and ensures the GitHub panel appears in tasks in that Space.

---

## 3) Verifying the GitHub Panel in a Task

1. Open **any task** in the linked Space.
2. On the **right sidebar**, look for the **GitHub** icon/panel.
   - If you don’t see it, click the **“+”** at the bottom of the sidebar and add **GitHub**.
3. If prompted, choose **Connect repository** and select your repo.

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/7.png)

> **Troubleshooting:** If the panel still doesn’t appear, re-check that (a) the GitHub ClickApp is ON for this Space and (b) the repo is linked to this Space in App Center.

---

## 4) Creating & Assigning a Task (Admin flow)

### 4.1 Create the task in ClickUp

1. Go to your project **List** → click **+ New Task**.
2. Fill in **Task name** and **Description** with clear acceptance criteria.
3. Assign the task to a **person** and set **priority**/**due date** as needed.
4. Copy the **Task ID** (format like `CU-xxxxx`) visible near the task title.

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/8.png)

### 4.2 Link the task to GitHub and create an Issue (manual, no automations)

1. In the task, open the **GitHub** panel → click **Add GitHub link** → **New GitHub Issue**.
2. Select the **Repository**.
3. Confirm **Title** (defaults to task name) and **Body** (include description + a copy of the ClickUp Task ID (format like `CU-xxxxx`)).
4. (Optional) Add **Labels** or **Assignee** to the GitHub issue.
5. Click **Create**.

![Screenshot 1](https://raw.githubusercontent.com/ryzhokhin/SomeDocs/main/AdminScreenshots/9.png)

> **Best practice:** Include the **ClickUp Task URL** and the **Task ID** in the issue description so devs/agents can reference it and ClickUp can auto-link future commits/PRs.

### 4.3 Create a GitHub Branch for the task (manual)

1. In the same **GitHub** panel → click **New GitHub Branch**.
2. Confirm the **Repository** and **Base branch** (defaults to `main`; change if needed).
3. Confirm/edit the **Branch name**. ClickUp will suggest a slug (often derived from the task name). Recommended pattern:
   - `feature/CU-<taskId>-<short-task-name>` OR `bugfix/CU-<taskId>-<short-task-name>`
4. Click **Create**.



> **Note:** The branch is now created in GitHub and linked to the task. Developers should include the **Task ID** in commits (e.g., `CU-xxxxx`) so ClickUp auto-associates activity.

### 4.4 (Optional) Create a Pull Request from the task

- When the developer is ready, they (or you) can open **New Pull Request** from the **GitHub** panel in the task.
- Include `Fixes #<issue-number>` in the PR description to auto-close the GitHub issue upon merge.
- Include the **ClickUp Task ID** (`CU-xxxxx`) in the PR title or body for robust linking.



---

## 5) Hand‑off to Developers (at a glance)

Provide the assignee with:

- The **ClickUp task link** and **Task ID** (e.g., `CU-3k5yq6`)
- The **linked GitHub Issue** number (e.g., `#42`)
- The **feature branch** name (or instructions to create it from the task panel)

> **Developer essentials:**
>
> - Commit messages should include `CU-<taskId>`
> - PR description should include `Fixes #<issue-number>` to close the issue on merge
> - PR will appear in the task’s GitHub panel; merging the PR will reflect back in ClickUp

---

## 6) Naming & Conventions (recommended)

- **Branches:** `feature/CU-<taskId>-<slug>` or `bugfix/CU-<taskId>-<slug>`
- **Labels:** Use a minimal set (`feature`, `bug`, `docs`, `priority:high`)
- **Commits:** Start with concise action + include `CU-<taskId>` (e.g., `feat: add session queue isolation (CU-3k5yq6)`)
- **PR Title:** Start with a verb + include **Issue** and **Task ID** (e.g., `Add session isolation, Fixes #42 (CU-3k5yq6)`).

---

## 7) Verifying Progress & Status (Admin view)

- In the task’s **GitHub panel**, you can see:
  - Linked **Issue** status (Open/Closed)
  - Linked **Branch**
  - Linked **PR** status (Open/Merged/Closed)
  - Linked **Commits** (when commit messages include `CU-<taskId>`)
- Update the ClickUp task **status** as your process requires (manual), or enable Automations later if you want status changes on **PR opened/merged**.



---

## 8) Troubleshooting

- **GitHub panel missing in task**

  - Ensure **ClickApps → GitHub** is ON for this Space
  - Ensure the **repository is linked** to this Space in App Center
  - Refresh and re-open the task, or add the panel via the sidebar **“+”**

- **Issue/PR not linking to the task**

  - Make sure you created it from the task’s **GitHub panel**, or
  - Include the ClickUp **Task ID** (`CU-xxxxx`) in the PR/commit messages; then click **Add GitHub link → Search** to attach existing items

- **PR merged but task didn't move**

  - If you want automatic status changes, you'll need **Automations** (optional). Without automations, update status manually.

---