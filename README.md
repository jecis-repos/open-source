# Open Source Work

Original open-source packages and engineering articles by [Jekabs Porietis](https://github.com/jecis-repos).

## Packages and tooling

| Project | Purpose | Checks verified on 2026-09-29 |
|---|---|---|
| [laravel-rag](https://github.com/jecis-repos/laravel-rag) | PHP AST extraction, knowledge graphs and hybrid retrieval for Laravel | 81 tests / 243 assertions; PHP 8.2–8.5 CI |
| [ab-stats](https://github.com/jecis-repos/ab-stats) | Dependency-free PHP statistical tests and sample-size calculations | 73 tests / 381 assertions; PHP 8.1–8.5 CI |
| [dev-machine](https://github.com/jecis-repos/dev-machine) | Docker Compose management through a terminal dashboard and MCP server | 67 tests; build, MCP handshake and local TUI startup |
| [staging-preview](https://github.com/jecis-repos/staging-preview) | PR preview lifecycle automation for a prepared application workspace | 11 tests; backend build and runtime import |

The four suites contain **232 tests** at this dated check. Runtime checks cover the paths listed above; provisioning also requires the services and configuration documented in each repository.

## Installation

Follow each project's README for its current requirements. The PHP packages can be installed directly from their public Git repositories with Composer:

```sh
composer config repositories.ab-stats vcs https://github.com/jecis-repos/ab-stats.git
composer require jekabs/ab-stats:dev-main
```

For the terminal dashboard:

```sh
git clone https://github.com/jecis-repos/dev-machine.git
cd dev-machine
npm ci
npm run build
npm run tui
# MCP stdio server: npm start
```

Staging preview includes a pinned backend submodule, so clone it with `--recurse-submodules` and follow its [workspace setup instructions](https://github.com/jecis-repos/staging-preview#quick-start).

## Technical articles

The [dev-articles index](https://github.com/jecis-repos/dev-articles) links the OAuth/MCP article, the three-part staging-system series, and the agent-pipeline article.

**Jekabs Porietis** — [GitHub](https://github.com/jecis-repos) | [Threads](https://threads.net/@ananiel_)
