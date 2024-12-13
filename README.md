# Workflows

Github Actions used in projects of the WordPress team.

- PHPStan
- Dependabot (auto-merge)
- Markdown Lint
  - Requires `.markdownlint.yml` in project root!
- PHP CS Fixer
- Composer lock differance
- NPM lock differance

## Usage

1. Create an `.github/workflows/` dir in your project root
2. Make a file workflow file with `.yml` suffix, in this example we wil use `phpstan.yml`
3. Add the syntax below:
    ```yaml
    name: PHPStan
    
    on:
        pull_request:
            paths:
                - '**.php'
                - 'phpstan.neon.dist'
                - '.github/workflows/phpstan.yml'
    
    jobs:
      phpstan:
        uses: yardinternet/workflows/.github/workflows/phpstan.yml@main
        secrets: inherit
    ```
   We reference the work flow in `uses` with the following schema: `{owner}/{repo}/.github/workflows/{filename}@{ref}`.
   Also make sure to pass on the secrets: `secrets: inherit`.
   
### run-laravel-testbench-tests.yml

When calling the `run-laravel-testbench-tests.yml` workflow one can use `with` to pass version settings.

```yaml

jobs:
  test:
    uses: yardinternet/workflows/.github/workflows/run-laravel-testbench-tests.yml@main
    with:
      php-versions: '["8.1"]'
      laravel-versions: '["10.*"]'
      testbench-versions: '["8.*"]'
    secrets: inherit
```

### run-pest-tests.yml

This alternative test runner can be used in packages that are not Laravel-based. When calling the `run-pest-tests.yml` workflow one can use `with` to pass version settings.

```yaml

jobs:
  test:
    uses: yardinternet/workflows/.github/workflows/run-pest-tests.yml@main
    with:
      php-versions: '["8.1"]'
    secrets: inherit
```