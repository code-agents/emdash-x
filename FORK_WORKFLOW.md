# Fork Workflow Guide

## Overview
This document outlines the branch naming conventions and workflow policies for maintaining a fork of emdash while keeping it synchronized with upstream changes and managing custom modifications.

## Branch Structure

```
main                          # Clean mirror of upstream/main
├── custom/main              # Your stable custom features branch
├── custom/feature-*         # Personal features/modifications
├── feat/*                   # Features to contribute upstream
├── fix/*                    # Bug fixes (personal or upstream)
└── sync/upstream-*          # Temporary branches for merging
```

## Git Remotes Configuration

```bash
# Your fork (origin)
origin: https://github.com/code-agents/emdash-x.git

# Upstream repository (when available)
upstream: [upstream-repo-url]
```

## Branch Naming Conventions

### Custom Branches (Stay in Fork)
- `custom/main` - Your stable customizations base branch
- `custom/feature-name` - Personal features/modifications  
- `custom/config-xyz` - Configuration specific to your setup
- `custom/experimental-*` - Experimental features
- `private/*` - Sensitive or personal configurations

### Upstream-Compatible Branches
Following the project's conventions from CONTRIBUTING.md:
- `feat/short-slug` - New features for upstream
- `fix/issue-name` - Bug fixes
- `docs/improvement` - Documentation updates  
- `chore/task` - Maintenance tasks
- `refactor/component` - Code refactoring
- `perf/optimization` - Performance improvements
- `test/addition` - Test additions

### Temporary Branches
- `sync/upstream-YYYY-MM-DD` - Upstream merge branches
- `merge/resolve-conflicts` - Conflict resolution

## Workflow Commands

### Quick Git Aliases
The following git aliases have been configured for efficient workflow:

```bash
# Sync with upstream (when available)
git sync-upstream

# Update your custom branch with main changes
git update-custom

# Create new custom feature branch
git new-custom my-feature

# Create new upstream feature branch
git new-upstream awesome-feature

# View branch tracking status
git branch-status

# View custom branch history
git custom-log
```

### Manual Workflow Steps

#### 1. Initial Setup
```bash
# Add upstream remote (when repository becomes available)
git remote add upstream [upstream-repo-url]

# Verify remotes
git remote -v
```

#### 2. Regular Upstream Sync
```bash
# Sync main with upstream
git checkout main
git fetch upstream
git merge upstream/main --ff-only
git push origin main

# Update custom/main with upstream changes
git checkout custom/main  
git merge main
# Resolve any conflicts if needed
git push origin custom/main
```

#### 3. Custom Feature Development
```bash
# Start new custom feature
git checkout custom/main
git checkout -b custom/my-feature
# ... develop ...
git commit -m "custom: add my feature"
git checkout custom/main
git merge --no-ff custom/my-feature
git push origin custom/main
```

#### 4. Upstream Contribution
```bash
# Start from clean upstream state
git checkout main
git checkout -b feat/shareable-feature
# ... develop following project conventions ...
git commit -m "feat: add shareable feature"
git push origin feat/shareable-feature
# Create PR to upstream
```

## Commit Message Conventions

### For Custom Commits
```
custom: general personal change
custom(component): specific component modification
private: sensitive configuration
experiment: experimental feature
```

### For Upstream Commits
Following [Conventional Commits](https://www.conventionalcommits.org/):
```
feat: new feature
fix: bug fix  
docs: documentation
chore: maintenance
refactor: code restructuring
style: formatting changes
test: test additions
perf: performance improvements
```

## Merge Strategies

| From | To | Strategy | Reason |
|------|----|---------:|--------|
| upstream | main | `--ff-only` | Keep clean history |
| main | custom/main | Regular merge | Preserve both histories |
| custom/feature | custom/main | `--no-ff` | Clear feature boundaries |
| feat/* | upstream | Via PR | Upstream review process |

## Best Practices

### DO's
- ✅ Keep `main` as clean mirror of upstream
- ✅ Regularly sync with upstream (weekly/bi-weekly)
- ✅ Use descriptive branch names
- ✅ Keep custom changes in `custom/*` branches
- ✅ Test merge compatibility before major custom changes
- ✅ Document custom features in comments
- ✅ Use atomic commits for upstream contributions

### DON'Ts
- ❌ Don't commit directly to `main`
- ❌ Don't mix custom and upstream features in same branch
- ❌ Don't force push to shared branches
- ❌ Don't squash commits when contributing upstream
- ❌ Don't forget to sync before starting new features

## Conflict Resolution

When conflicts arise during upstream sync:

1. **Identify conflict source**
   ```bash
   git status
   git diff --name-only --diff-filter=U
   ```

2. **Create resolution branch**
   ```bash
   git checkout -b merge/resolve-upstream-conflicts
   ```

3. **Resolve conflicts**
   - Keep upstream changes for shared code
   - Preserve custom features in separate files when possible
   - Document resolution decisions

4. **Test thoroughly**
   ```bash
   npm run type-check
   npm run lint
   npm run build
   npm run dev  # Manual testing
   ```

5. **Complete merge**
   ```bash
   git add .
   git commit -m "merge: resolve upstream conflicts"
   git checkout custom/main
   git merge merge/resolve-upstream-conflicts
   ```

## Maintenance Tasks

### Weekly
- [ ] Sync main with upstream
- [ ] Update custom/main from main
- [ ] Review and clean up old feature branches

### Monthly  
- [ ] Audit custom changes for upstream potential
- [ ] Update this documentation as needed
- [ ] Check for security updates

### Per Release
- [ ] Major compatibility testing
- [ ] Consider rebasing custom changes if needed
- [ ] Tag stable custom versions

## Troubleshooting

### Common Issues

**Issue**: Upstream fetch fails  
**Solution**: Check remote URL and network connection
```bash
git remote -v
git remote set-url upstream [correct-url]
```

**Issue**: Merge conflicts in custom/main  
**Solution**: See Conflict Resolution section above

**Issue**: Alias not working  
**Solution**: Check git config
```bash
git config --get-regexp alias
```

## Current Status

- **Fork**: https://github.com/code-agents/emdash-x
- **Custom Branch**: `custom/main` (created)
- **Git Aliases**: Configured ✅
- **Upstream**: Not yet configured (repository not available)

## Notes

- This workflow allows maintaining custom modifications while staying synchronized with upstream
- Custom changes remain separate for easy identification
- Selected features can be contributed back via clean PRs
- The `custom/main` branch serves as your stable base for all personal modifications

Last Updated: October 2025
