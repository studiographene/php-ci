# php-ci

CI scans workflows for NodeJS based projects. Following is the sample code of the CI pipeline

```sh
name: studiographene-ci

on:
  pull_request: {}
  workflow_dispatch:

jobs:
  call-workflow:
    uses: studiographene/php-ci/.github/workflows/ci.yml@master
    with:
      project_name: microservice-boilerplate
      package_manager: pnpm
      build_command: pnpm run build
      lint_command: pnpm run lint
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
| lint_command             | lint command for the project                                                | `npm run lint`                   |
| allowedLicenses          | A file containing allowed licenses name in License scan finding             |                                  |
| semgrep_options          |                                                                             |                                  |

---

### Jobs list:

- sast
- dependency_scan
- licenseScan
- gitleaks
- docker
- pr_agent
