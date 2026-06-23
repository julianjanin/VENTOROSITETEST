1. Purpose
This appendix documents the academic literature and scientific paradigms that form the foundation of the Artificial Cognition Engine (ACE). It is intended for internal engineering reference and technical audits.

2. Cognitive Architectures & Agentic AI
The 8-stage perception-action cycle utilized by the ACE is grounded in classical and modern Cognitive Architectures.

Reference Paradigms: SOAR and ACT-R cognitive architectures.

Application: Moving beyond reactive LLM prompting, the ACE operates as an autonomous agentic loop, continuously perceiving state changes, updating internal representations, and planning actions independently of immediate user prompts.

3. Memory Systems (Dual-Process Architecture)
The ACE’s separation of the L1 rolling conversational cache (Redis) and the asynchronous Semantic Graph (Neo4j/Postgres) is derived from Dual-Process Memory models.

Literature: Research on Long-Horizon AI Agents.

Application: Decoupling the immediate episodic buffer from background semantic consolidation prevents "cognitive degradation" (context window collapse or hallucination drift) over thousands of longitudinal interactions.

4. Neuro-Symbolic AI & Knowledge Graphs
The system relies on a hybrid approach, combining the probabilistic nature of neural networks (LLMs) with the deterministic logic of structured knowledge graphs.

Literature: Advancements in Neuro-Symbolic AI and Directed Acyclic Graphs (DAGs) for explainability.

Application: LLMs are used strictly for extraction and semantic reasoning (System 1 thinking), while the Knowledge Graph enforces strict ontological constraints, provenance tracking, and auditable reasoning pathways (System 2 thinking).

5. Multi-Agent Systems & Planning Engines
Our transition from text-generation to multi-objective optimization is backed by research in multi-agent reinforcement learning and planning systems.

Application: The Planning Engine evaluates candidate directives against a weighted hierarchy of System, User, and Session objectives, selecting the action that mathematically maximizes human-centric outcomes (e.g., preserving dignity, minimizing cognitive load).
