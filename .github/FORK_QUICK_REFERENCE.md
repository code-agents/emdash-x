# Fork Workflow - Quick Reference

## 🚀 Quick Commands (Git Aliases)

```bash
git new-custom my-feature     # Start custom feature
git new-upstream cool-feature # Start upstream contribution
git update-custom             # Sync custom/main with main
git sync-upstream            # Sync main with upstream (when available)
git branch-status           # See all branch tracking info
git custom-log             # View custom branch history
```

## 📁 Branch Naming

| Type | Pattern | Example | Purpose |
|------|---------|---------|---------|
| **Custom** | `custom/*` | `custom/dark-theme` | Your features |
| **Upstream** | `feat/*` | `feat/api-enhancement` | To contribute |
| **Fixes** | `fix/*` | `fix/memory-leak` | Bug fixes |
| **Private** | `private/*` | `private/api-keys` | Sensitive |

## 🔄 Daily Workflow

### Working on YOUR features:
```bash
git new-custom my-feature
# ... code ...
git add .
git commit -m "custom: describe change"
git checkout custom/main
git merge custom/my-feature
git push
```

### Contributing upstream:
```bash
git new-upstream feature-name
# ... code following their standards ...
git add .
git commit -m "feat: describe change"  # Use their conventions!
git push
# Open PR to upstream
```

## ✅ Commit Prefixes

**Your commits:** `custom:`, `private:`, `experiment:`  
**Upstream commits:** `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`

## 🌿 Branch Structure
```
main              → mirrors upstream
custom/main       → your stable custom code
custom/*          → your features
feat/*, fix/*     → for upstream PRs
```

## 📝 Remember
- Never commit directly to `main`
- Keep custom changes in `custom/*`
- Use upstream conventions for PRs
- Sync weekly with upstream
