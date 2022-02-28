# lb-a
single nuxtjs app

## Communities

```mermaid
flowchart TB
    classDef service fill:#fff;
    Init[Init] --> Load
    Load --> End
    * --> Open
    Open --> =
```

```mermaid
flowchart TB
    classDef service fill:#fff;
    
    Init --> Load
    Load --> Show

    CommunityGetRequest:::service
    
      subgraph Load1
        direction LR
        A1 --> |"(name)"| A2
        A3 --> |"(name)"| A4        
      end
      
    * --> Load1
    Load1 --> |"(config),[(community),...]"| Show1
    Show1 --> =

```

