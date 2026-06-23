1. The Perception-Action Cycle
The ACE operates on an 8-stage continuous loop.

Voice and telemetry interfaces act purely as sensory inputs that trigger the loop and execute outputs; they do not possess reasoning capabilities.

2. The 8-Stage Execution Pipeline

Experience: Ingestion of raw events (transcripts, telemetry, caregiver inputs) via the Event Bus.


Facts: Deterministic extraction of verifiable objective data (e.g., "User stated they have a headache").


Beliefs: Synthesis of Facts into an internal state model (e.g., "User is currently experiencing physical discomfort").


Reasoning: Construction of a Directed Acyclic Graph (DAG) linking Beliefs back to underlying Facts to ensure explainability.


Predictions: Probabilistic forecasting of immediate future states (e.g., "User is likely to skip their morning walk").


Plans: Generation of candidate actions based on Predictions and World State.


Objectives: Multi-variable optimization scoring candidate actions against System, User, and Session goals.


Actions: The selected highest-value directive published back to the Event Bus for execution by Layer 1 clients.
