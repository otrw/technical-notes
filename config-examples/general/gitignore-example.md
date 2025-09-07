# `.gitignore` file example

**NOTE**: `.gitignore` does not retroactively ignore files or directories.  
If a file or directory has already been committed, adding it to `.gitignore` will not stop it from being tracked.  

Example of a `.gitignore` file for projects.

```bash
# Cloud credentials/configs
.azure/
.aws/
*.publishsettings
*.azureauth

# Infrastructure as Code
.terraform/
*.tfstate
*.tfstate.*
*.tfvars
.terraform.lock.hcl

# Editor/IDE files
.vscode/
.idea/
*.code-workspace
*.swp
*.swo

# Environment/secrets
.env                   # Ignore base .env file containing local environment variables.
.env.*                 # Ignore all other env files (e.g., .env.production, .env.local) except specific templates (below)
!config.template.json  # Do *not* ignore config.template.json – used as a safe example config
!.env.template         # Do *not* ignore env template – useful for sharing expected env variables safely
*.pem
*.key
id_rsa*
*.pfx
*.cer
*.p12
*password*
*secret*
*credential*
config.local.*
config.json

# Binaries
*.jar

# OS files
.DS_Store
Thumbs.db
*.tmp

# Personal/draft notes (Obsidian etc.)
drafts/
personal/
private/
inbox/
__inbox/
.obsidian/
AccountSettings.json
Settings.json

# Docker volumes, configs and overrides
docker-compose.override.yml  # Ignore local Docker Compose override files (developer-specific)
**/backups/                  # Ignore 'backups' directory at any depth
**/data/                     # Ignore any 'data' directory at any depth (used for Docker volumes or app data)
**/.env                      # Ignore any .env files inside subdirectories (usually project-specific environment files)
**/logs/                  # Ignore logs folders at any depth (often in Docker apps)
docker-compose.override.*  # Catch alternate overrides like override.dev.yml
.docker/                 # Some repos use this for docker config/scripts
**/config/            # Ignore any 'config' directory at any depth (often used for app configs)
```

---

## Global `.gitignore`

**NOTE:** You can also set up a global ignore file (e.g. `~/.gitignore_global`) for patterns you want applied everywhere. Configure it with:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

However, using a `.gitignore` per project is usually clearer and avoids unexpected conflicts.
