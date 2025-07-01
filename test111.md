graph TD
    A[Your Oracle Page] --> B[Load Checkout.js Script]
    B --> C{Script Source Domain?}
    C -->|devcheckout.usiopay.com| D[Set Sandbox Endpoints]
    C -->|checkout.usiopay.com| E[Set Production Endpoints]
    D --> F[GenerateToken: devcheckout.usiopay.com/2.0/GenerateToken]
    E --> G[GenerateToken: checkout.usiopay.com/2.0/GenerateToken]
    F --> H[Create Embedded iFrame]
    G --> H
    H --> I[User Fills Payment Form]
    I --> J[Form Submits to GenerateToken]
    J --> K[Return Token via postMessage]
    K --> L[Your Oracle App Receives Token]
    L --> M[Oracle Server Calls SubmitTokenPayment]
