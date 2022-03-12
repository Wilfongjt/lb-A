# lb-a
single nuxtjs app

## Communities
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

 
    
    
    state LoadGuest1 {
        [*] --> S1
        S1 --> [abc] : guest

    }
    state LoadUser1 {
       
        [*] --> Authenticated
        Authenticated --> xxx : user
    }
 
    Adopter --> Config : adopter.json
    Config --> Load : (title,subtitle,displayname,username,password,services)
    Load --> End : owner,id
 
    [*] --> Config1 : adopter.json
    Config1 --> Load1 : (title,subtitle,displayname,username,password,services)
    Load1 --> [*] : token
```

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
      stateDiagram

        Community.vue --> Config : (community.json)
        Config --> Load : (community)
        Load --> Show : (communityList)
        Show --> End : (html)
        
        
        state Config1 {
            [*] --> CommunityConfig
            CommunityConfig --> CommunityConfigHandler : (title,subtitle,services)
        }
        
        state Load1 {
          [*] --> acommunityGET
          acommunityGET --> bcommunityGETHandler : [(name,count,lat,lon),...]
          bcommunityGETHandler --> ccommunityGET
          --
          [*] --> communityGET
          communityGET --> communityGETHandler : [(name,count,lat,lon),...]
          communityGETHandler --> xcommunityGET
          xcommunityGET --> xcommunityGETHandler : [(name,count,lat,lon),...]
          xcommunityGETHandler
          --
          [*] --> A
          A --> B

        }
        
        [*] --> Config1  : (community.json)
        Config1 --> Load1
        Load1 --> Show1 : (communityList)
        Show1 --> [*] : (html)
        
```


```mermaid
flowchart TB
 
    classDef service fill:#fff;
 
    
        subgraph *
          direction LR
          
        end
    
        subgraph Config1
          direction LR
              CommunityConfig[CommunityConfig] --> CommunityConfigHandler[CommunityConfigHandler]
        end
    
        subgraph Load1
          direction LR
              Community[Community] --> |"[(name,count,lat,lon),...]"| CommunityGETHandler[CommunityGETHandler]
        end
    
        subgraph Show1
          direction LR
              Click_Community[Click Community] --> Go_To_Community_Map[Go To Community Map]
        end
 
        Community --> Config
        Config --> Load
        Load --> Show
        Show --> End
 
        * --> Config1
        Config1 --> Load1
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

