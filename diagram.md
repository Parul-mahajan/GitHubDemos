# Order Processing Flow

```mermaid
graph TD
    A[Payment Service] -->|Send Payment Confirmation| B[Payment Confirmation Queue]
    A -->|Payment Failed| F[Error Queue]

    B --> C[Inventory Service]
    C -->|Update Stock| D[Shipping Queue]
    C -->|Stock Update Failed| G[Inventory Error Queue]

    D --> E[Shipping Service]
    D -->|Shipping Error| F

    %% Assigning colors for clarity
    classDef azure fill:#2D2D2D,stroke:#0078D4,stroke-width:2px,color:#FFFFFF,padding:20px;
    classDef service fill:#333333,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,padding:15px;
    classDef error fill:#f44336,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,padding:15px;

    class A,B,C,D,E,F,G azure;
    class A,C,E service;
    class F,G error;
