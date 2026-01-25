# Contributing Guide

Welcome to contribute to the RushChat project!

## Contributing Process Overview

```markmap
# Contributing Guide
## How to Contribute
- Report Bug
  - GitHub Issue
  - Describe Problem
  - Reproduction Steps
  - Environment Info
- Submit Feature Request
  - GitHub Issue
  - Feature Description
  - Use Cases
  - Implementation Plan
- Submit Code
  - Fork Project
  - Create Branch
  - Submit Changes
  - Pull Request
## Development Process
- Fork Project
  - GitHub Fork
  - Clone Repository
- Create Branch
  - feature/xxx
  - bugfix/xxx
- Development
  - Write Code
  - Add Tests
  - Update Documentation
- Submit
  - git commit
  - git push
  - Create PR
## Code Standards
- Rust Code
  - rustfmt
  - clippy
- JavaScript Code
  - ESLint
  - Prettier
- Commit Messages
  - Clear Description
  - Link Issue
```

## How to Contribute

### Report Bug

1. Submit Issue on GitHub
2. Describe the problem
3. Provide reproduction steps
4. Provide environment information

### Submit Feature Request

1. Submit Issue on GitHub
2. Describe feature requirements
3. Explain use cases
4. Discuss implementation plan

### Submit Code

1. Fork project
2. Create feature branch
3. Submit changes
4. Create Pull Request

## Development Process

### 1. Fork Project

```bash
# Fork to your GitHub account
# Then clone
git clone https://github.com/your-username/RustChat.git
cd RustChat
```

### 2. Create Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 3. Development

- Write code
- Add tests
- Update documentation

### 4. Submit Changes

```bash
git add .
git commit -m "Describe your changes"
git push origin feature/your-feature-name
```

### 5. Create Pull Request

1. Create Pull Request on GitHub
2. Describe changes
3. Wait for code review

## Code Standards

### Rust

- Use `cargo fmt` for formatting
- Use `cargo clippy` for checking
- Add necessary comments

### JavaScript

- Use ESLint
- Use Prettier
- Follow React Hooks rules

### Commit Messages

Use clear commit messages:

```
feat: Add new feature
fix: Fix bug
docs: Update documentation
style: Code formatting
refactor: Refactoring
test: Add tests
chore: Build/tools
```

## Testing

### Backend Testing

```bash
cd server-rust
cargo test
```

### Frontend Testing

```bash
cd client
npm test
```

## Related Documentation

- [Development Environment](setup.md)
- [Code Structure](structure.md)
