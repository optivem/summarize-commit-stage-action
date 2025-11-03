# Summarize Commit Stage Action

[![CI](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/ci.yml/badge.svg)](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/ci.yml)
[![Example CI Pipeline](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/example.yml/badge.svg)](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/example.yml)
[![Release](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/release.yml/badge.svg)](https://github.com/optivem/summarize-commit-stage-action/actions/workflows/release.yml)

[![GitHub release](https://img.shields.io/github/release/optivem/summarize-commit-stage-action.svg)](https://github.com/optivem/summarize-commit-stage-action/releases)

A GitHub Action that generates comprehensive summaries of commit stage results, including build status and Docker image information. This action is particularly useful for CI/CD pipelines where you want to provide clear, formatted summaries of your commit stage outcomes.

## Features

- ✅ Generates formatted summaries of commit stage results
- 🐳 Displays Docker image information including URLs and digests
- 📊 Shows build status with customizable messages
- 🎨 Uses the underlying `optivem/summarize-stage-action` for consistent formatting
- ⚡ Simple composite action - no complex setup required

## Usage

### Basic Example

```yaml
name: CI Pipeline
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  commit-stage:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Build and Push Docker Image
        # Your build steps here...
        id: docker-build
        
      - name: Summarize Commit Stage
        uses: optivem/summarize-commit-stage-action@v1
        with:
          stage-result: ${{ job.status }}
          component-name: 'My Application'
          artifact-url: ${{ steps.docker-build.outputs.image-url }}
          artifact-created-timestamp: ${{ steps.docker-build.outputs.image-created }}
```

### Docker Image Example

```yaml
      - name: Summarize API Commit Stage
        uses: optivem/summarize-commit-stage-action@v1
        with:
          stage-result: ${{ job.status }}
          stage-name: 'API Build & Deploy'
          component-name: 'Backend API'
          artifact-url: 'my-registry.com/my-app:latest'
          artifact-created-timestamp: '2025-10-13T10:30:00Z'
          artifact-type: 'Docker Image'
```

### Installer/MSI Example

```yaml
      - name: Summarize Windows Build
        uses: optivem/summarize-commit-stage-action@v1
        with:
          stage-result: ${{ job.status }}
          component-name: 'Desktop Application'
          artifact-url: 'https://releases.example.com/v1.0.0/MyApp-Setup.msi'
          artifact-created-timestamp: '2025-10-13T10:30:00Z'
          artifact-type: 'MSI Installer'
```

### NPM Package Example

```yaml
      - name: Summarize NPM Publish
        uses: optivem/summarize-commit-stage-action@v1
        with:
          stage-result: ${{ job.status }}
          component-name: 'UI Components'
          artifact-url: 'https://www.npmjs.com/package/my-components'
          artifact-created-timestamp: '2025-10-13T10:30:00Z'
          artifact-type: 'NPM Package'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `stage-result` | Result of the stage job (success, failure, cancelled, etc.) | ✅ Yes | |
| `stage-name` | Name of the stage being summarized | ❌ No | `Commit Stage` |
| `component-name` | Name of the component being processed (e.g., Monolith, API, Frontend) | ✅ Yes | |
| `artifact-url` | URL of the published artifact (Docker image, installer, package, etc.) | ✅ Yes | |
| `artifact-created-timestamp` | Timestamp when the artifact was created (ISO 8601 format) | ✅ Yes | |
| `artifact-type` | Type of artifact for display purposes | ❌ No | `Artifact` |

## Output

This action generates a formatted summary that includes:

- **Stage Status**: Clear indication of success/failure
- **Component Information**: The component name being processed
- **Artifact Details**:
  - Artifact type for context
  - Artifact URL for easy access
  - Creation timestamp

## Example Output

When successful, the action generates a summary like:

```
✅ API Build & Deploy - Backend API

Successfully Published Docker Image:

**Artifact Type:**
`Docker Image`

**Artifact URL:**
`my-registry.com/my-app:latest`

**Created:**
`2025-10-13T10:30:00Z`
```

## Dependencies

This action is built on top of [`optivem/summarize-stage-action@v1`](https://github.com/optivem/summarize-stage-action), which provides the core summarization functionality.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

If you encounter any issues or have questions, please [open an issue](https://github.com/optivem/summarize-commit-stage-action/issues) on GitHub.
