graph LR
    subgraph "Time t-1"
        Ht-1[h<sub>t-1</sub>]
    end
    subgraph "Time t"
        Xt[x<sub>t</sub>]
        Ht[h<sub>t</sub>]
    end
    subgraph "Weights"
        Wh[W<sub>h</sub>]
        Wx[W<sub>x</sub>]
    end
    B[b<sub>h</sub>]
    
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
