---
name: gen-context
description: Generate adaptive boilerplate context files from a completed PRD. Reads the PRD's Project Type section and outputs only the relevant context markdown files (under 200 lines each) saved in a context/ folder. Use this skill immediately after the PRD is finalized, before starting to code.
---

# Context Generator

You are a senior software architect. Given a completed PRD, generate a set of concise context files that serve as the coding reference for this project. These files will live in a `context/` folder and be used as AI context during development.

## Step 1 — Read Project Type

First, extract these fields from the PRD's **Section 0: Project Type**:
- `Type` (REST API, Frontend App, Fullstack, CLI Tool, Library, Serverless, Mobile)
- `Architecture` (Monolith, Microservices, Serverless, JAMstack)
- `Has Controller Layer` (Yes / No)
- `Has Auth` (Yes / No)

---

## Step 2 — Determine Which Files to Generate

Use this matrix to decide which files to generate:

| File | REST API | Frontend | Fullstack | CLI | Library | Serverless | Mobile |
|------|----------|----------|-----------|-----|---------|------------|--------|
| `structure.md` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `data-model.md` | ✅ | ⚠️ | ✅ | ⚠️ | ⚠️ | ✅ | ✅ |
| `api-contract.md` | ✅ | ❌ | ✅ | ❌ | ❌ | ✅ | ⚠️ |
| `controller.md` | if Yes | ❌ | if Yes | ❌ | ❌ | ❌ | ❌ |
| `service.md` | ✅ | ❌ | ✅ | ⚠️ | ✅ | ✅ | ✅ |
| `auth.md` | if Yes | if Yes | if Yes | ❌ | ❌ | if Yes | if Yes |
| `error-handling.md` | ✅ | ⚠️ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `component.md` | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ |
| `state.md` | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ |

> ✅ Always generate | ⚠️ Generate only if relevant to the project | ❌ Skip

---

## Step 3 — Generate Each File

For each file that should be generated, follow the template below. **Each file must stay under 200 lines.**

---

### `context/structure.md`
```
# Project Structure

## Folder Layout
[ASCII tree of the recommended folder/file structure]

## Layer Responsibilities
Brief explanation of what each major folder/layer is responsible for.

## Naming Conventions
- Files: [kebab-case / camelCase / snake_case]
- Functions/Methods: [camelCase / snake_case]
- Classes: [PascalCase]
- Constants: [UPPER_SNAKE_CASE]
- Database tables: [snake_case / PascalCase]
```

---

### `context/data-model.md`
```
# Data Model

## Entities & Fields
[List each entity with its fields, types, and constraints]

Entity: [Name]
- field_name: type — description (constraints: nullable, unique, etc.)

## Relationships
[Describe how entities relate to each other]
- User has many Orders (1:N)
- Order has many Products through OrderItems (M:N)

## Notes
[Any important rules about data integrity, soft deletes, timestamps, etc.]
```

---

### `context/api-contract.md`
```
# API Contract

## Base URL
[Base URL pattern, e.g. /api/v1]

## Response Format
[Standard response envelope structure]

Success:
{
  "success": true,
  "data": { ... }
}

Error:
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message"
  }
}

## Endpoints

### [Resource Name]
| Method | Path | Description | Auth Required |
|--------|------|-------------|---------------|
| GET | /resource | List all | Yes/No |
| POST | /resource | Create new | Yes/No |
| GET | /resource/:id | Get by ID | Yes/No |
| PUT | /resource/:id | Update | Yes/No |
| DELETE | /resource/:id | Delete | Yes/No |

### Request & Response Examples
[Show request body and response shape for the most important endpoints]
```

---

### `context/controller.md`
*(Only if Has Controller Layer: Yes)*
```
# Controller Pattern

## Responsibilities
- Receive and validate incoming request
- Call the appropriate service method
- Return formatted response
- Do NOT contain business logic

## Structure Pattern
[Show the standard controller function/class pattern for this project]

## Input Validation
[How inputs are validated — schema validation, manual checks, etc.]

## Error Handling in Controllers
[How errors from services are caught and returned]

## Example
[A concrete example of a complete controller method]
```

---

### `context/service.md`
```
# Service Layer Pattern

## Responsibilities
- Contains all business logic
- Interacts with the database/repository layer
- Does NOT handle HTTP request/response
- Throws errors for invalid operations

## Structure Pattern
[Show the standard service function/class pattern for this project]

## Example
[A concrete example of a complete service method including error throwing]
```

---

### `context/auth.md`
*(Only if Has Auth: Yes)*
```
# Auth Pattern

## Method
[JWT / Session / OAuth / API Key — from PRD]

## Auth Flow
[Step-by-step auth flow: login → token → protected route]

## Middleware / Guard Pattern
[How auth is enforced on protected routes]

## Token Structure (if JWT)
Payload:
- sub: user ID
- role: user role
- iat / exp: timestamps

## Permission Levels
[List roles and what they can access]
```

---

### `context/error-handling.md`
```
# Error Handling

## Error Format
[Standard error response shape]

## Error Codes
| Code | HTTP Status | Description |
|------|-------------|-------------|
| VALIDATION_ERROR | 400 | Invalid input |
| UNAUTHORIZED | 401 | Not authenticated |
| FORBIDDEN | 403 | Not permitted |
| NOT_FOUND | 404 | Resource not found |
| INTERNAL_ERROR | 500 | Unexpected server error |

## Error Throwing Pattern
[How errors are created and thrown in service/controller layer]

## Logging
[What gets logged and at what level: info, warn, error]
```

---

### `context/component.md`
*(Frontend / Fullstack / Mobile only)*
```
# Component Pattern

## Component Types
- **Page / Screen**: top-level route components
- **Feature Component**: business logic components
- **UI Component**: reusable, stateless presentational components

## Naming & File Structure
[How components are named and organized]

## Props Pattern
[How props/inputs are typed and passed]

## Example
[A concrete example of a feature component]
```

---

### `context/state.md`
*(Frontend / Fullstack / Mobile only)*
```
# State Management

## State Layers
- **Local state**: component-level (form inputs, toggles)
- **Feature state**: shared within a feature
- **Global state**: app-wide (auth user, theme, etc.)

## Pattern
[How state is managed — Context API, Zustand, Redux, Pinia, etc. from PRD]

## Data Fetching Pattern
[How API calls are made and cached — React Query, SWR, raw fetch, etc.]

## Example
[Concrete example of a state slice or store]
```

---

## Step 4 — Output Format

Present each file clearly separated like this:

```
## context/structure.md
[file content]

---

## context/data-model.md
[file content]

---
```

End with a summary:
```
## Generated Files
- context/structure.md
- context/data-model.md
- ... (list all generated files)

## Skipped Files
- context/controller.md — not applicable (no controller layer)
- ... (explain why each was skipped)
```

---

## Guidelines

- **Stay under 200 lines per file** — be concise, use examples over long explanations
- **Be specific to the PRD** — use actual entity names, endpoint names, and tech stack from the PRD, not generic placeholders
- **Examples are mandatory** — every pattern file must have at least one concrete example
- **Framework-agnostic** — show patterns in pseudocode or language-specific but not framework-specific code unless the PRD specifies a framework
- **Consistent with PRD** — never contradict what's already decided in the PRD
