# lb-a
single nuxtjs app

```mermaid
stateDiagram
   
    [*] --> [[ Community_Service ]]
    
    [[ Community_Service ]] --> success
    [[ Community_Service ]] --> fail
    fail --> [*]
    success --> Show
    Show --> [*]
```
Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
