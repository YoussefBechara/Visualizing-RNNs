```mermaid
graph LR
    subgraph "Time t-1"
        Ht-1[hₜ₋₁]
    end
    subgraph "Time t"
        Xt[xₜ]
        Ht[hₜ]
    end
    subgraph "Weights"
        Wh[Wₕ]
        Wx[Wₓ]
    end
    B[bₕ]
    
    Ht-1 -->|Hidden state| Wh
    Xt -->|Input| Wx
    Wh --> Sum((+))
    Wx --> Sum
    B -->|Bias| Sum
    Sum -->|Pre-activation| Tanh[tanh]
    Tanh --> Ht
    
    style Ht-1 fill:#f9f,stroke:#333,stroke-width:2px
    style Xt fill:#bbf,stroke:#333,stroke-width:2px
    style Ht fill:#f9f,stroke:#333,stroke-width:2px
    style Wh fill:#fbb,stroke:#333,stroke-width:2px
    style Wx fill:#fbb,stroke:#333,stroke-width:2px
    style B fill:#bfb,stroke:#333,stroke-width:2px
    style Sum fill:#ff9,stroke:#333,stroke-width:2px
    style Tanh fill:#f99,stroke:#333,stroke-width:2px
\```
