# lb-a
single nuxtjs app

## Communities

```mermaid
flowchart TB
    classDef service fill:#fff;
    Init --> Load
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
    subgraph Open2
        direction LR
        A1 --> A2        
    end
      
    subgraph Open
      direction LR
      CommunityConfig --> |"(config:(title,subtitle))"| configHandler         
      CommunityGetRequest --> |"[(community:(dr_jurisdiction,count,lat,lon)),...]"| CommunityGetHandler
    end
    
    
    * --> Open
    Open --> |"(config),[(community),...]"| Display
    Display --> =

```

