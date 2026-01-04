<!--
Sync Impact Report:
- Version: NONE → 1.0.0 (Initial constitution)
- Rationale: Initial creation - MINOR bump from 0.0.0 baseline for first complete governance
- Modified principles: N/A (new creation)
- Added sections:
  * Core Principles: I. Simplicity & YAGNI, II. Observability First, III. CLI-First Design
  * Development Workflow: Implementation Process, Quality Gates, Forbidden Patterns
  * Governance: Amendment Process, Compliance, Living Document
- Removed sections: N/A
- Templates updated:
  ✅ .specify/templates/plan-template.md - Added Constitution Check section with all three principles as checkable gates
  ✅ .specify/templates/spec-template.md - Added CLI Interface Requirements section referencing Principle III
  ✅ .specify/templates/tasks-template.md - Reviewed, already aligned (incremental structure supports simplicity)
  ✅ .claude/commands/*.md - Reviewed, no generic guidance issues (agent context references are legitimate)
  ✅ README.md - Reviewed, minimal content, no updates needed
- Follow-up TODOs: None
-->

# Groceries CLI Constitution

## Core Principles

### I. Simplicity & YAGNI (You Ain't Gonna Need It)

**Rule**: Build only what is explicitly needed right now. No speculative features, no premature abstractions, no "just in case" code.

**This means**:
- Three similar lines of code are better than a premature abstraction
- No helper functions or utilities until needed in at least 2-3 places
- No configuration options for hypothetical future use cases
- No framework patterns (repository, factory, strategy) unless the problem actually requires them
- Delete unused code completely - no commenting out, no "just in case" retention
- If a feature isn't in the current spec, don't build it

**Rationale**: Complexity is the enemy of maintainability. Every abstraction has a cost. The simplest solution that works is the right solution. Future requirements will guide future refactoring when they actually arrive.

### II. Observability First

**Rule**: The system MUST make it easy to understand what it's doing, what went wrong, and why.

**This means**:
- Text-based I/O: stdin/args → stdout for results, stderr for errors and diagnostics
- Support both JSON output (for automation) and human-readable output (for debugging)
- Log key operations with context: what happened, when, why (if relevant)
- Error messages MUST be actionable: what failed + what the user should do
- No silent failures - every error path MUST be observable
- Include diagnostic flags (--verbose, --debug) for troubleshooting

**Rationale**: CLI tools are often used in automation and scripts. When things fail at 3am, clear logs and error messages are the difference between a 5-minute fix and a 5-hour debug session.

### III. CLI-First Design

**Rule**: Every feature MUST be accessible via command-line interface with clear, predictable behavior.

**This means**:
- Commands follow standard Unix conventions (flags, options, arguments)
- Exit codes: 0 for success, non-zero for failure (with distinct codes for different failure types)
- Commands are composable: output of one can be input to another (pipe-friendly)
- Help text MUST be clear, with examples for common use cases
- Sane defaults for common scenarios, explicit flags for advanced use
- No interactive prompts in scripts - all required input via flags or stdin
- Support --dry-run or --preview for destructive operations

**Rationale**: CLI tools are the building blocks of automation. They must be predictable, composable, and scriptable. Users should never have to read source code to understand how to use the tool.

## Development Workflow

### Implementation Process

1. **Feature Specification**: Every feature starts with a spec.md defining user scenarios and requirements
2. **Implementation Plan**: Create plan.md with technical approach and file structure
3. **Incremental Development**: Build the simplest thing that works, then iterate only if needed
4. **Manual Testing**: Verify the CLI works as expected with real commands
5. **Documentation**: Update help text, README examples, and usage docs

### Quality Gates

- **Clarity Check**: Can a new user understand what this command does from --help alone?
- **Simplicity Check**: Is this the simplest solution? What complexity can be removed?
- **Observability Check**: If this fails, will the error message tell users what to do?
- **Composability Check**: Can this be used in a script or pipeline?

### Forbidden Patterns

- **No speculative features**: If it's not in the current spec, don't build it
- **No premature optimization**: Don't optimize until you have evidence of a problem
- **No hidden behavior**: Every feature MUST be documented and accessible via CLI
- **No magic**: Explicit is better than implicit. No auto-detection unless absolutely necessary.

## Governance

### Amendment Process

1. Proposed changes MUST include justification: what problem does this solve?
2. Constitutional changes require updating all dependent templates and workflows
3. Version bump MUST follow semantic versioning:
   - **MAJOR**: Removing or fundamentally changing a principle
   - **MINOR**: Adding a new principle or section
   - **PATCH**: Clarifications, wording fixes, non-semantic changes

### Compliance

- All PRs and code reviews MUST verify compliance with these principles
- Any violation MUST be explicitly justified and documented
- Complexity MUST be justified: why is the simple solution insufficient?
- This constitution supersedes all other development practices

### Living Document

- Review constitution relevance when project direction changes
- Principles should reflect actual project values, not aspirational ideals
- Update immediately when principles prove impractical or harmful

**Version**: 1.0.0 | **Ratified**: 2026-01-03 | **Last Amended**: 2026-01-03
