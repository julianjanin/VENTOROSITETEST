Topology
The ACE utilizes a pub/sub Event Bus, such as Redis Streams or RabbitMQ.

Services are strictly decoupled, meaning producers do not know about consumers.

2. Core Event Schemas

ConversationCompleted: Emitted by Layer 1 (Voice) when a call terminates. Contains a transcript_uri pointer to raw text and session_metrics (duration, latency, interruption count).


FactExtracted: Emitted by Stage 2 of the Cognition Pipeline. Contains the entity_id and provenance metadata.


ObjectiveScored: Emitted by the Planning Engine. Contains an array of candidate_actions and the selected_action JSON directive.


SafetyAlertTriggered: Emitted by the Behavioral Analysis worker. Contains a severity rating (LOW, MEDIUM, CRITICAL) and the reasoning_graph IDs that triggered the alert.
