# NPM Publishing Setup Guide

This guide explains how to set up and use the automated npm publishing workflow for this package.

## Prerequisites

1. An npm account with publishing rights to the package
2. An npm access token with publish permissions
3. GitHub repository access with admin permissions

## Setup Instructions

### 1. Create an NPM Access Token

1. Log in to your npm account at https://www.npmjs.com
2. Go to your account settings
3. Click on "Access Tokens"
4. Click "Generate New Token"
5. Select "Automation" token type (recommended for CI/CD)
6. Copy the generated token (you won't be able to see it again!)

### 2. Add NPM Token to GitHub Secrets

1. Go to your GitHub repository
2. Click on "Settings" → "Secrets and variables" → "Actions"
3. Click "New repository secret"
4. Name: `NPM_TOKEN`
5. Value: Paste your npm access token
6. Click "Add secret"

### 3. Update Package Name (If Publishing Under Different Scope)

If you want to publish under a different scope (e.g., `@yourusername/genai` instead of `@google/genai`):

1. Edit `package.json`
2. Change the `name` field to your desired package name
3. If using a scoped package, ensure it's set to public access or configure your npm account

## Publishing Workflow

### Automated Publishing on Release

The package is automatically published to npm when you create a GitHub release:

1. The Release Please workflow automatically creates a release PR when you merge changes to main
2. When the Release Please PR is merged, it creates a GitHub release
3. The npm-publish workflow is triggered by the release
4. The workflow runs tests, builds the package, and publishes to npm

### Manual Release Process

If you prefer to create releases manually:

1. Make your changes and commit them
2. Update the version in `package.json` following semantic versioning
3. Update the `CHANGELOG.md` file
4. Create a git tag: `git tag v1.2.3`
5. Push the tag: `git push origin v1.2.3`
6. Create a GitHub release from the tag
7. The npm-publish workflow will run automatically

## Workflow Features

### Release Please Workflow

- **Trigger**: Runs on push to main branch
- **Purpose**: Automatically creates release PRs with version bumps and changelog updates
- **Configuration**: Uses `release-please-config.json` and `.release-please-manifest.json`
- **Conventional Commits**: Analyzes commit messages to determine version bumps
  - `feat:` → minor version bump
  - `fix:` → patch version bump
  - `BREAKING CHANGE:` → major version bump

### NPM Publish Workflow

- **Trigger**: Runs when a GitHub release is published
- **Steps**:
  1. Checkout code
  2. Setup Node.js (v22)
  3. Install dependencies
  4. Run linting
  5. Build production bundle
  6. Run unit tests
  7. Publish to npm with provenance
- **Features**:
  - Provenance signatures for supply chain security
  - Public access for scoped packages
  - Automated testing before publish

## Testing the Workflow

To test the workflow without publishing:

1. Make changes to the workflow file
2. Change the trigger to `workflow_dispatch` temporarily
3. Test the workflow manually from the Actions tab
4. Review the workflow logs
5. Once verified, change the trigger back to `release`

## Troubleshooting

### Authentication Errors

- Verify the NPM_TOKEN secret is set correctly
- Ensure the token has publish permissions
- Check if the token has expired

### Build Failures

- Run `npm run build-prod` locally to test the build
- Check the workflow logs for specific error messages
- Ensure all dependencies are correctly specified

### Test Failures

- Run `npm run unit-test` locally
- Fix any failing tests before attempting to publish

### Version Conflicts

- Ensure the version in `package.json` is higher than the published version
- Check npm registry for the current published version

## Best Practices

1. **Use Conventional Commits**: Follow the conventional commits format for automatic versioning
2. **Test Locally**: Always test builds and tests locally before pushing
3. **Review Release PRs**: Carefully review Release Please PRs before merging
4. **Keep Dependencies Updated**: Regularly update dependencies to avoid vulnerabilities
5. **Monitor Workflow Runs**: Check the Actions tab to ensure workflows complete successfully

## Security Considerations

1. **Provenance**: The workflow uses npm provenance for supply chain security
2. **Token Security**: Never commit npm tokens to the repository
3. **Dependency Audits**: Run `npm audit` regularly to check for vulnerabilities
4. **Pre-publish Checks**: The workflow runs linting and tests before publishing

## Additional Resources

- [npm Publishing Documentation](https://docs.npmjs.com/cli/v8/commands/npm-publish)
- [Release Please Documentation](https://github.com/googleapis/release-please)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Conventional Commits](https://www.conventionalcommits.org/)
