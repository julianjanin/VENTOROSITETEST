1. Roadmap Overview
This roadmap covers the initial 4-week sprint to build the Phase 1 Voice Companion and the foundational hooks for the Artificial Cognition Engine (ACE). The focus is entirely on establishing the streaming pipeline, tuning the acoustic endpoints, and wiring the asynchronous memory components.

Sprint 1: The Streaming Pipeline (Critical Latency Path)

Goal: Wire up the WebSockets to connect a low-latency Speech-to-Text provider (like Deepgram Nova-3), the core LLM, and a fast Text-to-Speech engine (like Cartesia or ElevenLabs).


Task 1.1: Twilio Handshake: Scaffold a FastAPI server to handle the incoming Twilio webhook. Your server must reply with a snippet of XML (TwiML) to keep the phone line open, fork the audio, and establish a bidirectional WebSocket connection (wss://) directly to your backend.

Task 1.2: The Pipecat Orchestrator: Initialize the Pipecat framework. Open a WebSocket route and configure Pipecat's TwilioFrameSerializer to handle the incoming audio bytes.


Task 1.3: Audio Translation: Explicitly configure the STT provider and the TTS provider to operate strictly at an 8000Hz sample rate and use the μ-law encoding format. Pipecat's native Twilio serializers must automatically decode and upsample inbound Twilio streams, and correctly format the outbound TTS bytes.


Task 1.4: Model Integration: Connect the Deepgram streaming STT API, the core Layer 1 LLM, and the Cartesia/ElevenLabs TTS API to the Pipecat pipeline.

Sprint 2: Memory & Orchestration (State & Episodic)

Goal: Set up a database like Supabase to handle the asynchronous long-term memory extraction and retrieval.


Task 2.1: L1 Cache (Redis): Implement Redis to hold the immediate, rolling transcript of the current session. Ensure that as the user speaks, text is appended to Redis so the LLM can instantly pull context from the last 30 seconds.

Task 2.2: L2 Storage (Supabase): Provision a Supabase PostgreSQL instance. Create the initial append-only tables for Episodic Memory to store the raw interactions and transcripts permanently.

Task 2.3: Event Bus Initialization: Deploy a Redis Streams (or similar pub/sub) instance. Configure the Voice Layer to emit a ConversationCompleted event when a Twilio call terminates, pushing the payload (with a transcript pointer and session metrics) to the bus.

Sprint 3: Turn-Taking & The "Elderly Factor"

Goal: Tune the Voice Activity Detection (VAD) and system prompts. This is where you adjust the mechanics so the agent feels like a patient listener.


Task 3.1: VAD Silence Thresholds: Standard tech-industry VAD configurations assume a user is done speaking after 500ms of silence, which will cause the AI to constantly interrupt elderly users. You must intentionally force the AI to wait 1.5 to 2 seconds before it decides the user is finished speaking.


Task 3.2: Barge-In Handling: Implement logic so that when the VAD detects the user speaking, it instantly cuts off the TTS audio, cancels the current LLM generation, and instructs the pipeline to listen again.


Task 3.3: System Prompt Injection: Write the initial Layer 1 system prompt, defining its immediate persona and operational constraints (e.g., "Keep responses under three sentences; ask only one question at a time").

Sprint 4: Frontend & Testing (Deployment)

Goal: Scaffold a simple web interface or dialing system to house the application and conduct live conversations to test the flow.


Task 4.1: Cloud Deployment: Deploy the FastAPI server to AWS or GCP. Ensure the server region physically matches Twilio's edge location (e.g., deploying to us-east-1 if Twilio ingests the call in Ashburn, Virginia) to minimize network hop latency.


Task 4.2: Acoustic QA via Claude Code: Because Claude Code is a text-based CLI and suffers from "Audio Blindness," a human engineer must run the code, test the microphone, listen for audio clipping or unnatural overlaps, and manually describe those acoustic errors back to the agent so it can adjust the code.


Task 4.3: End-to-End Latency Tracing: Implement telemetry to measure end-to-end latency across every stage (Twilio → STT → LLM first token → TTS first byte → playback) to identify bottlenecks.
