```mermaid
graph TD
    classDef default fill:#f9f9f9,stroke:#333,stroke-width:2px,color:black;
    classDef input fill:#CCFFCC,stroke:#333,stroke-width:2px,color:black;
    classDef hidden fill:#FFCCCC,stroke:#333,stroke-width:2px,color:black;
    classDef output fill:#CCCCFF,stroke:#333,stroke-width:2px,color:black;
    classDef weight fill:#FFFFCC,stroke:#333,stroke-width:2px,color:black;
    classDef loss fill:#FF9999,stroke:#333,stroke-width:2px,color:black;
    classDef gradient fill:#99CCFF,stroke:#333,stroke-width:2px,color:black;

    subgraph "Forward Pass"
        subgraph "Time t-2"
            Xt-2[x<sub>t-2</sub>]:::input
            Ht-2[h<sub>t-2</sub>]:::hidden
            Yt-2[y<sub>t-2</sub>]:::output
        end

        subgraph "Time t-1"
            Xt-1[x<sub>t-1</sub>]:::input
            Ht-1[h<sub>t-1</sub>]:::hidden
            Yt-1[y<sub>t-1</sub>]:::output
        end

        subgraph "Time t"
            Xt[x<sub>t</sub>]:::input
            Ht[h<sub>t</sub>]:::hidden
            Yt[y<sub>t</sub>]:::output
        end

        Wx["W<sub>x</sub>"]:::weight
        Wh["W<sub>h</sub>"]:::weight
        Wy["W<sub>y</sub>"]:::weight

        Xt-2 -->|"W<sub>x</sub>"| Ht-2
        Ht-2 -->|"W<sub>h</sub>"| Ht-1
        Ht-2 -->|"W<sub>y</sub>"| Yt-2

        Xt-1 -->|"W<sub>x</sub>"| Ht-1
        Ht-1 -->|"W<sub>h</sub>"| Ht
        Ht-1 -->|"W<sub>y</sub>"| Yt-1

        Xt -->|"W<sub>x</sub>"| Ht
        Ht -->|"W<sub>y</sub>"| Yt

        Wx -.-> Xt-2
        Wx -.-> Xt-1
        Wx -.-> Xt

        Wh -.-> Ht-2
        Wh -.-> Ht-1

        Wy -.-> Ht-2
        Wy -.-> Ht-1
        Wy -.-> Ht
    end

    subgraph "Backward Pass (BPTT)"
        Lt-2[L<sub>t-2</sub>]:::loss
        Lt-1[L<sub>t-1</sub>]:::loss
        Lt[L<sub>t</sub>]:::loss

        Yt-2 --> Lt-2
        Yt-1 --> Lt-1
        Yt --> Lt

        Lt-2 -->|"∂L/∂y<sub>t-2</sub>"| Yt-2
        Lt-1 -->|"∂L/∂y<sub>t-1</sub>"| Yt-1
        Lt -->|"∂L/∂y<sub>t</sub>"| Yt

        Yt-2 -->|"∂L/∂h<sub>t-2</sub>"| Ht-2
        Yt-1 -->|"∂L/∂h<sub>t-1</sub>"| Ht-1
        Yt -->|"∂L/∂h<sub>t</sub>"| Ht

        Ht -->|"∂L/∂h<sub>t-1</sub>"| Ht-1
        Ht-1 -->|"∂L/∂h<sub>t-2</sub>"| Ht-2

        GradWh["∇W<sub>h</sub>"]:::gradient
        Ht-2 -->|"∂L/∂W<sub>h</sub>"| GradWh
        Ht-1 -->|"∂L/∂W<sub>h</sub>"| GradWh

        UpdateWh["W<sub>h</sub> = W<sub>h</sub> - η∇W<sub>h</sub>"]:::weight
        GradWh --> UpdateWh
        Wh --> UpdateWh
    end

    subgraph "Wh Optimization"
        WhCalc["W<sub>h</sub> calculation:<br/>h<sub>t</sub> = tanh(W<sub>h</sub>h<sub>t-1</sub> + W<sub>x</sub>x<sub>t</sub> + b)"]:::weight
        GradWhCalc["∇W<sub>h</sub> calculation:<br/>∇W<sub>h</sub> = Σ<sub>t</sub> ∂L/∂h<sub>t</sub> · ∂h<sub>t</sub>/∂W<sub>h</sub>"]:::gradient
        WhUpdate["W<sub>h</sub> update:<br/>W<sub>h</sub> = W<sub>h</sub> - η∇W<sub>h</sub>"]:::weight
    end

    WhCalc -.-> Wh
    GradWhCalc -.-> GradWh
    WhUpdate -.-> UpdateWh
\```
