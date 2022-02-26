# lb-a
single nuxtjs app



```mermaid
flowchart TB
    
    subgraph Init
      direction TB
    a1-->a2
    end
    
    subgraph Load
    b1-->b2
    end
    
    subgraph Show
    c1-->c2
    end
    
    Init --> |"(abc)"| Load
    Load --> |"[(ABC),...]"| Show
    
    
```


```mermaid
flowchart TB


classDef service fill:#fff;
BB:::service
classDef service fill:#fff; 
CC:::service
classDef service fill:#fff; 
DD:::service
classDef service fill:#fff; 

A(taskA) --> |xxx| B(taskB)
B(taskB) --> |bbb| C(taskC)
C(taskC) --> |ccc| D(taskD)
C(taskC) --> |bbb| DD[Service]

BB[ServiceB] --> |"(bbb)"| B
CC[ServiceC] --> |"[(ccc)]"| C
DD[ServiceD] --> |"[(ddd)]"| CC
```

```mermaid
stateDiagram
    [*] --> Communities: (click)
     
    Communities(ccc) --> Community_Service: mount
    
    Community_Service --> Show: [(dr_jurisdiction, count,lat,lon),...]
    Community_Service --> [*]: (empty)

    Show --> [*]
```
