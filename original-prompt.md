# Build a full-stack TanStack Start app with auth, database access, forms, and monitoring.

Prefer these integrations where they fit: WorkOS (Authentication), PowerSync (Databases), Prisma (Databases).
The request clearly calls for these integrations where they fit: CodeRabbit (Code Review), Cloudflare (Deployment/Hosting).
Make sure each requested or clearly implied partner integration is represented in the resulting project somehow. If one cannot be implemented cleanly, explain what was omitted and why instead of silently dropping it.
If a requested or inferred partner is not available as a real TanStack CLI add-on, do not invent one. Follow the partner's official install path, keep secrets server-side, and fall back to setup notes or TODOs when the integration depends on external infra, dashboards, licenses, or GitHub App installs.
Install the official PowerSync web client packages such as @powersync/web and @journeyapps/wa-sqlite when PowerSync is explicitly requested.
If TanStack collections or query integration fits, wire the official TanStack PowerSync packages rather than inventing a custom bridge.
Leave backend connector, auth token, and sync infrastructure setup explicit instead of pretending PowerSync can be fully demoed without backend prerequisites.
Do not add runtime app code for CodeRabbit.
Treat CodeRabbit as external repository tooling configured through the GitHub App, with optional .coderabbit.yaml guidance if useful.
Mention the GitHub App install/setup path briefly instead of pretending CodeRabbit is an in-app SDK integration.
Prefer the standard repository integration for pull request reviews first instead of inventing a custom workflow.
Only add CodeRabbit IDE or CLI workflows if they clearly support the requested developer workflow.
Include and demonstrate these TanStack libraries in the project: TanStack Start, TanStack Router, TanStack Intent, TanStack CLI, TanStack Form.

Start by scaffolding the project with the TanStack CLI.
Use this command: npx @tanstack/cli@latest create my-tanstack-app --agent --deployment cloudflare --add-ons tanstack-query,neon,better-auth,drizzle,form,sentry
If the execution environment starts from an existing platform template or custom starter instead of the TanStack CLI output, still run the TanStack CLI command in a separate scratch directory.
Then merge the generated integrations, dependencies, config, scripts, and relevant file structure into the actual project instead of skipping the TanStack CLI result.
Do not drop requested partner integrations or stack choices just because the host platform bootstraps its own template. Represent them in the final project somehow, or explicitly call out what could not be represented and why.

After scaffolding, run npx @tanstack/intent@latest install and npx @tanstack/intent@latest list.
Use the installed TanStack Intent skills and package-shipped guidance before making architectural or library-specific changes. Do not guess when a shipped skill can tell you the current pattern.
Keep durable project context in AGENTS.md (or equivalent), including the exact TanStack CLI command used, any follow-up TanStack Intent commands, the chosen stack and integrations, environment variable requirements, deployment notes, key architectural decisions, known gotchas, and next steps.

Stack: Use React, the blank starter, with tanstack-query, neon, better-auth, drizzle, form, sentry, targeting cloudflare.
Toolchain: keep the default CLI toolchain.
Preserve the generated project structure unless there is a clear reason to change it.
Explain any environment variables and follow-up setup steps after scaffolding.  url: https://tanstack.com/start/latest
