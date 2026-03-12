# Promptfoo Key Features & Capabilities

This document summarizes Promptfoo's core capabilities based on both product documentation and implementation in `src/`.

## 1) Core LLM evaluation platform (CLI + library)

- Promptfoo is positioned as an open-source framework for **evaluating and red-teaming LLM applications**.
- The `promptfoo` CLI exposes first-class commands for evaluation workflows (`eval`, `view`, `validate`, `export`, etc.), with shared options for verbose logging and `.env` loading.
- The Node library API (`evaluate`) supports programmatic test execution and can optionally persist and share results.

## 2) Test-driven prompt/model development

- Docs emphasize a **test-driven workflow**: define test cases, run evals, analyze scores, iterate.
- Evaluation execution includes loading providers, resolving prompt/provider/test configuration, running assertions, and producing structured outputs.
- Promptfoo supports writing eval outputs to files and generating shareable links when sharing is enabled.

## 3) Rich assertion and grading system

- Promptfoo includes a broad assertion engine with deterministic checks and model-graded checks.
- Built-in assertion handlers cover lexical checks (`contains`, `regex`, `starts-with`), structure checks (`is-json`, `is-sql`, `is-xml`), quality metrics (`bleu`, `rouge`, `levenshtein`), LLM-judged metrics (`factuality`, `answer-relevance`, `llm-rubric`), safety/moderation checks, latency/cost checks, tool-call validation, tracing assertions, and webhook/custom script integrations.
- Model-graded assertion categories are explicitly tracked to support evaluator behavior and orchestration.

## 4) Broad model/provider interoperability

- Docs position Promptfoo as supporting 50+ providers and custom APIs.
- Provider loading supports:
  - provider IDs resolved through a registry,
  - `file://` provider definitions from YAML/JSON,
  - per-provider/per-suite environment overrides,
  - cloud-linked provider resolution,
  - function-based custom providers.
- This enables side-by-side benchmarking across hosted APIs and self-hosted/open-source models.

## 5) Automated red teaming for AI security

- Red teaming is a primary product pillar: adversarial test generation, automated grading, risk quantification, and reporting.
- The redteam command family includes generation, discovery, run, report, setup, and plugin management workflows.
- The redteam plugin system includes many security categories (e.g., prompt extraction, SQL injection, shell injection, PII and policy-related checks, excessive agency, hallucination, toxic content, tool discovery), and can generate tests locally or via remote generation endpoints.
- The library API also exposes redteam extractors, graders, plugins, strategies, and programmatic `generate`/`run` entry points.

## 6) AI code scanning for LLM vulnerabilities

- Promptfoo includes a dedicated `code-scans` command group for scanning repositories for LLM-specific risks.
- Documentation describes agentic code scanning that traces data flow to detect issues like prompt injection and PII exposure in pull requests and CI workflows.

## 7) Model artifact auditing (ModelAudit integration)

- The CLI includes `model-scan` capabilities that integrate with `modelaudit` tooling for model artifact security analysis.
- Implementation includes modelaudit version checks, subprocess management, result parsing, and sharing support for model audit results.

## 8) Dataset and assertion generation utilities

- Promptfoo can generate synthetic datasets (`generate dataset`) from test suites with persona/test-case controls, optional writing back into config, and CSV/YAML export.
- It also provides assertion generation tooling to accelerate benchmark authoring.

## 9) Web UI + local server for analysis and collaboration

- Promptfoo ships an Express-based local server and web app support for viewing eval history/results.
- Server APIs expose health checks, result history, prompts, datasets, sharing endpoints, and redteam/provider/model-audit related routes.
- This enables local analysis workflows in addition to CLI output.

## 10) Integrations, automation, and developer ergonomics

- Built-in telemetry hooks and command usage tracking are wired into command lifecycle hooks.
- CI/CD usage is a documented first-class workflow for both eval regression checks and security scanning.
- Ancillary capabilities include config init helpers, caching controls, retry/config/debug commands, import/export, and MCP server mode (`promptfoo mcp`) for external tool integration over HTTP or stdio.

---

## Source Basis (sample)

Primary files reviewed for this summary:

- Documentation: `README.md`, `site/docs/intro.md`, `site/docs/red-team/index.md`, `site/docs/code-scanning/index.md`
- Source: `src/main.ts`, `src/index.ts`, `src/assertions/index.ts`, `src/providers/index.ts`, `src/redteam/plugins/index.ts`, `src/codeScan/index.ts`, `src/commands/modelScan.ts`, `src/commands/generate/dataset.ts`, `src/commands/mcp/index.ts`, `src/server/server.ts`
