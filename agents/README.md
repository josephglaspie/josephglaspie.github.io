# Multi-Agent System for Weather GitHub Pages

This directory contains coordinating agents that work together to build and maintain a Go-based weather application that publishes to GitHub Pages.

## Agent Architecture

### Agent Roles

1. **project-setup** (Architect)
   - Role: Project architect and coordinator
   - Model: Sonnet (efficient for planning and coordination)
   - Responsibilities:
     - Define project structure and architecture
     - Initialize Go modules and tooling
     - Configure CI/CD pipelines
     - Coordinate agent workflows
     - Make architectural decisions

2. **golang-pro** (Primary Developer)
   - Role: Go application developer
   - Model: Opus (high-quality code generation)
   - Responsibilities:
     - Implement application features
     - Build HTTP clients and API integrations
     - Create data processing pipelines
     - Write comprehensive tests
     - Handle errors and edge cases

3. **code-reviewer** (Quality Assurance)
   - Role: Code quality and security expert
   - Model: Opus (thorough analysis required)
   - Responsibilities:
     - Review code for security issues
     - Analyze performance implications
     - Verify test coverage
     - Ensure Go best practices
     - Validate production readiness

## Coordination Workflow

```
project-setup (Architect)
    │
    ├──> golang-pro (Developer)
    │       │
    │       └──> code-reviewer (QA)
    │               │
    │               └──> [feedback loop]
    │
    └──> [architectural decisions]
```

### Typical Workflow

1. **Project Setup** initiates task
   - Defines requirements and architecture
   - Assigns implementation to **golang-pro**

2. **golang-pro** implements feature
   - Writes code following specifications
   - Creates comprehensive tests
   - Requests review from **code-reviewer**

3. **code-reviewer** evaluates code
   - Performs security and quality analysis
   - Provides feedback and suggestions
   - Approves or requests changes

4. **Project Setup** coordinates
   - Resolves conflicts
   - Makes architectural decisions
   - Coordinates iterations

## Using the Agents

### Load All Agents

To use these agents in Claude Code, you can reference them:

```bash
# The agents are automatically available in this project
# Each agent's responsibilities are documented in their .md file
```

### Agent Coordination Examples

**Starting a New Feature:**
```
project-setup: "Define architecture for weather data fetching"
golang-pro: "Implement weather API client with retry logic"
code-reviewer: "Review weather client for security and performance"
```

**Bug Fix Workflow:**
```
project-setup: "Investigate timeout issues in production"
golang-pro: "Add configurable timeouts to HTTP client"
code-reviewer: "Verify timeout handling and test coverage"
```

**Deployment Setup:**
```
project-setup: "Configure GitHub Actions for automated deployment"
golang-pro: "Create build and release scripts"
code-reviewer: "Review CI/CD security and best practices"
```

## Agent Coordination Protocol

### Communication Pattern

Agents coordinate through shared context:
- **project-setup** defines requirements and assigns tasks
- **golang-pro** implements and tests features
- **code-reviewer** provides feedback and approval
- All agents maintain awareness of project state

### Decision Making

- **Architectural decisions**: project-setup (with input from others)
- **Implementation details**: golang-pro (within defined architecture)
- **Quality standards**: code-reviewer (with veto power)

### Conflict Resolution

When agents disagree:
1. code-reviewer flags issue with specific concern
2. golang-pro proposes alternative solution
3. project-setup makes final architectural decision
4. All agents align on chosen approach

## Benefits of Multi-Agent Architecture

- **Separation of Concerns**: Each agent focuses on their expertise
- **Quality Assurance**: Built-in review process
- **Scalability**: Easy to add specialized agents
- **Maintainability**: Clear responsibilities and boundaries
- **Best Practices**: Agents enforce their domain standards
