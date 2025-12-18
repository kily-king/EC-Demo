
# Vending Machines
     - Role: Event producers (edge devices)
          - Physical devices generating telemetry and operational events
          - Events include health status, errors, transactions, connectivity, etc.
          - These events are pushed upstream in near real time

# Event Collector Application (Running on Amazon EKS)
     - Role: Ingestion & normalization layer
          - A containerized application running on Amazon EKS
          - Receives raw events from vending machines via APIs or protocols
          - Performs validation, enrichment, and normalization
          - Publishes standardized events to Kafka topics in Amazon MSK
     - Why EKS:
          - Horizontal scalability
          - High availability
          - Cloud-native deployment and upgrades
