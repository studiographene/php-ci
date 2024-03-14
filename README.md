# php-ci

CI scans workflows for PHP based projects. Following is the sample code of the CI pipeline

```sh
name: studiographene-ci

on:
  pull_request: {}
  issue_comment:
  workflow_dispatch:

jobs:
  call-workflow:
    uses: studiographene/php-ci/.github/workflows/ci.yml@master
    with:
      package_manager: pnpm
      build_command: pnpm run build
      excluded_jobs: docker
    secrets: inherit
    permissions: write-all
```

## Inputs

### Required:

| Name | Description |
| ---- | ----------- |
|      |             |

### Optional:

| Name                     | Description                                                                 | Default                          |
| ------------------------ | --------------------------------------------------------------------------- | -------------------------------- |
| excluded_jobs            | A string of comma separated jobs that you want to exculude.                 |                                  |
| docker_build_command     | Docker build command                                                        | `docker build -t local:latest .` |
| docker_build_image_id    | Docker image ID as mentioned in docker_build_command                        | `local:latest`                   |
| CONTAINER_SCANNERS:      | comma-separated list of what security issues to detect (vuln,secret,config) | `vuln`                           |
| CONTAINER_SCAN_SKIP_DIRS | Comma separated list of directories to skip scanning                        |                                  |
| allowedLicenses          | A file containing allowed licenses name in License scan finding             |                                  |
| semgrep_options          |                                                                             |                                  |
security_scan_before_step_command    | Optional commands to pass before secuirty scan job |                               |
security_scan_after_step_command    | Optional commands to pass after secuirty scan job steps execution |                               |
caching_before_step_command    | Optional commands to pass before caching job steps execution |                   |
caching_after_step_command    | Optional commands to pass after caching job steps execution |                   |
technology_based_scans_before_step_command    | Optional commands to pass before techology based scans job steps execution |                   |
technology_based_scans_after_step_command    | Optional commands to pass after techology based scans job steps execution |                   |
pr_agent_before_step_command    | Optional commands to pass before Codium PR agent job steps execution |                   |
 pr_agent_after_step_command    | Optional commands to pass after Codium PR agent job steps execution |                   |
---

### Jobs list:
#### Jobs have nested steps which are running the mentioned scans.

- Security scans
  - SAST Scan
  - Gitleaks scan
  - License Scan
  - Dependency Scan using Google OSV
- Technology based scans
  - Docker Build
  - Trivy container vulnerability scan
- Codium PR Agent Scan


---


