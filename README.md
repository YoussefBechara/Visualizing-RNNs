```mermaid
graph TD
    subgraph "Time t-1"
        Ht-1["h<sub>t-1</sub> = [0, 0, 0]"]
        style Ht-1 fill:#FF9999,stroke:#333,stroke-width:2px,color:#000
    end
    
    subgraph "Input at t"
        Xt["x<sub>t</sub> = [0.5, -0.2]"]
        style Xt fill:#99FF99,stroke:#333,stroke-width:2px,color:#000
    end
    
    subgraph "Weights"
        Wh["W<sub>h</sub> = [0.1 0.2 0.3;<br/>0.4 0.5 0.6;<br/>0.7 0.8 0.9]"]
        Wx["W<sub>x</sub> = [0.1 -0.1;<br/>0.2 -0.2;<br/>0.3 -0.3]"]
        style Wh fill:#9999FF,stroke:#333,stroke-width:2px,color:#000
        style Wx fill:#FF99FF,stroke:#333,stroke-width:2px,color:#000
    end
    
    B["b<sub>h</sub> = [0.1; 0.1; 0.1]"]
    style B fill:#FFFF99,stroke:#333,stroke-width:2px,color:#000
    
    Ht-1 -->|"W<sub>h</sub> · h<sub>t-1</sub>"| Sum1["[0; 0; 0]"]
    Xt -->|"W<sub>x</sub> · x<sub>t</sub>"| Sum2["[0.07; 0.14; 0.21]"]
    
    Sum1 --> Sum((+))
    Sum2 --> Sum
    B --> Sum
    
    Sum -->|"Pre-activation<br/>[0.17; 0.24; 0.31]"| Tanh["tanh()"]
    Tanh -->|"h<sub>t</sub> = [0.168; 0.236; 0.301]"| Ht
    
    subgraph "Time t"
        Ht["h<sub>t</sub> = [0.168, 0.236, 0.301]"]
        style Ht fill:#FF9999,stroke:#333,stroke-width:2px,color:#000
    end
    
    style Sum1 fill:#FFB366,stroke:#333,stroke-width:2px,color:#000
    style Sum2 fill:#66B3FF,stroke:#333,stroke-width:2px,color:#000
    style Sum fill:#FF66B3,stroke:#333,stroke-width:2px,color:#000
    style Tanh fill:#B366FF,stroke:#333,stroke-width:2px,color:#000

\```
