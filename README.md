# Plug-and-Play APK Builder

This repository provides a GitHub Actions workflow to automatically build an Android APK from any GitHub or GitLab Android project, even if it lacks a `build.gradle` file. Just provide the repository URL and optional parameters, and the workflow will detect the build system (Gradle, Ant, Maven) or scaffold a Gradle structure if needed.

## Features
- Supports Gradle, Ant, and Maven build systems.
- Automatically scaffolds a Gradle structure for projects without a build system but with Android files (`AndroidManifest.xml`, `src/`, `res/`).
- Handles nested project directories (e.g., `app/` or `android/`).
- Supports private repositories with a GitHub Personal Access Token.
- Caches Gradle dependencies for faster builds.
- Detailed error messages for easy debugging.

## How to Use

1. **Fork or Use This Repository as a Template**:
   - Click "Use this template" on GitHub to create your own repository, or fork this repository.

2. **Set Up a GitHub Personal Access Token (for Private Repositories)**:
   - If the target repository is private, create a [Personal Access Token](https://github.com/settings/tokens) with `repo` scope.
   - Add the token as a repository secret named `GH_TOKEN`:
     - Go to your repository → Settings → Secrets and variables → Actions → New repository secret.
     - Name: `GH_TOKEN`, Value: `<your_token>`.

3. **Trigger the Workflow**:
   - Go to the "Actions" tab in your repository.
   - Select the "Plug-and-Play APK Builder" workflow.
   - Click "Run workflow" and provide the following inputs:
     - `repo_url`: The GitHub or GitLab repository URL (e.g., `https://github.com/username/repo.git`).
     - `branch`: (Optional) The branch or tag to build (e.g., `main`).
     - `module_name`: (Optional) The Gradle module name (e.g., `app`, defaults to `app`).
     - `project_path`: (Optional) The path to the Android project directory (e.g., `android/`).
     - `build_system`: (Optional) The build system (`gradle`, `ant`, `maven`, `auto`; defaults to `auto`).
   - Example:
     ```bash
     repo_url: https://github.com/username/repo.git
     branch: main
     module_name: app
     project_path: 
     build_system: auto
     ```

4. **Download the APK**:
   - After the workflow completes, go to the "Actions" tab and find the workflow run.
   - Download the `debug-apk` artifact containing the built APK.

## Example Commands

- Build a public Gradle-based project:
  ```bash
  gh workflow run apk-builder.yml \
    -f repo_url=https://github.com/android/sunflower.git \
    -f branch=main \
    -f module_name=app \
    -f build_system=gradle
