```mermaid

graph TD
    A[Order Service] -->|Send Order Data| B[Order Queue (Azure Service Bus)]
    B -->|Order Details| C[Inventory Service]
    C -->|Check Stock & Update| D[Payment Queue (Azure Service Bus)]
    D -->|Payment Data| E[Payment Service]
    E -->|Process Payment & Confirmation| F[Payment Confirmation Queue (Azure Service Bus)]
    F -->|Payment Confirmation| G[Shipping Service]
    G -->|Update Shipping Info & Tracking| H[Shipping Notification Queue (Azure Service Bus)]
    H -->|Send Notification to Customer| I[Notification Service]
    H -->|Generate Invoice| J[Invoice Service]
    B -->|Invalid Orders| K[Dead-letter Queue (DLQ)]
    classDef azure fill:#e6f7ff,stroke:#0078d4,stroke-width:2px;
    class A,B,C,D,E,F,G,H,I,J,K azure;
