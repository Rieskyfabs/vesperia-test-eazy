# AGENTS.md

## 1. Project Overview

**Project Name:** Eazy Forms  
**Project Type:** Full-Stack Web Application  
**Purpose:** Vesperia Software Engineer Technical Assessment

Eazy Forms is a JSON-driven form application built with Laravel and React.

The application must consume a provided JSON feed, persist the data in a database, expose the stored data through backend APIs, dynamically render a form on the frontend, and submit form responses through the API.

The implementation must prioritize correctness, maintainability, appropriate database design, and memory efficiency over visual complexity.

## 2. Source of Truth

The following files are authoritative:

- `README.md` — Primary source of truth for project requirements, setup instructions, architecture, and implementation decisions.
- `submission.json` — Source data provided for the technical assessment.
- `AGENTS.md` — Instructions governing AI coding agent behavior.

### Mandatory Reading Order

Before implementing any feature or modifying existing code, the agent MUST:

1. Read `README.md` completely.
2. Locate and inspect `submission.json`.
3. Inspect the existing project structure and relevant source files.
4. Identify the actual requirements and constraints.
5. Check existing implementations before proposing changes.
6. Follow the established architecture and conventions.

Do not assume that undocumented features are required.

If `README.md` or `submission.json` is missing or unreadable, report the issue rather than inventing its contents.

If instructions conflict, preserve the original assessment requirements and ask for clarification before making consequential changes.

## 3. Technical Assessment Requirements

### Mandatory Requirements

The application must:

1. Provide a Laravel backend application written in PHP.
2. Consume the provided JSON feed.
3. Persist the feed data into a database.
4. Store JSON data in a well-formed way with appropriate indexes.
5. Expose persisted data through backend APIs.
6. Provide a frontend that consumes the backend API.
7. Dynamically display the form described by the provided data.
8. Submit completed form responses to the backend API.
9. Consider memory usage during data processing and application execution.

### Nice-to-Have Requirements

- Unit tests.
- Database migrations.

### Evaluation Priorities

Prioritize:

1. Functional correctness.
2. Backend architecture.
3. Database structure and indexing.
4. JSON processing.
5. API design and validation.
6. Memory efficiency.
7. Code maintainability.
8. Automated testing.

Frontend visual design is not evaluated. A minimal, usable interface is sufficient.

## 4. Technology Stack

### Backend

- PHP
- Laravel
- Laravel Eloquent ORM
- RESTful APIs

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS (optional for minimal styling)

### Database

- PostgreSQL
- JSONB where appropriate
- Database indexes based on actual query patterns

### Testing

- PHPUnit or Pest
- Laravel feature tests
- Frontend testing only when practical

These technologies represent the preferred implementation approach. Follow the actual project configuration and README.md when they differ.

Do not introduce unnecessary frameworks or dependencies.

## 5. JSON Feed — submission.json

The provided `submission.json` is the source data for the assessment.

The agent MUST inspect its actual contents before designing the implementation.

### JSON Analysis

Determine:

- Top-level JSON structure.
- Whether the root is an object or array.
- Nested objects and arrays.
- Field names and data types.
- Form definitions and field metadata, if present.
- Required and optional fields.
- Unique identifiers.
- Relationships between records.
- Expected validation rules.
- Potentially large collections.
- Missing, null, or unexpected values.

Do not assume the JSON structure.

Do not invent fields, relationships, validation rules, or business requirements.

### JSON Processing

- Preserve the original meaning and relevant structure of the JSON data.
- Validate the JSON before persistence.
- Handle malformed input gracefully.
- Avoid unnecessary data transformations.
- Prevent duplicate imports when appropriate.
- Consider streaming or batch processing for large datasets.
- Avoid loading large files entirely into memory when a streaming approach is justified.
- Keep the original JSON file unchanged.

### Important

The frontend must obtain form data through Laravel APIs.

Do not import or directly consume `submission.json` from the React frontend.

The database, populated by the Laravel importer, must serve as the application's data source.

## 6. Architecture Guidelines

Use a simple and maintainable architecture.

Recommended responsibilities:

### Laravel Backend

- JSON feed ingestion.
- Data validation.
- Database persistence.
- Form retrieval.
- Submission processing.
- API responses.
- Error handling.

### PostgreSQL Database

- Persist imported JSON data.
- Store form definitions and submissions as appropriate.
- Maintain suitable indexes.
- Preserve necessary identifiers and metadata.

### React Frontend

- Fetch form definitions through the API.
- Render form fields dynamically.
- Manage user input.
- Validate inputs where appropriate.
- Submit responses to the API.
- Display loading, success, and error states.

Avoid unnecessary abstraction.

Only introduce services, repositories, or additional architectural layers when they provide a clear benefit.

## 7. Backend Development Guidelines

Follow Laravel conventions and PSR-12 coding standards.

### Controllers

- Keep controllers focused on HTTP responsibilities.
- Validate incoming requests.
- Delegate complex logic to dedicated classes when appropriate.
- Return consistent JSON responses.
- Use appropriate HTTP status codes.

### Services

Use service classes for complex operations such as:

- JSON feed importing.
- Data transformation.
- Form schema processing.
- Submission processing.

Do not create service classes for trivial operations.

### Validation

- Validate request payloads on the backend.
- Derive form-specific validation rules from the actual schema where applicable.
- Reject malformed or invalid submissions.
- Do not rely exclusively on frontend validation.

### Error Handling

- Handle expected errors gracefully.
- Avoid exposing sensitive internal details.
- Return meaningful validation and error messages.
- Log relevant failures without logging secrets.

### Security

- Never trust client input.
- Avoid mass-assignment vulnerabilities.
- Use parameterized queries or Eloquent.
- Do not expose sensitive configuration.
- Apply appropriate CORS configuration for local frontend development.

## 8. Database Guidelines

Use PostgreSQL with JSONB where appropriate.

### Schema Design

- Analyze the JSON feed before creating tables.
- Design tables according to actual data relationships.
- Use appropriate primary keys.
- Preserve original identifiers when necessary.
- Use timestamps where appropriate.
- Avoid unnecessary data duplication.

### JSON Storage

- Store JSON documents using JSONB when suitable.
- Preserve relevant JSON structures and metadata.
- Do not normalize every JSON field into separate columns without a clear reason.
- Do not store all data in one unstructured table if meaningful relationships require otherwise.

### Indexing

- Index frequently queried identifiers and foreign keys where appropriate.
- Consider GIN indexes only when JSONB query patterns justify them.
- Avoid excessive indexes that increase write overhead.
- Explain significant indexing decisions in the README.

### Migrations

Prefer Laravel migrations for reproducible database setup.

Do not require reviewers to manually create database tables.

## 9. API Design Guidelines

Build RESTful APIs based on the actual JSON structure and application requirements.

Potential endpoints may include:

- `GET /api/forms`
- `GET /api/forms/{id}`
- `POST /api/forms/{id}/submissions`

These are examples, not mandatory endpoint contracts.

The final API design must follow the actual form structure and README.md.

### API Requirements

- Return valid JSON.
- Use appropriate HTTP status codes.
- Validate submission data.
- Handle missing resources.
- Provide consistent error responses.
- Avoid returning unnecessary data.
- Keep endpoint behavior predictable.

Do not invent additional endpoints unless necessary.

## 10. Frontend Development Guidelines

Use React with TypeScript.

### Dynamic Form Rendering

The frontend must:

1. Fetch the form definition from Laravel.
2. Interpret the returned form structure.
3. Render supported input fields dynamically.
4. Handle user input and state.
5. Apply validation based on the actual form definition.
6. Submit the completed form to Laravel.
7. Display submission results.

### Component Design

- Use functional components.
- Keep components focused and reusable.
- Avoid excessive component abstraction.
- Use TypeScript types for API responses and form data.
- Avoid hardcoded form definitions.
- Avoid unnecessary state management libraries.

### UI Requirements

- Keep the interface simple and functional.
- Provide accessible labels.
- Show loading and error states.
- Display validation messages.
- Prevent accidental duplicate submissions where practical.
- Prioritize usability over visual polish.

Do not spend unnecessary time on animations, branding, or advanced styling.

## 11. Performance and Memory Efficiency

Memory usage is an explicit requirement of the assessment.

The agent MUST consider memory efficiency throughout the implementation.

### JSON Importing

- Inspect feed size and structure before choosing a parser.
- Avoid loading large JSON files entirely into memory when possible.
- Consider streaming parsers for large JSON feeds.
- Process large collections incrementally.
- Use batch inserts where appropriate.
- Avoid unnecessary intermediate arrays and object copies.

### Database

- Select only required columns.
- Use efficient queries.
- Avoid N+1 query problems.
- Use appropriate indexes.
- Avoid unnecessary eager loading.
- Use pagination or chunking for large result sets where applicable.

### API

- Avoid returning excessive payloads.
- Minimize unnecessary serialization.
- Use efficient database retrieval patterns.

### Frontend

- Avoid unnecessary re-renders.
- Keep form state management straightforward.
- Avoid duplicating large data structures.
- Do not introduce optimization libraries without a demonstrated need.

Prefer measured improvements over premature optimization.

## 12. Testing Guidelines

Automated tests are desirable and should be implemented when practical.

### Backend Tests

Prioritize testing:

- JSON feed ingestion.
- Successful database persistence.
- Invalid or malformed JSON handling.
- Form retrieval APIs.
- Successful form submissions.
- Submission validation errors.
- Missing resources.
- Relevant edge cases.

### Testing Rules

- Use Laravel testing conventions.
- Keep tests deterministic.
- Avoid dependencies on external services.
- Use test fixtures where appropriate.
- Run relevant tests after implementation.
- Do not claim tests passed unless they were executed.

Document testing commands in README.md.

## 13. Documentation Guidelines

README.md must remain accurate and useful to reviewers.

Document:

- Project overview.
- Technology stack.
- Prerequisites.
- Installation instructions.
- Environment configuration.
- Database setup.
- Migration commands.
- JSON feed import commands.
- Backend startup commands.
- Frontend startup commands.
- API endpoint documentation.
- Testing instructions.
- Architectural decisions.
- Memory-efficiency considerations.
- Known limitations.

### Documentation Rules

- Update README.md when setup or behavior changes.
- Do not document features that are not implemented.
- Keep instructions reproducible.
- Do not include real credentials or secrets.
- Provide working commands based on the actual repository.

## 14. Repository Structure

A possible project structure is:

```text
eazy-forms/
├── AGENTS.md
├── README.md
├── answers.md
├── submission.json
├── backend/
│   ├── app/
│   ├── database/
│   ├── routes/
│   └── tests/
├── frontend/
│   ├── src/
│   └── package.json
└── .gitignore
```

This structure is a recommendation, not a strict requirement.

Inspect the existing repository before creating or moving directories.

Do not restructure existing code without a clear reason.

## 15. Agent Workflow

For every development task, follow this process.

### Step 1 — Understand

- Read README.md.
- Inspect submission.json when relevant.
- Review existing implementation.
- Identify requirements and constraints.

### Step 2 — Plan

- Determine the smallest valid implementation.
- Identify affected files.
- Consider database and API implications.
- Consider memory usage.
- Avoid unnecessary complexity.

### Step 3 — Implement

- Follow existing conventions.
- Keep code readable.
- Make focused changes.
- Avoid modifying unrelated files.
- Add validation and error handling.

### Step 4 — Verify

- Run relevant tests.
- Check API behavior.
- Verify database persistence.
- Confirm frontend integration.
- Review memory-related concerns.
- Report any unverified behavior.

### Step 5 — Document

- Update README.md when needed.
- Explain important technical decisions.
- Record known limitations.

### Step 6 — Report

Provide a concise summary covering:

- What was implemented.
- Which files were changed.
- What was tested.
- Whether tests passed.
- Any remaining issues.

## 16. Restrictions

The agent MUST NOT:

- Ignore README.md.
- Assume the structure of submission.json.
- Invent assessment requirements.
- Hardcode form fields that should be data-driven.
- Modify the original JSON feed without authorization.
- Introduce unnecessary dependencies.
- Overengineer the architecture.
- Prioritize UI polish over functional correctness.
- Expose secrets or credentials.
- Modify unrelated files.
- Claim successful testing without execution.
- Introduce unrelated product features.

## 17. Definition of Done

The technical assessment is complete when:

- Laravel successfully consumes the provided JSON feed.
- The data is persisted in the database.
- JSON storage and indexing are appropriate.
- Backend APIs expose the stored data.
- React retrieves form definitions through the API.
- Forms are rendered dynamically.
- Form submissions reach the backend API and are processed correctly.
- Memory efficiency has been considered.
- The application can be run locally using README.md.
- Relevant tests have been run, with results documented.
- Any known limitations are clearly communicated.

Migrations and automated tests should be included where practical.

## 18. Final Principles

Always prioritize:

1. Correctness.
2. Simplicity.
3. Maintainability.
4. Memory efficiency.
5. Security.
6. Clear documentation.
7. Appropriate testing.

Build only what is necessary to satisfy the assessment.

**README.md is the primary project instruction document.**

**submission.json is the authoritative source data.**

**AGENTS.md governs how the coding agent approaches implementation.**