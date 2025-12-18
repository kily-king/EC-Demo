
## Vending Machines
     - Role: Event producers (edge devices)
          - Physical devices generating telemetry and operational events
          - Events include health status, errors, transactions, connectivity, etc.
          - These events are pushed upstream in near real time

## Event Collector Application (Running on Amazon EKS)
     - Role: Ingestion & normalization layer
          - A containerized application running on Amazon EKS
          - Receives raw events from vending machines via APIs or protocols
          - Performs validation, enrichment, and normalization
          - Publishes standardized events to Kafka topics in Amazon MSK
     - Why EKS:
          - Horizontal scalability
          - High availability
          - Cloud-native deployment and upgrades

## Amazon MSK (Kafka Cluster)
     - Role: Central event backbone
          - Fully managed Apache Kafka service
          - Decouples producers (Event Collector) from consumers (Flink, Lambda, etc.)
          - Ensures durability, ordering, and replayability of events
     - Key benefit:
          - Acts as the single source of truth for all event streams

## Apache Flink (Streaming + Analytics)
     - Role: Real-time processing and analytics engine
          - Consumes events directly from MSK
          - Performs:
               - Stream processing
               - Aggregations and transformations
               - Windowed analytics (time-based insights)
               - Business rules and anomaly detection
     - Why Flink:
          - Handles both streaming and analytics in one engine
          - Low latency + stateful processing
          - Eliminates need for separate streaming and analytics services

## Amazon DynamoDB (Optional Stateful Store)
     - Role: State management for Flink jobs
          - Stores intermediate or long-lived state
          - Used for:
               - Device state
               - Counters
               - Session data
          - Enables fast, scalable key-value lookups
     - Optional:
          - Only needed if state must persist beyond Flink checkpoints

## AWS Lambda (Incident Orchestration)

Role: Event-driven automation

Triggered by processed events from Flink or MSK

Applies incident logic and workflows

Calls downstream systems (like ServiceNow)

Why Lambda:

No server management

Scales automatically

Ideal for short-lived orchestration logic






