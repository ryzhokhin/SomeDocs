# ClickUp ↔ GitHub Integration — **Developer Guide** (v0.1)

> **Audience:** Engineers who execute tasks created in ClickUp and deliver code via GitHub.
>
> **Goal:** Work a task end‑to‑end *manually* (no automations): locate the linked GitHub issue, do the work in your IDE/AI tool (Cursor recommended), open a PR that closes the issue, and let ClickUp reflect the status.

---

## 1) Prerequisites

- Access to the ClickUp **Space/List** where tasks are assigned
- GitHub **write** access to the target repository
- Local checkout of the project (or open in **Cursor** / your preferred IDE)

> **Screenshot to insert:** Task board with an assigned task highlighted

---

## 2) Pick your task in ClickUp

1. Open the task you’re going to work on.
2. Note the **Task ID** (format like `CU-xxxxxx`) shown near the task title.

> **Screenshot to insert:** Task view with **Task ID** location highlighted

---

## 3) Open the GitHub panel in the task

1. In the **top‑right** (task view), click the **GitHub** icon.
2. In the GitHub panel, locate the **linked GitHub Issue** for this task and make sure its status is **Open**.
3. Click **Copy link** (the Issue URL) — you’ll paste it into your IDE/AI tooling.

> **Screenshots to insert:**
>
> - Where to click the **GitHub** icon in the task
> - GitHub panel showing the **Open** Issue
> - **Copy Issue Link** affordance

---

## 4) Work in your AI‑assisted IDE (Cursor recommended)

Open the project in **Cursor** (or your favorite AI IDE). Provide the Issue URL and let the assistant handle routine steps. Use this prompt template:

```text
Complete the following GitHub workflow:

Issue URL: [PASTE_GITHUB_ISSUE_URL_HERE]

Instructions:
1. Extract the task ID from the issue (format: CU-XXXXXXX)
2. Find and checkout the branch matching that task ID
3. Make a meaningful change to the codebase (add a comment documenting the task) - break your response here if needed or prompted if task needs more involvement and finish the next steps later.
4. Commit with message: "Description #<task_id>[complete]"
5. Push the branch to origin
6. Provide me with the GitHub PR creation URL that includes "Closes #N" in the description

Project location: [put the project location if needed]
```

> **Notes:**
>
> - If a branch **doesn’t exist yet**, create one from the base branch (usually `main`). Suggested naming: `feature/CU-<taskId>-<short-name>`.
> - Keep commits small; include the **ClickUp Task ID** (`CU-xxxxxx`) in commit messages for reliable linking.

---

## 5) Open the PR and close the Issue

1. Use the **PR creation URL** returned by your AI tool (or open one manually in GitHub).
2. In the PR **description**, include the closing keyword with the Issue number, e.g. `Closes #123`.
3. Include the ClickUp **Task ID** (`CU-xxxxxx`) in the PR body or title for extra linkage.
4. Submit the PR for review.

> **Screenshot to insert:** PR creation screen with `Closes #N` and `CU-xxxxx` highlighted

---

## 6) Merge and verify ClickUp status

- When the PR is **merged**, GitHub will **close the Issue** automatically (thanks to `Closes #N`).
- In ClickUp, the task’s GitHub panel will reflect the PR as **Merged** and the Issue as **Closed**. If your team uses automations, the task status may update automatically; otherwise, update it manually.

> **Screenshot to insert:** Task view showing PR = Merged, Issue = Closed

---

## 7) Common variants & tips

- **Branch not found:** Create it: `git checkout -b feature/CU-<taskId>-<slug> origin/main`
- **Different base branch:** Use release or develop as required; confirm in task notes.
- **Multiple commits:** Keep each commit scoped; always include `CU-<taskId>`.
- **Link an existing Issue/PR:** In the task’s GitHub panel → **Add GitHub link → Search** and select the item.
- **Pure Codex Web limitation:** It cannot list Issues via API (sandboxed). Use **Cursor** (or similar) to fetch Issues automatically; otherwise copy/paste the Issue text and URL into the prompt.

---

## 8) Quick checklist (developer)

-

---

## 9) Troubleshooting

- **I don’t see the GitHub panel:** Ask an admin to ensure the repo is linked to this Space (App Center → GitHub → Workspace → Settings → Add repo → map to Space).
- **PR merged but task didn’t move:** Add automations later, or move the task manually.
- **AI can’t fetch issues:** Use Cursor (connected) or paste the Issue content manually.

---

## 10) Appendix: CLI snippets (optional)

```bash
# Create and push a branch if missing
BR="feature/CU-<taskId>-<slug>" && \
  git checkout -b "$BR" origin/main && \
  git push -u origin "$BR"

# Example commit with ClickUp Task ID
git add -A && git commit -m "feat: document session queue (CU-3k5yq6)" && git push
```

