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
   