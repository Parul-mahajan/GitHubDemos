# Category Processing Flow

```mermaid
sequenceDiagram
    participant User as User
    participant Browser as Browser (Frontend)
    participant Flask as Flask Backend
    participant ServiceBus as Azure Service Bus
    participant Subscription as Subscription(s)
    
    User->>Browser: Fill form (email, category)
    Browser->>Flask: POST /subscribe (email, category)
    Flask->>ServiceBus: Create Subscription with Filter<br>("category = <category>")
    ServiceBus-->>Flask: Subscription Created
    Flask-->>Browser: Success Message ("Subscription Created")
    
    User->>Browser: Publishes Content
    Browser->>Flask: POST /publish (content, category)
    Flask->>ServiceBus: Send Message to Topic<br>with "category" Property
    ServiceBus->>Subscription: Deliver Message to Matching Subscription(s)
    Subscription->>Flask: Message Received<br>(Optional API/Logic for Consumption)
    Subscription-->>User: Notify Subscribers<br>(via email, app, etc.)

