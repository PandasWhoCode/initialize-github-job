# initialize-github-job

Common steps for initializing a job for GitHub actions. This composite action provides a flexible way to set up your GitHub Actions workflow with repository checkout and various programming language runtimes.

## Features

- 🔄 Repository checkout with customizable options
- 🟢 Node.js setup with version management and caching
- 🐍 Python setup with version management and caching
- ☕ Java setup with multiple distributions
- 🔵 Go setup with module caching
- ⚡ Optimized with dependency caching support

## Usage

### Basic Example - Checkout Only

```yaml
- name: Initialize job
  uses: PandasWhoCode/initialize-github-job@v1
```

### Node.js Project

```yaml
- name: Initialize Node.js job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-node: 'true'
    node-version: '20'
    node-cache: 'npm'
```

### Python Project

```yaml
- name: Initialize Python job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-python: 'true'
    python-version: '3.11'
    python-cache: 'pip'
```

### Java Project

```yaml
- name: Initialize Java job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-java: 'true'
    java-version: '17'
    java-distribution: 'temurin'
```

### Go Project

```yaml
- name: Initialize Go job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-go: 'true'
    go-version: '1.21'
```

### Multi-Language Project

```yaml
- name: Initialize multi-language job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-node: 'true'
    node-version: '20'
    node-cache: 'npm'
    setup-python: 'true'
    python-version: '3.11'
    python-cache: 'pip'
```

### Skip Checkout

```yaml
- name: Initialize without checkout
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout: 'false'
    setup-node: 'true'
    node-version: '20'
```

### Custom Checkout Options

```yaml
- name: Initialize with custom checkout
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout-ref: 'develop'
    checkout-token: ${{ secrets.CUSTOM_GITHUB_TOKEN }}
    setup-node: 'true'
```

## Inputs

### Checkout Options

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `checkout` | Whether to checkout the repository | No | `true` |
| `checkout-ref` | The branch, tag or SHA to checkout | No | `''` |
| `checkout-token` | Personal access token (PAT) used to fetch the repository | No | `${{ github.token }}` |

### Node.js Options

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `setup-node` | Whether to setup Node.js | No | `false` |
| `node-version` | Node.js version to use | No | `20` |
| `node-version-file` | File containing the Node.js version (e.g., `.nvmrc`, `.node-version`) | No | `''` |
| `node-cache` | Package manager for caching (`npm`, `yarn`, `pnpm`) | No | `''` |

### Python Options

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `setup-python` | Whether to setup Python | No | `false` |
| `python-version` | Python version to use | No | `3.x` |
| `python-cache` | Package manager for caching (`pip`, `pipenv`, `poetry`) | No | `''` |

### Java Options

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `setup-java` | Whether to setup Java | No | `false` |
| `java-version` | Java version to use | No | `17` |
| `java-distribution` | Java distribution (`temurin`, `zulu`, `adopt`, etc.) | No | `temurin` |

### Go Options

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `setup-go` | Whether to setup Go | No | `false` |
| `go-version` | Go version to use | No | `stable` |
| `go-cache` | Whether to cache Go modules | No | `true` |

## Complete Workflow Example

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Initialize job
        uses: PandasWhoCode/initialize-github-job@v1
        with:
          setup-node: 'true'
          node-version: '20'
          node-cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run tests
        run: npm test
      
      - name: Build
        run: npm run build
```

## License

This project is licensed under the terms specified in the LICENSE file.
