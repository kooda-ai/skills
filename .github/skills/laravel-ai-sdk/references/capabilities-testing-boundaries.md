# Capabilities, Testing, And Boundaries

## Documented Capability Areas
The docs describe Laravel AI SDK as a unified API for:

- agents
- image generation
- audio synthesis
- transcription
- embeddings
- reranking
- vector stores
- file management

The docs also describe agents as capable of:

- tool utilization
- structured output generation
- image creation
- audio synthesis and transcription
- vector embedding generation
- document reranking

Only these capability areas are confirmed here. Exact method names and request/response shapes for broad capabilities must come from a fresh Context7 lookup before use.

## Testing And Faking
The docs state that Laravel AI supports testing and faking for:

- agents
- image generation
- audio processing
- transcription
- embeddings
- reranking
- file storage
- knowledge base stores

The docs state each capability provides a `fake()` method for setting up mock responses and assertion methods to verify interactions.

Do not name fake classes, assertion methods, assertion signatures, or fake response builders unless a fresh Context7 lookup returns those exact details.

## Common Boundary Checks
- Do not introduce an `AI` facade unless a fresh lookup confirms it.
- Do not add a Composer install command unless a fresh lookup confirms it.
- Do not add publish commands, migrations, queue setup, storage setup, or event setup unless a fresh lookup confirms them.
- Do not invent provider-specific capabilities or model compatibility rules.
- Do not convert broad support statements into concrete APIs.
- Do not import from `Illuminate\Ai` or `Laravel\AI`; the docs mark those namespace patterns as wrong.
- Do not use provider SDK class names unless Laravel AI docs show them.
- Do not assume testing helpers beyond the documented existence of `fake()` and assertions.

## Context7 Query Starters
Use narrow topic queries like these before final guidance:

```text
For Laravel AI SDK, show the documented API for image generation with exact namespaces, methods, request parameters, response properties, fakes, and assertions.
```

```text
For Laravel AI SDK, show the documented API for embeddings and reranking with exact namespaces, methods, config keys, caching behavior, fakes, and assertions.
```

```text
For Laravel AI SDK, show the documented testing API for agents, tools, structured output, streaming, images, audio, transcription, embeddings, reranking, file storage, and knowledge base stores.
```

```text
For Laravel AI SDK, show the documented installation and setup commands, service providers, config publishing, migrations, queues, and storage setup if any are documented.
```