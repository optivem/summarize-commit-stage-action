# Summarize Commit Stage Action

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
          image-url: ${{ steps.docker-build.outputs.image-url }}
          image-digest-url: ${{ steps.docker-build.outputs.image-digest-url }}
          image-created: ${{ steps.docker-build.outputs.image-created }}
```

### Advanced Example with Custom Stage Name

```yaml
      - name: Summarize API Commit Stage
        uses: optivem/summarize-commit-stage-action@v1
        with:
          stage-result: ${{ job.status }}
          stage-name: 'API Build & Deploy'
          component-name: 'Backend API'
          image-url: 'my-registry.com/my-app:latest'
          image-digest-url: 'my-registry.com/my-app@sha256:abc123...'
          image-created: '2025-10-13T10:30:00Z'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `stage-result` | Result of the stage job (success, failure, cancelled, etc.) | ✅ Yes | |
| `stage-name` | Name of the stage being summarized | ❌ No | `Commit Stage` |
| `component-name` | Name of the component being processed (e.g., Monolith, API, Frontend) | ✅ Yes | |
| `image-url` | Full URL of the pushed Docker image | ✅ Yes | |
| `image-digest-url` | Full URL with SHA256 digest of the pushed image | ✅ Yes | |
| `image-created` | Timestamp when the Docker image was created (ISO 8601 format) | ✅ Yes | |

## Output

This action generates a formatted summary that includes:

- **Stage Status**: Clear indication of success/failure
- **Component Information**: The component name being processed
- **Docker Image Details**:
  - Image URL for easy access
  - Creation timestamp
  - SHA256 digest URL for verification
  - Helpful note about potential digest URL truncation

## Example Output

When successful, the action generates a summary like:

```
✅ API Build & Deploy - Backend API

Successfully Published Docker Image:

**Image URL:**
`my-registry.com/my-app:latest`

**Image Created:**
`2025-10-13T10:30:00Z`

**Image Digest URL:**
`my-registry.com/my-app@sha256:abc123...`

⚠️ *If digest URL appears truncated, check 'Publish Docker Image' step logs for full details*
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
