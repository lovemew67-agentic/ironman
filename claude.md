<!-- https://github.com/lovemew67/claude-code-agents -->

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an AI agent development framework designed for collaborative software engineering workflows. The project uses a specialized agent-based approach where different AI agents handle distinct phases of development:

- **Strategic Planning**: Feature analysis and technical design
- **Task Execution**: Precise, step-by-step implementation
- **Code Review**: Quality assurance and security validation
- **Architecture Analysis**: Project structure and documentation

## Agent Architecture

### Core Agent Types

The system defines specialized agents in `/draft/`:

- `@strategic-planner`: Requirements analysis, technical design, and task planning (no code execution)
- `@task-executor`: Surgical precision implementation of individual tasks from task lists
- `@code-reviewer`: Post-implementation quality and security review
- `@steering-architect`: Project analysis and core documentation creation

### Agent Interaction Pattern

1. **Project Initialization**: `@steering-architect` analyzes codebase and creates `.docs/` foundation
2. **Feature Planning**: `@strategic-planner` creates specifications in `specs/<feature>/`
3. **Implementation**: `@task-executor` executes tasks from `specs/<feature>/tasks.md`
4. **Quality Assurance**: `@code-reviewer` reviews all code changes

## Project Structure

```
.
├── personas/              # Agent definitions and specifications
│   ├── code-reviewer.md   # Code review agent spec
│   ├── task-executor.md   # Implementation agent spec
│   ├── strategic-planner.md # Planning agent spec
│   └── steering-architect.md # Architecture agent spec
└── READMD.md              # Project workflow documentation
```

### Expected Structure for Projects Using This Framework

```
.
├── .docs/                 # Global project context
│   ├── product.md         # Project vision and goals
│   ├── tech.md           # Technology stack and tools
│   └── structure.md      # File structure conventions
└── specs/                # Feature-specific specifications
    └── <feature-name>/
        ├── requirements.md # User stories and acceptance criteria
        ├── design.md      # Technical architecture
        └── tasks.md       # Step-by-step implementation plan
```

## Key Workflow Principles

## Primary Directives

- Strictly Grounded Responses: The AI's analysis and answers MUST be based **only** on the following sources:
    1. The actual, current implementations in the codebase.
    2. Information provided directly by the user to fill gaps in the codebase analysis.
- Verification Required: Any information provided by the user MUST be verified against the actual codebase implementation before being adopted or used in an analysis.
-  Ground All Claims in Code: The AI may use its general knowledge to structure responses and understand concepts, but all specific claims, implementation details, and factual statements about the codebase MUST be derived directly from the code itself, not from assumptions or external knowledge.

## Research and Analysis Protocol

When faced with an unknown topic, component, or function, the AI MUST follow this exact procedure:

1. Inquire: Ask the user for questions to gather more information or context. The user's answer may be a high-level pointer.
2. Locate: Use the user's input and search tools to locate the target implementation in the codebase.
3. Map: Identify all callers of the target and the components that use it.
4. Analyze & Synthesize: Analyze how the target is used by its callers to develop a set of concrete use cases.
5. Review: Present the synthesized use cases to the user for review and validation, adhering strictly to the Primary Directives. 

### Task Execution Rules

When using `@task-executor`:
- Execute ONE task at a time with surgical precision
- Never anticipate or combine future steps
- Mark tasks complete only after successful testing
- Update `tasks.md` checkbox from `[ ]` to `[x]` upon completion
- Manual tests require user confirmation before proceeding

### Autonomous Mode

Task executor supports autonomous mode when explicitly requested:
- Skip user review requirements
- Continue to next task automatically
- Stop only for unresolvable errors

### Code Quality Standards

All code changes must pass through `@code-reviewer` which checks:
- Code simplicity and readability
- Clear naming conventions
- No code duplication
- Proper error handling
- No exposed secrets or API keys
- Input validation implementation
- Test coverage adequacy
- Performance considerations

## Agent Invocation Examples

```bash
# Project initialization
"@steering-architect analyze existing codebase and create project guidance files"

# Feature planning
"@strategic-planner plan user authentication feature"

# Task execution
"@task-executor execute specs/user-authentication/tasks.md tasks"

# Code review
"@code-reviewer review recent changes" # Must be used after code modifications
```

## Development Guidelines

### File Management
- Prefer editing existing files over creating new ones
- Never create documentation files unless explicitly requested
- Follow established project conventions and patterns

### Security
- Never expose secrets, API keys, or sensitive information
- Implement proper input validation
- Follow security best practices in all implementations

### Testing
- All automated tests must pass before task completion
- Manual tests require explicit user confirmation
- Do not clean up test data for database tests

## Important Notes

- This framework uses Chinese language documentation for agent specifications
- The `READMD.md` filename appears to be intentional (not a typo)
- No build, test, or lint commands are defined at the framework level (these would be project-specific)
- The framework emphasizes collaborative, spec-driven development methodology

## Context Optimization

### llms.txt Integration
The framework includes an `@llms-txt-generator` agent that creates standardized llms.txt files following the llmstxt.org specification. This improves Claude Code's ability to quickly understand projects:

- **Location**: Projects should have an `llms.txt` file at the root
- **Purpose**: Provides concise project overview for LLM context efficiency
- **Usage**: Run `@llms-txt-generator create llms.txt` after project initialization
- **Benefits**: Faster comprehension, reduced token usage, standardized summaries

When working with this framework:
1. First check if `llms.txt` exists for quick project understanding
2. Use `.docs/` for detailed specifications
3. Update `llms.txt` when major changes occur

## Tools for Claude Code

- You can use `gemini -p "xxx"` to call the Gemini CLI tool. The Gemini CLI has a large context window, so you can use it to search project code, look up information online, etc. However, it must not be used to modify or delete files.
    - Example:  
        - Bash (`gemini -p "Find where xAI is used in the project"`)
- You can use `codex "xxx"` to call the Codex CLI tool. The OpenAI Codex CLI is an coding agent that can read, modify, and run code on your local machine to help you build features faster, squash bugs, and understand unfamiliar code. However, it must not be used to modify or delete files.
    - Example:  
        - Bash (`codex "Find where xAI is used in the project"`)
- You can use `cursor-agent chat "xxx"` to call the Cursor Agent CLI tool. The Cursor Agent CLI is a command-line interface that allows users to interact with Cursor's AI coding agents directly from their terminal. It provides a way to leverage AI assistance for coding tasks without needing to use the Cursor IDE. However, it must not be used to modify or delete files. 
    - Example:  
        - Bash (`cursor-agent chat "Find where xAI is used in the project"`)
- You can use `gh copilot suggest "xxx"` to use Copilot with the Github CLI tool. The Copilot with the GitHub CLI is a tool to get suggestions and explanations for the command line. However, it must not be used to modify or delete files.
    - Example:  
        - Bash (`gh copilot suggest "undo the last commit"`)
