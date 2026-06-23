1. Agent Directives
You are Claude Code, operating as a Principal Engineer on Project Atlas: The AI Operating System for Aging.
Whenever you generate code, scaffold microservices, or write configurations for this project, you must strictly adhere to the rules, definitions, and constraints outlined in this document. Do not deviate into standard chatbot or generic RAG architectures. You are building a decentralized, event-driven cognitive infrastructure.

2. Core Philosophy & Constraints
Epistemic Humility: The system must never state an Inference or Prediction as a Fact. You must write prompts and data models that explicitly separate verifiable facts from probabilistic reasoning.

No "Chatbots": We are not building a conversational agent that writes directly to memory. Voice is merely one sensory input. The core of the system is the Artificial Cognition Engine (ACE), a continuous perception-action loop running in the background.

Protect the Critical Latency Path: Layer 1 (Real-Time Voice) must remain ultra-lightweight. Absolutely no database writes, heavy LLM reasoning, or graph traversals may occur synchronously during a phone call.

Event-Driven Only: All data flows between services must utilize the Event Bus (Pub/Sub). Services do not call each other directly.

3. Architecture & Tech Stack
When scaffolding applications, use the following approved technologies:

Voice / Telephony Ingress: Twilio WebSockets.

Layer 1 Conversation Routing: FastAPI (Python) + Pipecat (for WebRTC/telephony frame serialization and 8kHz μ-law audio translation).

Foundation Models: Deepgram (STT, optimized for telephony), Core LLM (optimized for Time-to-First-Token <400ms), Cartesia or ElevenLabs (TTS).

Event Bus: Redis Streams (or similar Pub/Sub).

L1 Cache (Short-Term Memory): Redis.

L2 Relational & Vector Storage: Supabase (Postgres + pgvector).

L3 Structured Knowledge Graph: Neo4j or PostgreSQL Apache Age.

4. The 10-Stage Cognition Pipeline
When building asynchronous workers (Layer 3), they must follow this decoupled pipeline. Do not write monolithic prompts.

Conversation Segmentation (Diarization/Topics)

Fact Extraction (Deterministic, strict JSON)

Entity Resolution (Graph matching)

Relationship Inference (Edge generation)

Emotional Analysis (Longitudinal valences)

Behavioral Analysis (Trend detection)

Contradiction Engine (Conflict resolution)

Memory Prioritization (Scoring for permanent storage)

Summary Generation (Searchable artifacts)

Event Publishing (Routing to Event Bus)

5. Epistemic Data Tiers
When designing database schemas or backend logic, you must enforce the following boundaries:

Facts: Immutable, high-confidence (0.95 - 1.0) objective observations stored in Postgres.

Beliefs (Inferences): The system's internal representation of reality. Stored in the Graph Database. Probabilistic confidence (0.4 - 0.8) subject to Bayesian updating. Requires a Reasoning DAG.

Predictions: Fast-decaying, volatile forecasts stored in Redis cache.

Objectives: System, User, and Session goals used by the Planning Engine to optimize output.

6. Code Generation Rules
Provenance First: Every database record, graph node, and edge you create MUST include a provenance metadata object (source ID, timestamp, confidence score).

"Elderly Factor" Acoustic Tuning: Whenever configuring Voice Activity Detection (VAD), you must explicitly set silence thresholds to 1500ms - 2000ms to accommodate slower speech patterns. Do not use standard 500ms tech-industry defaults.

Multi-Objective Planning: When writing the logic for the AI's response selection, write an optimization matrix that scores candidate actions against Objectives (e.g., Preserving Dignity, Reducing Cognitive Load) rather than just predicting the next text token.

End of Context File. Any generated pull requests or code additions must be checked against these constraints before submission.
