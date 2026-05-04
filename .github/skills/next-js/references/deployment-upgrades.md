# Deployment And Upgrades

This reference captures the deployment guidance, static export, build output, and upgrade details bundled into this skill.

## Build And Start
The current docs cover the standard production build and start workflow for Next.js.

Use only the exact commands confirmed by the current lookup when the user asks for local production verification or deployment preparation.

## Deployment Targets
The docs cover deployment guidance for running Next.js on a Node.js server and also cover Docker deployment.

If the user asks about a specific hosting platform, adapter, runtime, or platform-managed feature, refresh the docs for that exact target before answering.

## Static Export
The docs cover static export through the documented `output` configuration.

When static export is involved, do not assume server features remain available. Use only the limitations and capabilities confirmed by the current lookup for that export mode.

## Build Output Configuration
The docs cover output-related configuration examples such as a custom `distDir` in current migration guidance.

Keep output configuration examples restricted to the exact keys and behavior confirmed by the current lookup.

## Upgrades
The current Next.js docs include upgrade guidance and version-specific migration notes.

If the task depends on a particular upgrade path, async request API change, codemod, or bundler default, refresh the docs for that exact version-to-version step before adding detail.

## Topics Requiring Fresh Lookup
This reference does not lock in every version-specific breaking change, adapter API detail, platform recommendation, or static-export limitation. If those details are needed, explicitly say this skill does not confirm them.