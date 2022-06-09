# Opportunities

```mermaid

```

# Nav

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

        [*] --> Adoptions : is(/)
        Adoptions --> [*] : isNot(/)
        Adoptions --> Adoptions : is(/)
        

        [*] --> MyAdoptees : is(isModalVisible)
        MyAdoptees --> [*] : isNot(isModalVisible)
        MyAdoptees --> MyAdoptees : is(isModalVisible)
        

        [*] --> Communities : is(isModalVisible)
        Communities --> [*] : isNot(isModalVisible)
        Communities --> Communities : is(isModalVisible)
        

        [*] --> Signin : is(isModalVisible)
        Signin --> [*] : isNot(isModalVisible)
        Signin --> Signin : is(isModalVisible)
        

        [*] --> Signup : is(/adopter)
        Signup --> [*] : isNot(/adopter)
        Signup --> Signup : is(/adopter)
```

# Footer

```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

        [*] --> TOU : is(/tou)
        TOU --> [*] : isNot(/tou)
        TOU --> TOU : is(/tou)
        

        [*] --> Opportunities : is(/opportunities)
        Opportunities --> [*] : isNot(/opportunities)
        Opportunities --> Opportunities : is(/opportunities)
        

        [*] --> Sponsors : is(/sponsors)
        Sponsors --> [*] : isNot(/sponsors)
        Sponsors --> Sponsors : is(/sponsors)
        

        [*] --> Stats : is(/stats)
        Stats --> [*] : isNot(/stats)
        Stats --> Stats : is(/stats)
        

        [*] --> About : is(/about)
        About --> [*] : isNot(/about)
        About --> About : is(/about)
        

        [*] --> Github : is(github.com/citizenlabsgr)
        Github --> [*] : isNot(github.com/citizenlabsgr)
        Github --> Github : is(github.com/citizenlabsgr)
        

        [*] --> Slack : is(/slack.com)
        Slack --> [*] : isNot(/slack.com)
        Slack --> Slack : is(/slack.com)
```

# Community

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> CommunityGet
        CommunityGet --> CommunityGetHandler : (response[(dr_jurisdiction, count, lat, lon),...])
        CommunityGetHandler --> [*] : (communityList[(name, count, lat, lon),...])
     }    
         
    state Show {
             
        Title --> Subtitle
        Subtitle --> CommunityLinks
     }    
         
[*] --> [*] : isModalVisible=False
[*] --> Config : isModalVisible=True
Config --> Load : (title, subtitle)
Load --> Show : communityList
Show --> [*] : isModalVisible=false
 
Show --> Show : isModalVisible=true
CommunityLinks --> CommunityLinks : communityList
CommunityLinks --> CommunityLinks : moveMap
```

# About

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> AboutGet
        AboutGet --> AboutGetHandler : (response[(id, title, description),...])
        AboutGetHandler --> [*] : (aboutList[(id, title, description),...])
     }    
         
    state Show {
             
        Title --> Subtitle
        Subtitle --> Description
        Description --> AboutTitle
        AboutTitle --> About
     }    
         
[*] --> [*] : not(/about)
[*] --> Config : /about
Config --> Load : (title, subtitle, description, aboutTitle)
Load --> Show : aboutList
Show --> [*] : not(/about)
 
Show --> Show : /about
About --> About : aboutList

 
```
