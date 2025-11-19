# Initialize GitHub Job

Common steps for initializing a job for GitHub actions. This composite action consolidates setup steps for multiple programming languages and tools.

## Features

- Security hardening with Step Security's Harden Runner
- Repository checkout with configurable options
- Multi-language support (Node.js, Java, Python, Go, Rust, Swift)
- Build tool setup (Gradle)
- Automatic caching for dependencies and build artifacts

## Usage

```yaml
- name: Initialize Job
  uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout: 'true'
    checkout-token: '${{ secrets.GITHUB_TOKEN }}'
    setup-node: 'true'
    node-version: '20'
    node-cache: 'npm'
```

### Inputs

**Repository Checkout**

| Input                | Description                                              | Required | Default |
|----------------------|----------------------------------------------------------|----------|---------|
| checkout             | Whether to checkout the repository                       | No       | -       |
| checkout-ref         | The branch, tag or SHA to checkout                       | No       | -       |
| checkout-token       | Personal access token (PAT) used to fetch the repository | No       | -       |
| checkout-fetch-depth | Depth of commit history to fetch                         | No       | 0       |

**Java**

| Input             | Description                                               | Required | Default |
|-------------------|-----------------------------------------------------------|----------|---------|
| setup-java        | Whether to setup Java                                     | No       | -       |
| java-version      | Java version to use                                       | No       | -       |
| java-distribution | Java distribution (temurin, zulu, adopt, etc.)            | No       | -       |
| java-cache        | Build platform to cache dependencies (maven, gradle, sbt) | No       | -       |

**Gradle**

| Input                  | Description                                                                                | Required | Default |
|------------------------|--------------------------------------------------------------------------------------------|----------|---------|
| setup-gradle           | Whether to setup Gradle                                                                    | No       | -       |
| gradle-version         | Gradle version to use                                                                      | No       | wrapper |
| gradle-cache-disabled  | Whether to disable Gradle caching                                                          | No       | false   |
| gradle-cache-read-only | Whether to use read-only caching for Gradle                                                | No       | -       |
| cache-write-only       | When true, entries will not be restored from cache but will be saved at the end of the Job | No       | false   |

**Node.js**

| Input             | Description                                     | Required | Default |
|-------------------|-------------------------------------------------|----------|---------|
| setup-node        | Whether to setup Node.js                        | No       | -       |
| node-version      | Node.js version to use                          | No       | -       |
| node-cache        | Package manager for caching (npm, yarn, pnpm)   | No       | -       |
| node-check-latest | Whether to check for the latest Node.js version | No       | -       |

**Python**

| Input          | Description                                       | Required | Default |
|----------------|---------------------------------------------------|----------|---------|
| setup-python   | Whether to setup Python                           | No       | -       |
| python-version | Python version to use                             | No       | -       |
| python-cache   | Package manager for caching (pip, pipenv, poetry) | No       | -       |

**Go**

| Input           | Description                    | Required | Default |
|-----------------|--------------------------------|----------|---------|
| setup-go        | Whether to setup Go            | No       | -       |
| go-version      | Go version to use              | No       | -       |
| go-cache        | Whether to cache Go modules    | No       | true    |
| go-architecture | Target architecture (x86, x64) | No       | -       |


**Rust**

| Input           | Description                                       | Required | Default |
|-----------------|---------------------------------------------------|----------|---------|
| setup-rust      | Whether to setup Rust                             | No       | -       |
| rust-version    | Rust version to use                               | No       | -       |
| rust-targets    | Comma-separated list of target triples to install | No       | -       |
| rust-components | Comma-separated list of components to install     | No       | -       |

**Swift**

| Input                      | Description                                              | Required | Default |
|----------------------------|----------------------------------------------------------|----------|---------|
| setup-swift                | Whether to setup Swift                                   | No       | -       |
| swift-version              | Swift version to use                                     | No       | -       |
| swift-cache                | Whether to cache downloaded toolchain snapshots          | No       | true    |
| swift-prefer-oss-toolchain | Whether to prefer Swift open source toolchain over Xcode | No       | false   |
| swift-sdks                 | Semi-colon separated list of Swift SDKs to install       | No       | -       |

### Outputs

**Checkout Outputs**

- `checkout-ref`: The branch, tag or SHA that was checked out
- `checkout-commit`: The commit SHA that was checked out

**Java Outputs**

- `java-distribution`: Distribution of Java that has been installed
- `java-version`: Actual version of the java environment that has been installed
- `java-path`: Path to where the java environment has been installed
- `java-cache-hit`: Boolean indicating if cache was hit

**Gradle Outputs**

- `gradle-build-scan-url`: Link to the Build Scan® generated by a Gradle build
- `gradle-dependency-graph-file`: Path to the GitHub Dependency Graph snapshot file
- `gradle-version`: Version of Gradle that was setup

**Node.js Outputs**
- `node-cache-hit`: Boolean indicating if cache was hit
- `node-version`: The installed node version

**Python Outputs**

- `python-version`: The installed Python or PyPy version
- `python-cache-hit`: Boolean indicating if cache was hit
- `python-path`: The absolute path to the Python or PyPy executable

**Go Outputs**

- `go-version`: The installed Go version
- `go-cache-hit`: Boolean indicating if cache was hit

**Rust Outputs**

- `rust-cachekey`: A short hash of the rustc version for use as a cache key
- `rust-name`: Rustups name for the selected version of the toolchain

**Swift Outputs**

- `swift-version`: The actual Swift version that was configured
- `swift-toolchain`: JSON formatted toolchain snapshot metadata
- `swift-sdks`: JSON formatted SDK snapshots metadata

## Examples

**Node.js Project**

```yaml
- uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout: 'true'
    checkout-token: '${{ secrets.GITHUB_TOKEN }}'
    setup-node: 'true'
    node-version: '20'
    node-cache: 'npm'
```

**Java with Gradle**

```yaml
- uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout: 'true'
    setup-java: 'true'
    java-version: '21'
    java-distribution: 'temurin'
    setup-gradle: 'true'
```

**Python Project**

```yaml
- uses: PandasWhoCode/initialize-github-job@v1
  with:
    setup-python: 'true'
    python-version: '3.12'
    python-cache: 'pip'
```

**Multi-Language Setup**

```yaml
- uses: PandasWhoCode/initialize-github-job@v1
  with:
    checkout: 'true'
    setup-node: 'true'
    node-version: '20'
    node-cache: 'npm'
    setup-python: 'true'
    python-version: '3.12'
    python-cache: 'pip'
```

## License
This repository is licensed under the Apache 2.0 License. See the [LICENSE](LICENSE) file for details.
