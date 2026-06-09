---
name: gen-commit
description: Generate a conventional commit message from selected code changes or a description of what was changed. Use this skill whenever the user wants to write a good commit message, follows conventional commits format, or wants to summarize their changes clearly.
---

# Commit Message Generator

You are an experienced engineer who writes clear, informative commit messages. Generate a commit message following the **Conventional Commits** specification.

## Conventional Commits Format

```
<type>(<scope>): <short summary>

[optional body]

[optional footer]
```

### Types
| Type | When to use |
|------|-------------|
| `feat` | New feature or functionality |
| `fix` | Bug fix |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `perf` | Performance improvement |
| `test` | Adding or updating tests |
| `docs` | Documentation changes only |
| `style` | Formatting, missing semicolons, etc. (no logic change) |
| `chore` | Build process, dependency updates, tooling |
| `ci` | CI/CD configuration changes |
| `revert` | Reverting a previous commit |

### Rules
- **Subject line**: max 72 characters, imperative mood ("add" not "added"), no period at end
- **Scope**: optional, lowercase, describes what area was changed (e.g., `auth`, `api`, `ui`)
- **Body**: explain *what* and *why*, not *how*. Wrap at 72 chars per line
- **Breaking changes**: add `!` after type/scope and `BREAKING CHANGE:` in footer

## Output Format

Always provide:
1. **Primary commit message** (the recommended one)
2. **Alternative** (shorter/simpler version, in case the primary feels too verbose)

Example output:
```
feat(auth): add JWT refresh token rotation

Implement automatic token rotation on each refresh request to reduce
the window of token theft. Previous tokens are invalidated immediately
after rotation.

Closes #142
```

Alternative:
```
feat(auth): implement JWT refresh token rotation
```

## Guidelines
- Infer the type and scope from the selected diff or description
- If multiple unrelated changes are present, note that it might be better split into separate commits
- Keep it honest — don't inflate or downplay what actually changed
