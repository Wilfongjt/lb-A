# Community
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

 
    
    [*] --> Terms_of_Use : /tou
    Terms_of_Use --> [*]
    Terms_of_Use --> Terms_of_Use
    
    [*] --> Opportunities : /opportunities
    Opportunities --> [*]
    Opportunities --> Opportunities
    
    [*] --> Sponsors : /sponsors
    Sponsors --> [*]
    Sponsors --> Sponsors
    
    [*] --> Stats : /stats
    Stats --> [*]
    Stats --> Stats
    
    [*] --> About : /about
    About --> [*] 
    About --> About
 
 
 
```
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
        [*] --> CommunityGet 
        CommunityGet --> CommunityGetHandler : [(name,count,lat,lon),...]
        CommunityGetHandler --> [*] : (communityList)
    }
    state Show {
        Title --> Subtitle 
        
        Subtitle --> CommunityList 
    }
   
    [*] --> [*] : (isModalVisible=false)
    [*] --> Config : isModalVisible=true
    Config --> Load : (name,page,isModalVisible,community_get)
    Load --> Show : (communityList)
    Load --> ShowError : (fail)
    ShowError --> [*] : (isModalVisible=false)
    ShowError --> ShowError : (isModalViaible=true)
    Show --> [*] : (isModalVisible=false)
    Show --> Show : (isModalVisible=true)
    Title --> Title : hi
    
```
# Community Load

[[Start]]

...

[[Load]]

[Start]

[CommunityGet]

Edge: a, goto_a



[CommunityGetHandler]

Edge: 

[End]

...

[[End]]
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    direction LR
     state CommunityGet {
     [*] --> a : goto_a
      a --> b : goto_b
      b --> [*] : 
    }
    state CommunityGetHandler {
      [*] --> x
      x --> y
      y --> [*]
    }
    [*] --> CommunityGet 
        CommunityGet --> CommunityGetHandler : [(name,count,lat,lon),...]
        CommunityGetHandler --> [*] : (communityList)
        
        
```

