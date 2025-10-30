# Project Context

## What This Project Does

[One paragraph describing the project's purpose, target users, and core value proposition]

Example:
"This is a web application that helps developers manage their API keys securely. It provides a dashboard for viewing usage, rotating keys, and setting up webhooks for key expiration events. Target users are development teams managing multiple APIs across microservices."

## Key Domains & Modules

### Core Modules
- **Module A**: [Purpose and responsibility]
  - Located in: `src/module-a/`
  - Dependencies: [what it depends on]
  - Used by: [what depends on it]

- **Module B**: [Purpose and responsibility]
  - Located in: `src/module-b/`
  - Key patterns: [architectural patterns used]

### Data Models
- **Model X**: Represents [concept], stored in [location]
- **Model Y**: Represents [concept], relationships: [describe]

### External Integrations
- **Service A**: API for [purpose], auth via [method]
- **Database**: [type], schema location: [path]

## How to Run

### Setup
```bash
make setup  # or: npm install, pip install -r requirements.txt, etc.
```

### Development Server
```bash
make run  # or: npm start, python manage.py runserver, etc.
# Runs on: http://localhost:3000
```

### Tests
```bash
make test  # or: npm test, pytest, go test, etc.
```

### Linting & Formatting
```bash
make lint     # Check code style
make fmt      # Auto-format code
make typecheck # Type checking
```

### Build & Deploy
```bash
make build    # Production build
make deploy   # Deploy to production
```

## Architecture Highlights

### Key Design Decisions
- [Decision 1]: [rationale]
- [Decision 2]: [rationale]

### Data Flow
[Describe how data flows through the system - request → service → database → response]

### State Management
[How state is managed - Redux, Context API, database, etc.]

## Known Tricky Areas

### Gotchas
- **Area 1**: [Why it's tricky] - [How to handle it]
  - Example: "The auth middleware must be applied in this specific order because..."
  
- **Area 2**: [Context]
  - Common mistake: [what people get wrong]
  - Correct approach: [how to do it right]

### Technical Debt
- [Known issue 1]: [impact, plan to fix]
- [Known issue 2]: [context]

## Important Files & Locations

- Entry point: `src/main.ts` / `src/index.js` / etc.
- Config: `.env`, `config/`, etc.
- Tests: `tests/`, `__tests__/`, `*.test.*`
- Documentation: `docs/`, `README.md`

## Links & Resources

- Architecture diagram: [link or path]
- API documentation: [link]
- Design system: [link]
- Deployment docs: [link]

