# 🌍 Terraform

## ⚡ Cheat Sheet / Quick Revision
- Workflow: `terraform init` → `plan` → `apply` → `destroy`
- Core files: `main.tf`, `variables.tf`, `outputs.tf`, `terraform.tfvars`
- State: `terraform.tfstate` — use **remote backend** (S3+DynamoDB, Azure Storage, GCS) for teams
- Providers: `aws`, `azurerm`, `google`, etc.
- Modules: reusable blocks — `module "name" { source = "./modules/xyz" }`
- Key commands: `terraform fmt`, `terraform validate`, `terraform state list`, `terraform import`
- Best practices: lock state, use workspaces for envs, pin provider versions, never commit `.tfstate` or secrets

## 📚 Notes in this topic

| Note | Description |
|---|---|
| _(add your notes here)_ | e.g. `state-management.md`, `modules-basics.md` |

## ➕ How to add a note
Copy `../resources/templates/note-template.md`, save inside this folder, add a row above.
