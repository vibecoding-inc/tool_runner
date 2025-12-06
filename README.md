# tool_runner

A collection of GitHub Actions workflows for running linters and tests on Java, Go, and Python projects.

## Available Workflows

### Java Workflows

#### java-lint.yml
Runs popular Java linters on Maven and Gradle projects:
- **Checkstyle**: Code style checker
- **SpotBugs**: Static analysis for bug detection
- **PMD**: Source code analyzer

#### java-test.yml
Runs Java tests using Maven or Gradle:
- Executes test suites
- Generates test summary reports
- Supports both Maven and Gradle projects

### Go Workflows

#### go-lint.yml
Runs comprehensive Go linters:
- **golangci-lint**: Meta-linter running multiple linters
- **go vet**: Official Go static analysis tool
- **go fmt**: Code formatting checker
- **staticcheck**: Advanced static analysis

#### go-test.yml
Runs Go tests with detailed reporting:
- Executes tests with race detection
- Generates coverage reports
- Runs benchmarks
- Supports Go modules

### Python Workflows

#### python-lint.yml
Runs comprehensive Python linters:
- **flake8**: Style guide enforcement and error detection
- **pylint**: Static code analysis
- **black**: Code formatting checker
- **mypy**: Static type checking

#### python-test.yml
Runs Python tests with pytest:
- Executes test suites with verbose output
- Generates coverage reports
- Supports requirements.txt, setup.py, and pyproject.toml
- Installs dev/test dependencies automatically

## Workflow Interface

All workflows follow the same interface pattern:

### Inputs
- `target_repository` (required): Repository to run against (format: `owner/repo`)
- `resumeUrl` (required): Webhook URL to receive results

### Authentication
Uses GitHub App authentication with the following secrets:
- `APP_ID`: GitHub App ID
- `APP_PRIVATE_KEY`: GitHub App private key

### Output
Results are:
1. Collected in a `report.txt` file
2. Uploaded as a workflow artifact
3. Sent to the webhook URL as JSON: `{"summary": "report content"}`

## Usage

Trigger workflows manually via workflow_dispatch, providing:
1. The target repository to analyze
2. The webhook URL to receive results

Example:
```yaml
target_repository: "my-org/my-repo"
resumeUrl: "https://example.org/webhook"
```

## Security

All workflows implement least-privilege permissions:
- Workflow level: `permissions: {}`
- Tool jobs: `contents: read`
- Webhook jobs: `permissions: {}`

