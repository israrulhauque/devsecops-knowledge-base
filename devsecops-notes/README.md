# 🛡️ DevSecOps Notes

Personal knowledge base for **DevSecOps** — Linux, Cloud (Azure/AWS/GCP), Terraform, Git & GitHub, and CI/CD Pipelines.
Built for **quick revision** before interviews, and designed so **new topics/tools can be added anytime** without breaking structure.

---

## 📌 How to use this repo

- Har topic ka apna folder hai. Har folder ke andar ek `README.md` (index) hai jisme sab notes ka summary + links hain.
- Naya note likhna ho toh `resources/templates/note-template.md` copy karo, rename karo, fill karo.
- Quick revision ke liye har topic README ke top par **⚡ Cheat Sheet / Quick Revision** section hai.
- Naya topic add karna ho (e.g. Kubernetes, Docker, Ansible) toh bas root me naya folder bana lo, isi pattern se.

---

## 🗂️ Repo Structure

```
devsecops-notes/
├── linux/                 # Linux fundamentals, commands, hardening
├── cloud/
│   ├── azure/             # Azure notes
│   ├── aws/                # AWS notes
│   └── gcp/                # GCP notes
├── terraform/              # IaC notes, modules, best practices
├── git-github/              # Git commands, GitHub workflows, branching
├── pipeline/                # CI/CD (GitHub Actions, Jenkins, Azure Pipelines etc.)
├── resources/
│   └── templates/           # Reusable templates for new notes
└── .github/                 # Issue templates (optional, for tracking TODOs)
```

---

## ✅ Topic Index

| Topic | Status | Link |
|---|---|---|
| Linux | 🟡 In Progress | [linux/](./linux/README.md) |
| Cloud - Azure | 🟡 In Progress | [cloud/azure/](./cloud/azure/README.md) |
| Cloud - AWS | 🟡 In Progress | [cloud/aws/](./cloud/aws/README.md) |
| Cloud - GCP | 🟡 In Progress | [cloud/gcp/](./cloud/gcp/README.md) |
| Terraform | 🟡 In Progress | [terraform/](./terraform/README.md) |
| Git & GitHub | 🟡 In Progress | [git-github/](./git-github/README.md) |
| CI/CD Pipeline | 🟡 In Progress | [pipeline/](./pipeline/README.md) |

> Status legend: 🔴 Not Started · 🟡 In Progress · 🟢 Complete

---

## ➕ Adding a New Topic (e.g. Kubernetes, Docker, Ansible)

1. Root me naya folder banao: `mkdir kubernetes`
2. Uske andar `README.md` bana kar `resources/templates/topic-index-template.md` se copy karo.
3. Upar wali **Topic Index** table me ek row add kar do.
4. Notes likhte time `resources/templates/note-template.md` use karo — consistency maintain hogi.

Bas itna hi — structure predictable rahega, chahe kitne bhi topics add karo.

---

## 🏷️ Tags / Labels (optional convention)

Notes ke top par tags use kar sakte ho taaki search/filter easy ho:

```
tags: [linux, security, interview-prep]
```

---

## 📅 Revision Tracker

Use this to track jab last revise kiya:

| Topic | Last Revised | Next Revision Due |
|---|---|---|
| Linux | - | - |
| Azure | - | - |
| AWS | - | - |
| GCP | - | - |
| Terraform | - | - |
| Git & GitHub | - | - |
| Pipeline | - | - |

---

## 📝 License

Personal notes — MIT licensed (see [LICENSE](./LICENSE)), feel free to fork if it helps you too.
