# lb-a
single nuxtjs app

## Communities
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

 
    
    state Config {
        [*] --> A 
    A --> B 
    
    --


    [*] --> C 
    C --> D 
    
    [*] --> E 
    E --> F 
    }
    
    state Show {
        Title --> Subtitle 
    Subtitle --> CommunityList 
    }
 
    [*] --> Config 
    Config --> Load 
    Load --> Show 
    Show --> End 
 
    [*] --> Config1 
    Config1 --> Load1 
    Load1 --> Show1 
    Show1 --> End 

Config1 --> Config1 : cc

A --> A : a
B --> B : b


C --> C : c
D --> D : d

E --> E : e
F --> F : f


Title --> Title : edit
Subtitle --> Subtitle : edit
CommunityList --> CommunityList : edit
    
```


```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram-v2
    Adopter.vue

    [*] --> Config : adopter.json
    Config --> Load : guestToken
    Load --> Show : (displayname, \nusername, \npassword)
    Show --> RequestPost : create
    RequestPost --> Show : (displayname, \nusername, \npassword)

    Config --> Load1 : userToken
    Load1 --> Show1 : (displayname,\nusername)

    Show1 --> RequestPut : update 
    RequestPut --> Show1 : (displayname, \nusername)

    Show1 --> RequestDelete : delete
    RequestDelete --> [*]

    state Load1 {
        [*] --> AdopterGet : userToken
        
        AdopterGet --> AdopterGetHandler : (owner,id)
        AdopterGet --> [*] : fail
    }
    
    state RequestPost {
        [*] --> AdopterPost : (displayname, \nusername, \npassword)
        AdopterPost --> AdopterPostHandler : (response) 
        AdopterPost --> [*] : fail 
    }

   state RequestPut {
        [*] --> AdopterPut : (displayname, \nusername)
        AdopterPut --> AdopterPutHandler : (response)
        AdopterPut --> [*] : fail 
    }
    
    state RequestDelete {
        [*] --> AdopterDelete : (owner,id)
        AdopterDelete --> AdopterDeleteHandler : (response) 
        AdopterDelete --> [*] : fail 
    }
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

