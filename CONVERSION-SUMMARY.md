# What Changed: Full Repo Conversion

## Before
- Legacy structure: `cases/`, `runbooks/`, `doc-gaps/`, `enhancement-idea/`
- Platform-agnostic documentation
- Mixed artifact types in folders
- No standardized entry point
- No platform-aware fixes

## After

### New Entry Points (Pick One)
1. **[BY-PLATFORM.md](BY-PLATFORM.md)** — Click platform, scan table, copy fix ⭐ **RECOMMENDED**
2. **[QUICK-FIX-PLATFORM.md](QUICK-FIX-PLATFORM.md)** — All fixes by platform, copy-paste ready
3. **[START-HERE.md](START-HERE.md)** — 4-step guided troubleshooting
4. **[indexes/by-platform.md](indexes/by-platform.md)** — Detailed table with incident links
5. **[indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)** — Search by error pattern

### New Canonical Structure
```
knowledge/
├── incidents/
│   ├── incident-inc-0001-namespace-missing.md (ArgoCD+AKS)
│   ├── incident-inc-0002-values-file-missing.md (ArgoCD+AKS)
│   ├── incident-inc-0003-destination-mismatch.md (ArgoCD+AKS)
│   ├── incident-inc-0004-rbac-denied.md (ArgoCD+AKS)
│   ├── incident-inc-0005-hook-failed.md (ArgoCD+AKS)
│   ├── incident-inc-0010-appservice-targetinvocation.md (App Service) ✨ NEW
│   ├── incident-inc-0020-aca-container-failed.md (ACA) ✨ NEW
│   ├── incident-inc-0030-podman-image-pull.md (Podman) ✨ NEW
│   └── incident-inc-0040-weblogic-classnotfound.md (WebLogic) ✨ NEW
├── runbooks/ (scaffolded)
├── doc-gaps/ (scaffolded)
├── automations/ (scaffolded)
└── decisions/ (scaffolded)

indexes/
├── incidents-index.md (sorted by ID + platform)
├── by-platform.md ⭐ KEY FOR USERS
├── error-signatures-by-platform.md ⭐ KEY FOR USERS
├── runbooks-index.md
├── doc-gaps-index.md
├── automations-index.md
└── tags-index.md
```

### Platform Support
✅ **9 total incidents across 5 platforms (ready to copy-paste):**
- **ArgoCD + AKS** — 5 incidents (all published)
- **Azure App Service** — 1 incident (published)
- **Azure Container Apps (ACA)** — 1 incident (published)
- **Podman** — 1 incident (published)
- **WebLogic** — 1 incident (published)

### Key Changes to Incidents
- Added `platforms: [...]` array (was single `platform: ` field)
- All 5 ArgoCD incidents now have full Error → Fix → Verify format
- 4 new sample incidents for other platforms with platform-specific commands
- All incidents use frontmatter for machine-readability

### Updated Documentation
- **[README.md](README.md)** — Clean entry point table + principles
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — Platforms, precision-first rules, platform-aware linking
- **[TAXONOMY.md](TAXONOMY.md)** — Platforms list, platform-specific tags
- **[PRECISION-GUIDE.md](PRECISION-GUIDE.md)** — Writing rules for minimal docs
- **[BY-PLATFORM.md](BY-PLATFORM.md)** — New first-choice entry point ⭐

### Template Improvements
- Updated [templates/incident-template.md](templates/incident-template.md) to show `platforms` array
- All templates now emphasize platform field

### Legacy Folders (Still Present)
- `cases/`, `runbooks/`, `doc-gaps/`, `enhancement-idea/` — Available for reference
- Updates to legacy index files point to canonical locations

---

## Usage Example

**Before:** Had to read long case files, find relevant runbook section, no platform distinction.

**Now:**
1. Go to [BY-PLATFORM.md](BY-PLATFORM.md)
2. Click your platform (e.g., "ArgoCD + AKS")
3. Find error in table (e.g., "namespaces" not found")
4. Click incident link or copy fix directly
5. Run command
6. Verify

---

## For Contributors

**Adding fixes for a new platform?**
1. Create incident file: `incident-inc-XXXX-<domain>-<error>.md`
2. Set `platforms: [appservice]` (or your platform)
3. Add Error, Fix, Verify sections
4. Update [indexes/by-platform.md](indexes/by-platform.md) row for your platform
5. Update [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

**Template:** [templates/incident-template.md](templates/incident-template.md)

**Full guide:** [CONTRIBUTING.md](CONTRIBUTING.md)

---

## What's Next (Optional)

- Add more platform-specific incidents (App Service 401, ACA port conflicts, etc.)
- Create runbooks from incident fixes
- Build automation specs to link to incident patterns
- Wire up GitHub Copilot to use platform index for context
