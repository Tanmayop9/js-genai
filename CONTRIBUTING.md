# Contributing

Thank you for your interest in contributing to the Google Gen AI SDK fork!

## Development Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Tanmayop9/js-genai.git
   cd js-genai
   ```

2. Install dependencies:
   ```bash
   npm ci
   ```

3. Build the project:
   ```bash
   npm run build
   ```

4. Run tests:
   ```bash
   npm run unit-test
   ```

## Code Quality

Before submitting changes, ensure:

- Code passes linting: `npm run lint`
- All tests pass: `npm run unit-test`
- Code is formatted: `npm run format`

## Commit Convention

This project uses [Conventional Commits](https://www.conventionalcommits.org/) for automated versioning and changelog generation.

Format: `<type>(<scope>): <description>`

Types:
- `feat:` - New feature (minor version bump)
- `fix:` - Bug fix (patch version bump)
- `docs:` - Documentation changes
- `chore:` - Maintenance tasks
- `test:` - Test additions or modifications
- `refactor:` - Code refactoring
- `BREAKING CHANGE:` - Breaking changes (major version bump)

Examples:
```
feat: add support for new Gemini model
fix: correct error handling in streaming responses
docs: update installation instructions
```

## Publishing

See [NPM_PUBLISHING.md](./NPM_PUBLISHING.md) for details on the automated publishing process.

## Questions?

Feel free to open an issue for any questions or concerns.
