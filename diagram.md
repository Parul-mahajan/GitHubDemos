``` mermaid

graph TD
    A[Order Service] -->|Send Order Data| B[Order Queue Azure Service Bus]
    B -->|Order Details| C[Inventory Service]
    C -->|Update Stock & Notify| D[Payment Queue Azure Service Bus]
    D -->|Payment Data| E[Payment Service]
    E -->|Process Payment| F[Payment Confirmation Queue Azure Service Bus]
    F -->|Payment Confirmation| G[Shipping Service]
    G -->|Shipping Info| H[Shipping Notification Queue Azure Service Bus]
    H -->|Notify Customer| I[Notification Service]
    
    classDef azure fill:#2D2D2D,stroke:#0078D4,stroke-width:2px,color:#FFFFFF,padding:20px;
    classDef service fill:#333333,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,padding:15px;
    
    class A,B,C,D,E,F,G,H,I azure;
    class A,C,E,G,I service;
