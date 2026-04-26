---
name: laravel-ai-sdk
description: 'Use when: working with Laravel AI SDK, laravel/ai, AI agents, Promptable, agent(), Agent, Conversational, HasTools, HasStructuredOutput, HasMiddleware, Tool, JsonSchema, AgentPrompt, AgentResponse, provider/model attributes, make:agent, make:tool, ai:chat, images, audio, transcription, embeddings, reranking, vector stores, file management, testing fakes, and Laravel AI code reviews. Requires Context7 /laravel/ai docs before adding details.'
argument-hint: 'Laravel AI SDK task, agent/tool/structured output/provider setup, image/audio/embedding/reranking/testing, or code review'
---

# Laravel AI SDK

## Purpose
Use this skill to create, review, or explain Laravel AI SDK (`laravel/ai`) usage using only details confirmed in the current Context7 documentation for `/laravel/ai`.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/laravel/ai` with the exact Laravel AI SDK topic the user asks about.
2. Do not add installation commands, provider names, model names, config keys, environment variables, namespaces, contracts, traits, methods, response properties, command flags, testing helpers, or capability APIs unless they appear in the retrieved documentation or the reference files below.
3. If the user asks about behavior not confirmed by the current Context7 result, run a narrower Context7 lookup or explicitly say the current Laravel AI SDK documentation context does not confirm it.
4. Preserve documented casing and namespaces. The confirmed namespace pattern is `Laravel\Ai`, and the docs explicitly mark `Illuminate\Ai\Image` and `Laravel\AI\Agent` as wrong.
5. Do not infer behavior from general Laravel conventions, provider SDKs, HTTP clients, package source code, older examples, or non-Context7 memory.

## Reference Map
- Configuration defaults, provider keys, model selection, artisan commands, and correct namespace imports: [configuration-and-commands.md](./references/configuration-and-commands.md)
- Agent contracts, prompting, tools, structured output, middleware, and streaming: [agents-tools-structured.md](./references/agents-tools-structured.md)
- Broad capabilities, testing boundaries, and unconfirmed-detail handling: [capabilities-testing-boundaries.md](./references/capabilities-testing-boundaries.md)

## Workflow
1. Identify the requested surface: configuration, provider/model selection, agent creation, prompt calls, tools, structured output, middleware, streaming, CLI, images, audio, transcription, embeddings, reranking, vector stores, file management, testing/fakes, or code review.
2. Run a narrow Context7 query for `/laravel/ai` before producing code, commands, or review findings.
3. Load the relevant reference file from the map above.
4. For configuration, use only documented `config/ai.php` keys and provider entries from the current lookup or [configuration-and-commands.md](./references/configuration-and-commands.md).
5. For provider/model selection, use only documented inline `provider` / `model` arguments, provider failover arrays, or the documented `Provider`, `Model`, `UseSmartestModel`, and `UseCheapestModel` attributes.
6. For agents, keep to documented contracts and trait usage: `Agent`, `Conversational`, `HasTools`, `Promptable`, `instructions()`, `messages()`, `tools()`, `make()`, `prompt()`, and the `Laravel\Ai\agent` helper.
7. For tools, use only documented `Tool`, `description()`, `handle(Request $request)`, `schema(JsonSchema $schema)`, and `Laravel\Ai\Tools\Request` behavior.
8. For structured output, require documented `HasStructuredOutput`, `schema(JsonSchema $schema)`, JSON Schema field definitions, and documented array-style response access.
9. For middleware, require documented `HasMiddleware`, `middleware()`, middleware `handle(AgentPrompt $prompt, Closure $next)`, `AgentResponse`, and documented response usage fields.
10. For streaming, use only the documented agent `stream()` example unless a fresh lookup confirms more streaming APIs.
11. For images, audio, transcription, embeddings, reranking, vector stores, file management, and testing fakes, do not invent method names. Query Context7 for the exact capability and include only the APIs returned by that lookup.
12. For reviews, verify every namespace, contract, trait, method, command, config key, env var, provider driver, model name, response property, and testing helper against the current Context7 result and the reference files.

## Confirmed Core Patterns
- `laravel/ai` is documented as the official Laravel AI SDK package.
- The SDK is documented as a unified API for agents, image generation, audio synthesis, transcription, embeddings, reranking, vector stores, and file management.
- Configuration is documented in `config/ai.php` with separate defaults for general use, images, audio, transcription, embeddings, and reranking.
- Documented provider configuration entries include `openai`, `anthropic`, `gemini`, `azure`, `ollama`, and `cohere`.
- Documented agent classes implement `Laravel\Ai\Contracts\Agent` and use `Laravel\Ai\Promptable`.
- Documented agent capabilities include conversational messages, tools, structured output, middleware, provider/model selection, prompt calls, and streaming.
- Documented tool classes implement `Laravel\Ai\Contracts\Tool` and define description, handler, and JSON Schema input methods.
- Documented testing support exists through `fake()` methods and assertions for agents, images, audio processing, transcription, embeddings, reranking, file storage, and knowledge base stores, but exact helper names must be confirmed with a fresh lookup before use.

## Completion Check
- A fresh Context7 lookup for `/laravel/ai` was performed for the user's exact topic.
- All commands, config keys, env vars, namespaces, interfaces, traits, methods, response fields, model names, provider names, and testing helpers are confirmed by the current lookup or these reference files.
- Broad capability claims are not turned into concrete APIs unless the current lookup documents those APIs.
- Unsupported or unconfirmed details are omitted or explicitly described as not confirmed by the current Laravel AI SDK documentation context.