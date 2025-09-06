**VSCode Git workflow**:

---

# VSCode Git Workflow using Issues

### 0. Create an Issue (GitHub)

- In your repo (e.g. [docker-projects](https://github.com/otrw/docker-projects) ):
    
    - Click **Issues → New Issue**.
        
    - Title: short + actiony (e.g. _Add Docker install guide_).
        
    - Body:
        
        ```md
        ## What
        Write a step-by-step install guide for Docker.
        
        ## Why
        To standardize install instructions across projects.
        
        ## Notes
        Tested on Ubuntu 24.04.
        ```
        
    - Submit.
        
- Copy the issue number (e.g. `#12`).
    

---

### 1. Start a branch (linked to the issue)

- In VSCode: Source Control -> `…` → **Branch -> Create Branch…**
    
- Name it after the issue:
    
    ```
    docs/install-docker-guide-12
    ```
    
- This makes it obvious which branch fixes which issue.
    

---

### 2. Make your changes

- Edit files.
    
- Save.
    

---

### 3. Stage & Commit

- In Source Control, stage file(s) with **+**.
    
- Commit with message referencing the issue:
    
    ```
    docs: add install-docker guide (#12)
    ```
    
- The `(#12)` auto-links the commit to the issue.
    

---

### 4. Push branch

- Source Control -> **Sync Changes**.
    
- If it’s new, choose **Publish Branch**.
    

---

### 5. Create Pull Request (VSCode default)

- VSCode will prompt: **Create Pull Request**.
    
- Fill in:
    
    - Title = same as commit prefix (`docs: …`).
        
    - Body = template:
        
        `## What …  ## Why …  ## Notes Closes #12`
        
- PR is created on GitHub via VSCode.

_(Optional in browser)_: You can open the PR in browser to edit/review instead — it’s the same thing.

---

### 6. Squash & Merge

- In VSCode’s **Pull Request panel**, use **Merge → Squash and Merge**.
    
- **Important:** Edit the commit title here if needed (e.g. `feat:` → `docs:`).
    
- Confirm merge.
    

_(Optional in browser)_: Hit **Squash and Merge** on GitHub instead, edit title/body, then confirm.


---

### 7. Cleanup (VSCode)

- Click **Delete Branch** in the PR panel.
    
- VSCode auto-switches to `main` and prompts to **Sync**.
    
- Accept Sync → local `main` now has the merged commit.
    
- Confirm bottom-left shows `main`.

---

## Workflow Summary

- **Issue -> Branch -> Commit -> PR -> Merge -> Auto-close Issue -> Cleanup**

