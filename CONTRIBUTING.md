# Contributing to Squad Engineering

Thank you for your interest in contributing to Squad Engineering! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [Getting Started](#getting-started)
3. [Development Process](#development-process)
4. [Contribution Guidelines](#contribution-guidelines)
5. [Squad Engineering Principles](#squad-engineering-principles)
6. [Pull Request Process](#pull-request-process)
7. [Code Standards](#code-standards)
8. [Testing](#testing)
9. [Documentation](#documentation)
10. [Community](#community)

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment. We expect all contributors to:

- Be respectful and considerate in communication
- Welcome newcomers and help them get started
- Focus on constructive criticism and solutions
- Respect differing viewpoints and experiences

## Getting Started

1. **Fork the Repository**
   ```bash
   git clone https://github.com/[your-username]/squad-engineering.git
   cd squad-engineering
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Set Up Development Environment**
   - Ensure you have Node.js 18+ installed
   - Configure your IDE to follow the project's code style
   - Read through the Squad Engineering documentation in `.squad/`

## Development Process

### 1. Understanding Squad Engineering

Before contributing, familiarize yourself with:
- The Squad Engineering workflow in `docs/workflows/`
- Role definitions in `.squad/role-definition-*.md`
- Current features in `.squad/features/`

### 2. Creating an Issue

Before starting work:
1. Check existing issues to avoid duplicates
2. Create a new issue describing:
   - The problem or feature
   - Your proposed solution
   - Expected outcomes

### 3. Working on Features

For new features:
1. Discuss the feature in an issue first
2. Follow the Squad Engineering workflow:
   ```bash
   /analyze
   /define-feature
   /evaluate
   ```

### 4. Making Changes

1. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes following the Squad Engineering principles
3. Commit with meaningful messages:
   ```bash
   git commit -m "feat: add new squad role for database migrations"
   ```

## Contribution Guidelines

### Types of Contributions

We welcome:
- **Bug fixes**: Identify and fix issues in the codebase
- **Feature implementations**: Add new capabilities following Squad Engineering patterns
- **Documentation improvements**: Enhance clarity and completeness
- **Test coverage**: Add missing tests or improve existing ones
- **Performance optimizations**: Make the framework more efficient
- **Squad patterns**: Contribute new role definitions or workflows

### What Makes a Good Contribution

- **Follows Squad Engineering principles**: Respects role boundaries and communication protocols
- **Well-tested**: Includes appropriate test coverage
- **Documented**: Updates relevant documentation
- **Focused**: One feature or fix per pull request
- **Clean**: No unnecessary files or changes

## Squad Engineering Principles

When contributing, always follow these core principles:

1. **Role Separation**
   - Supervisor roles orchestrate but don't implement
   - Implementation roles stay within their defined boundaries
   - Communication happens through designated channels

2. **Clear Communication**
   - Use role-comm files for inter-agent communication
   - Document decisions and blockers clearly
   - Keep status updates current

3. **Deterministic Outcomes**
   - Write code that produces predictable results
   - Avoid side effects outside defined boundaries
   - Test edge cases thoroughly

## Pull Request Process

1. **Before Submitting**
   - Ensure all tests pass
   - Update documentation as needed
   - Check that your code follows the style guide
   - Rebase on the latest main branch

2. **PR Description Template**
   ```markdown
   ## Description
   Brief description of changes

   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Documentation update
   - [ ] Performance improvement

   ## Testing
   - [ ] Unit tests pass
   - [ ] Integration tests pass
   - [ ] Manual testing completed

   ## Squad Engineering Compliance
   - [ ] Follows role boundaries
   - [ ] Updates necessary squad files
   - [ ] Communication protocols respected
   ```

3. **Review Process**
   - PRs require at least one review
   - Address all feedback constructively
   - Keep PRs focused and reasonably sized

## Code Standards

### TypeScript/JavaScript
- Use TypeScript for all new code
- Follow ESLint configuration
- Prefer functional programming patterns
- Use descriptive variable and function names

### File Organization
```
src/
├── agents/          # Agent implementations
├── commands/        # CLI commands
├── core/           # Core framework logic
├── templates/      # File templates
└── utils/          # Utility functions
```

### Naming Conventions
- Files: `kebab-case.ts`
- Classes: `PascalCase`
- Functions/Variables: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- Squad files: `role-[type]-[number].md`

## Testing

### Test Requirements
- All new features must include tests
- Maintain or improve code coverage
- Test both happy and error paths

### Running Tests
```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run specific test file
npm test -- path/to/test.spec.ts
```

### Writing Tests
- Use descriptive test names
- Follow AAA pattern (Arrange, Act, Assert)
- Mock external dependencies
- Test edge cases

## Documentation

### When to Update Documentation
- Adding new features
- Changing existing behavior
- Adding new squad roles or workflows
- Fixing documentation errors

### Documentation Standards
- Use clear, concise language
- Include code examples where helpful
- Keep README.md up to date
- Update squad files when changing workflows

### Squad-Specific Documentation
- Role definitions must include:
  - Clear boundaries
  - Technology stack
  - Communication protocols
  - Example implementations

## Community

### Getting Help
- Check existing documentation
- Search closed issues
- Ask in discussions
- Join our community chat

### Helping Others
- Answer questions in discussions
- Review pull requests
- Improve documentation
- Share your Squad Engineering patterns

## License

By contributing to Squad Engineering, you agree that your contributions will be licensed under the project's MIT License.

---

Thank you for contributing to Squad Engineering! Your efforts help make LLM-driven development more structured and scalable for everyone.