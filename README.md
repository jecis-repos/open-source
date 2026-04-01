# Open Source Work

7+ years of building high-scale, high-load production systems taught me what actually works — and what doesn't. These packages are the patterns that survived: the search algorithms, the statistical methods, the infrastructure automation, the deployment strategies that hold up under real traffic and real deadlines.

**228+ tests. 19,000+ lines.**

---

## Packages

### [laravel-rag](https://github.com/jecis-repos/laravel-rag) — Laravel RAG that understands code structure

A RAG package that doesn't just chunk text — it parses PHP with 12 AST extractors, builds a typed knowledge graph, and searches it with a 4-stage pipeline.

| | |
|---|---|
| **AST Extractors** | Classes, methods, Eloquent relationships, morph maps, routes, service bindings, event/listeners, migrations, configs, Filament resources, middleware, validation rules |
| **Search Pipeline** | pgvector cosine similarity &#8594; BM25 keyword scoring &#8594; Reciprocal Rank Fusion &#8594; multi-hop graph traversal with score decay |
| **Indexing** | Incremental (SHA-256 hash skip), CLI commands (`rag:index`, `rag:search`, `rag:index-repo`), external git repo cloning |
| **Tests** | 81 tests, 243 assertions |
| **Stack** | PHP 8.2+, Laravel 10-13, PostgreSQL + pgvector, nikic/php-parser |

```php
// Index any git repo
php artisan rag:index-repo laravel/framework --extensions=php,md

// Search with graph traversal
$results = app(KnowledgeSearch::class)->search('How does lead assignment work?');
// LeadController (hop=0) → AssignLeadAction (hop=1) → ActivityRepository (hop=2)
```

---

### [ab-stats](https://github.com/jecis-repos/ab-stats) — A/B testing statistics, zero dependencies

Pure PHP statistical testing. No frameworks, no extensions, no external calls. Chi-squared, Bayesian analysis, power calculations — all in ~1,400 lines.

| | |
|---|---|
| **Frequentist** | Chi-squared with Yates' correction, Abramowitz & Stegun CDF (max error 7.5e-8, NIST-verified) |
| **Bayesian** | Beta-Binomial Monte Carlo, credible intervals, P(B beats A), expected lift with CI |
| **Power** | Required sample size calculator, achievable power for given N, inverse CDF via Acklam's approximation |
| **Multi-variant** | Bonferroni correction for k comparisons, auto-sorted by significance |
| **Tests** | 73 tests, 381 assertions |
| **Stack** | PHP 8.1+, zero dependencies |

```php
$result = ABTest::evaluate(
    Variant::make('Original', successes: 320, total: 10_000),
    Variant::make('Redesign', successes: 380, total: 10_000),
);
// isSignificant: true, winner: 'Redesign', lift: +18.75%, p: 0.0005

$bayesian = BayesianTest::evaluate($control, $treatment);
// probabilityTreatmentWins: 0.997, credibleInterval: [0.034, 0.042]

$n = PowerCalculator::requiredSampleSize(baselineRate: 0.03, mde: 0.005);
// 4,810 per variant for 80% power
```

---

## Infrastructure Tools

### [dev-machine](https://github.com/jecis-repos/dev-machine) — One-command local dev environment

Terminal dashboard that manages your entire Docker Compose stack. Dual-mode: interactive TUI or headless MCP server.

| | |
|---|---|
| **TUI** | Blessed dashboard with splash screen, action menu, job queue, activity log, system doctor, first-run wizard |
| **MCP Tools** | create-instance (Saga rollback), remove, update, health check, view-logs, run-command, backup, restore |
| **Infrastructure** | YAML AST editing (not regex), POSIX file locks with stale PID recovery, gap-filling port allocator, Caddy TLS |
| **Tests** | 66 tests |
| **Stack** | TypeScript, Node.js 20+, blessed, Docker Compose, Caddy |

```bash
npm install && npm run tui  # Interactive dashboard
npm run dev                  # Headless MCP server mode
```

---

### [staging-preview](https://github.com/jecis-repos/staging-preview) — Vercel-style PR previews on your own infra

Open a PR, get a live URL. Close it, instance destroyed. No vendor lock-in.

| | |
|---|---|
| **CI/CD** | GitHub Actions workflows for PR lifecycle + hourly orphan reconciliation |
| **Operations** | Self-healing maintenance daemon (348 lines), zstd database backups, GDPR data sanitization |
| **Infrastructure** | MCP provisioning orchestrator, branch-to-slug naming, systemd timers |
| **Tests** | 8 tests |
| **Stack** | Node.js 20+, GitHub Actions, Docker Compose, systemd, Caddy, PostgreSQL |

---

## Technical Articles

### [dev-articles](https://github.com/jecis-repos/dev-articles) — 5 deep-dive posts

| Article | Words | Topic |
|---------|-------|-------|
| **Building OAuth 2.1 for MCP in Laravel** | ~2,100 | PKCE S256, timing-safe verification, scope-encoded refresh tokens, per-user tool overrides |
| **Build a Staging System, Part 1: Saga Rollback** | ~1,500 | Compensating transactions for 16-step provisioning, ProvisionState with 8 boolean flags |
| **Build a Staging System, Part 2: YAML AST Editing** | ~1,500 | Docker Compose via parseDocument/YAMLMap — not regex. Post-write validation |
| **Build a Staging System, Part 3: File Locks** | ~1,500 | PID-based advisory locking, stale detection, gap-filling port allocator |
| **Self-Correcting Agent Pipelines** | ~2,100 | 4-layer directed pipeline, failure feedback loops, 7-state conversation machine |

---

## Numbers

```
Repositories:     6 (5 public + 1 private engine)
Total tests:      228+
Total assertions: 624+
Lines of code:    19,000+
Languages:        PHP, TypeScript, Bash
Test frameworks:  PHPUnit 11, Vitest
```

---

## Background

Multi-tenant SaaS, CI/CD pipelines processing 500+ PRs per quarter, AI infrastructure with 40+ MCP tools, Docker orchestration across multiple countries — after years of solving the same problems in different codebases, I started writing the solutions properly. Once. With tests.

Every line written the way I wish these tools had existed when I needed them.

---

**Jekabs Porietis** — [GitHub](https://github.com/jecis-repos) | [Threads](https://threads.net/@ananiel_)
