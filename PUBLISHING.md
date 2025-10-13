# Publishing Guide

This guide walks you through the steps to publish this GitHub Action to the GitHub Marketplace.

## Prerequisites

- [x] Repository is connected to GitHub (✅ `https://github.com/optivem/summarize-commit-stage-action.git`)
- [x] MIT License is present (✅)
- [x] Comprehensive README with usage examples (✅)
- [x] action.yml with proper metadata and branding (✅)
- [x] Release workflow is configured (✅)

## Steps to Publish

### 1. Make Repository Public

1. Go to your repository on GitHub: https://github.com/optivem/summarize-commit-stage-action
2. Click on **Settings** tab
3. Scroll down to the **Danger Zone** section
4. Click **Change repository visibility**
5. Select **Make public**
6. Type the repository name to confirm
7. Click **I understand, change repository visibility**

### 2. Commit and Push Changes

Run the following commands to commit all the improvements:

```bash
git add .
git commit -m "feat: prepare action for marketplace publication

- Enhanced README with comprehensive documentation and examples
- Added branding (icon and color) to action.yml
- Created GitHub workflows for CI, releases, and examples
- Added publishing guide and contribution guidelines"
git push origin main
```

### 3. Create Initial Release

1. Go to your repository on GitHub
2. Click **Releases** (on the right sidebar)
3. Click **Create a new release**
4. Choose a tag: `v1.0.0` (or click "Create new tag")
5. Release title: `v1.0.0 - Initial Release`
6. Description:
   ```markdown
   ## 🎉 Initial Release
   
   This is the first public release of the Summarize Commit Stage Action.
   
   ### Features
   - ✅ Generate comprehensive summaries of commit stage results
   - 🐳 Display Docker image information including URLs and digests
   - 📊 Show build status with customizable messages
   - 🎨 Consistent formatting using optivem/summarize-stage-action
   
   ### Usage
   
   ```yaml
   - name: Summarize Commit Stage
     uses: optivem/summarize-commit-stage-action@v1
     with:
       stage-result: ${{ job.status }}
       component-name: 'My Component'
       image-url: ${{ steps.build.outputs.image-url }}
       image-digest-url: ${{ steps.build.outputs.image-digest-url }}
       image-created: ${{ steps.build.outputs.image-created }}
   ```
   
   For detailed documentation, see the [README](https://github.com/optivem/summarize-commit-stage-action#readme).
   ```
7. Click **Publish release**

### 4. Publish to GitHub Marketplace

1. After creating the release, GitHub will automatically detect it's an Action
2. Go to your repository main page
3. You should see a banner "Publish this Action to the GitHub Marketplace"
4. Click **Draft a release** or **Publish this Action to the GitHub Marketplace**
5. Fill in the marketplace details:
   - **Primary Category**: Continuous Integration
   - **Secondary Category**: (optional) Utilities
   - **Logo**: The action will use the "file-text" icon specified in action.yml
   - **Color**: Blue (as specified in action.yml)
6. Review the Terms of Service
7. Click **Publish release**

### 5. Verify Publication

1. Your action should now be available at: `https://github.com/marketplace/actions/summarize-commit-stage`
2. Test the action by using it in another repository:
   ```yaml
   uses: optivem/summarize-commit-stage-action@v1
   ```

## Marketplace Requirements Checklist

- [x] **Repository is public** (you need to do this step)
- [x] **Valid action.yml** with name, description, inputs, and runs
- [x] **README.md** with clear usage instructions
- [x] **License file** (MIT License ✅)
- [x] **Proper versioning** (semantic versioning with tags)
- [x] **Branding** (icon and color in action.yml)
- [x] **No sensitive information** in the repository

## Best Practices

1. **Use semantic versioning**: v1.0.0, v1.1.0, v2.0.0, etc.
2. **Maintain major version tags**: When you release v1.1.0, also update the v1 tag
3. **Keep breaking changes in major versions**: v1.x.x should be backward compatible
4. **Document all inputs and outputs**: Clear descriptions in action.yml and README
5. **Provide examples**: Show real-world usage scenarios
6. **Test thoroughly**: Use the CI workflow to validate changes

## Maintenance

- Monitor issues and pull requests
- Keep dependencies updated (especially `optivem/summarize-stage-action`)
- Release new versions when features are added or bugs are fixed
- Update documentation as the action evolves

## Support

If you encounter any issues during publication:
1. Check the [GitHub Actions documentation](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace)
2. Review the [Marketplace guidelines](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace#requirements-to-publish-an-action)
3. Open an issue in this repository if you need help