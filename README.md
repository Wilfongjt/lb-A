# lb-a
single nuxtjs app

## Communities

```mermaid
 flowchart TB
       
          classDef service fill:#fff;
       
          
              subgraph *
                  direction LR
                  
              end
          
              subgraph Load1
                  direction LR
                  A --> B
                  
              end
          
              subgraph Show1
                  direction LR
                  C --> D
              end
       
              Start --> Load
              Load --> Show
              Show --> End
       
              * --> Load1
              Load1 --> Show1
              Show1 --> =
     
```

```mermaid
flowchart TB
    classDef service fill:#fff;
    classDef function fill:#ccc;
    classDef data fill:#aaa;
    
    Start --> Load
    Load --> Show
    Show --> End
    
    A1:::function 
    A3:::service
    
subgraph Load1
        direction LR
        CommunityConfig --> |"(title,subtitle)"| CommunityConfigHandler
CommunityGETRequest --> |"(name)"| CommunityGETHandler        
      end
     
     
    * --> Load1
    Load1 --> |"(config),[(community),...]"| Show1
    Show1 --> =
    
    

    
    A --> Legend
    Legend --> B
    B --> C
    
```

