# How I Add / Update Notes (Workflow)

Since yeh personal knowledge base hai, yeh workflow follow karo taaki structure consistent rahe:

## Naya note add karna hai
1. Relevant topic folder me jao (e.g. `linux/`, `cloud/aws/`)
2. `resources/templates/note-template.md` copy karo
3. File ka naam clear rakho: `kebab-case.md` (e.g. `ssh-key-auth.md`)
4. Us topic ke `README.md` ki table me ek row add karo
5. Commit message format: `docs(topic): add <short-description>`
   - example: `docs(linux): add ssh key authentication notes`

## Naya topic add karna hai (e.g. Kubernetes, Docker, Ansible)
1. Root me naya folder: `mkdir docker`
2. `resources/templates/topic-index-template.md` copy karke `docker/README.md` banao
3. Root `README.md` ki **Topic Index** table me row add karo
4. Commit: `docs: add docker topic`

## Existing note update karna hai
1. File edit karo
2. `last-updated` field update karo note ke top par
3. Commit: `docs(topic): update <note-name>`

## Quick revision se pehle
- Har topic ke README ka **⚡ Cheat Sheet** section padho — 5 min me refresh ho jayega
- Root README ke **Revision Tracker** table me date update kar do
