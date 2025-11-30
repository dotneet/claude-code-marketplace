# Code Review Toolkit

Code review toolkit for Claude Code. Includes code review expert for various tech stacks and software development practices.

## Installation

Follow the instructions below to install the toolkit in Claude Code.

```bash
# Register the marketplace
/plugin marketplace add dotneet/claude-code-marketplace
# Install the plugin
/plugin install code-review-toolkit@dotneet-marketplace
```

## Skills

### typescript-react-reviewer

Expert code reviewer for TypeScript + React 19 applications.

**Use when:**
- Reviewing React code and PR reviews
- Identifying anti-patterns and code smells
- Evaluating state management patterns
- Assessing code maintainability
- TypeScript type safety checks

**Key features:**
- React 19 new hooks patterns (useActionState, useOptimistic, use)
- useEffect abuse detection
- State mutation detection
- TypeScript strict mode recommendations

### code-modularization-evaluator

Evaluate and improve code modularization using the Balanced Coupling Model.

**Use when:**
- Reviewing code architecture
- Refactoring modules
- Designing new systems
- Identifying coupling problems

**Key features:**
- Integration strength analysis (Intrusive/Functional/Model/Contract)
- Distance evaluation
- Volatility assessment
- Connascence type identification
- Actionable refactoring recommendations

## Usage

Once installed, these skills are automatically available in Claude Code. They will be suggested when relevant tasks are detected, or you can invoke them directly.

