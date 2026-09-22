Bilkul bhai. Maine tumhare uploaded **Azure DevOps Learning diagram** ko base banaya hai. Isme mainly **Git + GitHub + branching + staging/commit + reset** wale concepts hain. Main ise **simple notes + interview answer + production usage** ke format mein samjha raha hoon.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Topics needed to clear one-by-one:

Azure DevOps fundamentals
Organization → Project → Team → Users → Permissions
Azure Repos
GitHub → Azure Repo migration
Git / Git Clone
Main branch protection
Self-hosted Agent
Agent Pool
Microsoft-hosted vs Self-hosted Agent
Classic Pipeline
YAML Pipeline
Terraform pipeline
Azure CLI / az login
Hardcoded credentials vs Service Connection
Variables
Variable Groups
Parameters
Secrets
Artifacts
Approvals
Templates
Parallel Jobs
Pipeline failures & troubleshooting
Pipeline structure — Organization → Project → Repo → Pipeline → Agent
Terraform workflow — init → fmt → validate → plan → apply
Manual Approval
Stage / Job / Step / Task / Command

The diagram also shows a practical flow involving GitHub → Azure Repo → Self-hosted Agent → Terraform → Azure.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Git — Interview + Production Notes

## 1. Git kya hai?

**Simple:**
Git ek **Distributed Version Control System (DVCS)** hai jo source code ke changes ko track karta hai.

### Real-life example

Maan lo tum Azure infrastructure ke liye Terraform code likh rahe ho:

```text
main.tf
variables.tf
outputs.tf
```

Tumne `main.tf` mein change kiya.

Git tumhe ye track karne deta hai:

```text
Old version → New version
```

Agar problem ho gayi, to previous version par ja sakte ho.

### Interview Answer

> **Git is a distributed version control system used to track, manage, and collaborate on source-code changes. Every developer can have a complete copy of the repository locally.**

---

# 2. Git vs GitHub

Ye interview mein bahut common question hai.

| Git                                         | GitHub                                |
| ------------------------------------------- | ------------------------------------- |
| Version control tool                        | Cloud-based code hosting platform     |
| Local machine par work kar sakta hai        | Remote platform                       |
| Internet required nahi for local operations | Generally internet required           |
| Commit, branch, merge etc.                  | Repository hosting, PR, collaboration |
| Git CLI use karta hai                       | Git repositories host karta hai       |

### Simple yaad rakho:

```text
Git = Tool

GitHub = Platform
```

Production example:

```text
Developer
   ↓
Git
   ↓
Commit
   ↓
GitHub / Azure Repos
   ↓
Azure DevOps Pipeline
   ↓
Azure
```

---

# 3. Git ke 3 Important Areas

Ye **bahut important interview concept** hai.

```text
Working Directory
       ↓
Staging Area
       ↓
Repository / Commit
```

### 1️⃣ Working Directory

Yahan tum actual code likhte ho.

```text
main.tf
variables.tf
outputs.tf
```

Change ki hui file Git mein generally:

```text
U = Untracked
```

ya modified state mein ho sakti hai.

---

### 2️⃣ Staging Area

Jab tum decide karte ho ki kaunsa change commit karna hai:

```bash
git add main.tf
```

Ya:

```bash
git add .
```

Ab file staging area mein hai.

---

### 3️⃣ Commit / Repository

Ab changes ko permanently Git history mein save karte hain:

```bash
git commit -m "Add Azure resource group"
```

---

# 4. Complete Git Flow

Interview mein ye diagram explain karna bahut useful hai:

```text
          Developer writes code
                   ↓
          Working Directory
                   ↓
              git add
                   ↓
            Staging Area
                   ↓
            git commit
                   ↓
          Local Repository
                   ↓
              git push
                   ↓
       GitHub / Azure Repos
```

### Production Example

Developer ne Azure VM ka Terraform code modify kiya:

```bash
git status
git add main.tf
git commit -m "Update VM configuration"
git push origin feature-vm
```

Then:

```text
Pull Request
      ↓
Code Review
      ↓
Merge
      ↓
CI/CD Pipeline
      ↓
Terraform Plan
      ↓
Terraform Apply
      ↓
Azure
```

---

# 5. `git init`

New local repository create karne ke liye:

```bash
git init
```

Ye `.git` directory create karta hai.

```text
project/
├── main.tf
├── variables.tf
└── .git/
```

`.git` ke andar Git repository ki information/history maintain hoti hai.

### Interview

**Q: What does git init do?**

> It initializes a new Git repository in the current directory by creating the `.git` directory.

---

# 6. `git status`

Current repository ki situation check karne ke liye:

```bash
git status
```

Ye bata sakta hai:

```text
Modified files
Untracked files
Staged files
Current branch
```

### Production use

Pipeline ya commit se pehle:

```bash
git status
```

se verify kar sakte ho ki exactly kya change hua hai.

---

# 7. `git add`

Specific file:

```bash
git add main.tf
```

Multiple files:

```bash
git add main.tf variables.tf outputs.tf
```

All changes:

```bash
git add .
```

### Important

`git add` **commit nahi karta**.

It only moves changes:

```text
Working Directory
       ↓
Staging Area
```

---

# 8. Staging se file wapas kaise laaye?

Agar accidentally file staging mein chali gayi:

```bash
git restore --staged main.tf
```

All staged files:

```bash
git restore --staged .
```

Older/common command:

```bash
git rm --cached main.tf
```

---

# 9. `git commit`

Staged changes ko repository history mein save karta hai:

```bash
git commit -m "Add Azure VM configuration"
```

Flow:

```text
Working
   ↓ git add
Staging
   ↓ git commit
Repository
```

### Interview answer

> `git commit` records the staged changes in the local Git repository with a commit message.

---

# 10. Git Log

History dekhne ke liye:

```bash
git log
```

Short format:

```bash
git log --oneline
```

Example:

```text
3f45ab2 Add Azure VM
8ac91de Add VNet
12ab567 Initial commit
```

---

# 11. `git show`

Specific commit ki detailed information:

```bash
git show 3f45ab2
```

Ye normally dikhata hai:

```text
Commit ID
Author
Date
Commit message
Changed files
Diff
```

### Interview Answer

> `git show` displays detailed information and the changes introduced by a specific commit.

---

# 12. Git Reset — Very Important

Ye interview mein frequently poocha jaata hai.

Teen important modes:

```text
--soft
--mixed
--hard
```

---

## `git reset --soft HEAD~1`

Last commit remove karo, **code safe rakho aur changes staged rahenge**.

```bash
git reset --soft HEAD~1
```

Flow:

```text
Commit
   ↓
Staging Area
```

### Use case

Galat commit message diya:

```text
Wrong commit message
```

Commit ko undo karke correct message ke saath dobara commit karna hai.

---

# 13. `git reset --mixed HEAD~1`

Ye default reset behaviour hai:

```bash
git reset HEAD~1
```

Last commit remove hota hai aur changes **working directory mein unstaged** ho jaate hain.

```text
Commit
   ↓
Working Directory
```

Changes delete nahi hote.

---

# 14. `git reset --hard HEAD~1`

⚠️ **Dangerous command**

```bash
git reset --hard HEAD~1
```

Commit aur associated working-tree changes discard ho sakte hain.

Simple memory:

```text
SOFT
Commit → Staging

MIXED
Commit → Working

HARD
Commit + local changes → Discard
```

### Interview Trick

| Reset     | Commit | Staging | Working Code |
| --------- | ------ | ------- | ------------ |
| `--soft`  | Remove | Keep    | Keep         |
| `--mixed` | Remove | Remove  | Keep         |
| `--hard`  | Remove | Remove  | Discard      |

**Production tip:** `--hard` ko production/shared branch par blindly use mat karo.

---

# 15. Branch kya hai?

Branch basically development ki **separate line** hai.

Production project mein normally:

```text
main
 │
 ├── feature-vm
 ├── feature-network
 └── bugfix-nsg
```

Developer feature branch par work karta hai.

---

# 16. Current branch kaise check kare?

```bash
git branch
```

Example:

```text
* master
  feature-vm
  feature-network
```

`*` ka meaning:

> Abhi tum `master` branch par ho.

Modern projects mein often:

```text
main
```

use hota hai instead of `master`.

---

# 17. New Branch Create

```bash
git branch feature-vm
```

Ye branch create karega but automatically switch nahi karega.

### Create + switch

```bash
git checkout -b feature-vm
```

Modern command:

```bash
git switch -c feature-vm
```

---

# 18. Branch Switch

Old command:

```bash
git checkout feature-vm
```

Modern:

```bash
git switch feature-vm
```

---

# 19. Production Branch par Direct Work?

Tumhare notes mein important production concept hai:

```text
❌ Direct production/main branch par development
```

Instead:

```text
main
 │
 ├── feature-rg
 ├── feature-vnet
 └── feature-vm
```

Developer:

```text
feature branch
      ↓
commit
      ↓
push
      ↓
Pull Request
      ↓
Code Review
      ↓
main
```

### Real Azure DevOps Example

Requirement:

> "Azure Resource Group create karna hai."

Branch:

```bash
git switch -c feature-resource-group
```

Code:

```text
main.tf
```

Then:

```bash
git add .
git commit -m "Add resource group"
git push origin feature-resource-group
```

Then Azure DevOps mein:

```text
Pull Request
      ↓
Review
      ↓
Validation Pipeline
      ↓
Merge
```

---

# 20. Branch Delete

Safe delete:

```bash
git branch -d feature-vm
```

Ye normally unmerged changes ko accidentally delete hone se protect karta hai.

Force delete:

```bash
git branch -D feature-vm
```

⚠️ Iska use carefully karo because unmerged work lose ho sakta hai.

---

# 21. Production Git Workflow ⭐

Azure DevOps project mein practical flow kuch aisa ho sakta hai:

```text
Developer
    │
    ▼
Feature Branch
    │
    ▼
Code Changes
    │
    ▼
git add
    │
    ▼
git commit
    │
    ▼
git push
    │
    ▼
Azure Repos
    │
    ▼
Pull Request
    │
    ▼
Code Review
    │
    ▼
Build / CI Pipeline
    │
    ▼
Terraform Plan
    │
    ▼
Approval
    │
    ▼
Terraform Apply
    │
    ▼
Azure Production
```

Ye **DevSecOps interview ke liye bahut important story** hai.

---

# 🎯 Interview Quick Revision

### Q1. Git kya hai?

**Answer:**

> Git is a distributed version control system used to track and manage source-code changes.

### Q2. GitHub kya hai?

> GitHub is a cloud-based platform used to host Git repositories and support collaboration.

### Q3. Git ke 3 areas?

```text
Working Directory
       ↓
Staging Area
       ↓
Repository
```

### Q4. `git add`?

> Moves changes from working directory to staging area.

### Q5. `git commit`?

> Saves staged changes into the local Git repository.

### Q6. `git push`?

> Uploads local commits to a remote repository.

### Q7. `git pull`?

> Fetches changes from remote and integrates them into the current branch.

### Q8. `git fetch`?

> Downloads remote changes without directly merging them into the current branch.

### Q9. `git reset --soft`?

> Removes the commit but keeps changes staged.

### Q10. `git reset --hard`?

> Removes the commit and discards local changes; use with caution.

### Q11. Branch kya hai?

> A separate line of development used to work on changes independently.

### Q12. Production mein feature branch kyun?

> To isolate development work from the stable production/main branch and allow review and testing before merging.

---

# 🧠 One-Line Memory Trick

```text
git status   → Kya change hua?
git add      → Kya commit karna hai?
git commit   → Save history
git log      → History dekho
git show     → Specific commit dekho
git branch   → Branch dekho
git switch   → Branch change karo
git merge    → Branch changes combine karo
git push     → Remote par bhejo
git pull     → Remote changes lao
git fetch    → Remote changes dekho/download karo
git reset    → Commit undo karo
```

**Interview mein sabse important flow yaad rakho:**

```text
CODE
 ↓
WORKING DIRECTORY
 ↓ git add
STAGING AREA
 ↓ git commit
LOCAL REPOSITORY
 ↓ git push
REMOTE REPOSITORY
 ↓
PULL REQUEST
 ↓
CODE REVIEW
 ↓
CI/CD
 ↓
PRODUCTION
```

Ye tumhare **Azure DevOps + Terraform + DevSecOps interviews** ke liye strong foundation hai.
