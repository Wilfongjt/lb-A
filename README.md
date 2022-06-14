# System
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
AAD --> API 
API --> Data
```

# Tou

```mermaid

```

# Stats

```mermaid

```

# Sponsors

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Show {
             
        [*] --> Title
        Title --> Subtitle
        Subtitle --> [*]
     }    
         
[*] --> [*] : not(/sponsers)
[*] --> Config : /sponsers
Config --> Show : (title, subtitle)
Show --> [*] : not(sponsors)
 
Show --> Show : /sponsers
```

# SignOut

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Show {
             
        [*] --> LogOut : token
        LogOut --> [*] : not(authenticated(token))
     }    
         
[*] --> [*] : isModalVisible=false
[*] --> [*] : not(authenticated(token))
[*] --> Config : authenticated(token)
Config --> Show : token
Show --> [*] : not(authenticated(token))
 
Show --> Show : authenticated(token)

```

# SignIn

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Show {
             
        Title --> Subtitle
        Subtitle --> Username
        Username --> Password
        --
        Feedback
     }    
         
    state Authenticate {
             
        [*] --> SignInRequest : (username),(password)
        SignInRequest --> SignInHandler : token
        SignInHandler --> [*]
     }    
         
[*] --> [*] : isModalVisible=false
[*] --> [*] : authenticated(token)
Config --> Show : (page(title, subtitle, feedback))
Show --> [*] : isModalVisible=false
Show --> Authenticate : (username, password)
[*] --> Config : not(authenticated(token))
Authenticate --> Show : not(authenticated(token)), feedback
Authenticate --> [*] : authenticated(token)
 
Show --> Show : isModalVisible=true
Show --> Show : not(authenticated(token))
Username --> Username : not(username)
Password --> Password : not(password)

```

# Header

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Show {
             
        BannerImage --> Title
        Title --> Subtitle
     }    
         
[*] --> Config : /*
Config --> Show : (page(bannerImage, title, subtitle))
 
```

# Opportunities

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> OpportunityGet
        OpportunityGet --> OpportunityGetHandler : (response[(id, title, description),...])
        OpportunityGetHandler --> [*] : (opportunityList[(id, title, description),...])
     }    
         
    state Show {
             
        Title --> Subtitle
        Subtitle --> Description
        Description --> OpportunityTitle
        OpportunityTitle --> Opportunities
     }    
         
[*] --> [*] : not(/opportunities)
[*] --> Config : /opportunities
Config --> Load : (page(title, subtitle, description, opportunityTitle))
Load --> Show : (page), (opportunityList)
Show --> [*] : not(/opportunities)
 
Show --> Show : /opportunities
Opportunities --> Opportunities : opportunityList
```

# Nav

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

        [*] --> Adoptions : is(/)
        Adoptions --> [*] : not(/)
        Adoptions --> Adoptions : is(/)
        

        [*] --> MyAdoptees : is(isModalVisible)
        MyAdoptees --> [*] : not(isModalVisible)
        MyAdoptees --> MyAdoptees : is(isModalVisible)
        

        [*] --> Communities : is(isModalVisible)
        Communities --> [*] : not(isModalVisible)
        Communities --> Communities : is(isModalVisible)
        

        [*] --> Signin : is(isModalVisible)
        Signin --> [*] : not(isModalVisible)
        Signin --> Signin : is(isModalVisible)
        

        [*] --> Signup : is(/adopter)
        Signup --> [*] : not(/adopter)
        Signup --> Signup : is(/adopter)
```

# Footer

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

        [*] --> TOU : is(/tou)
        TOU --> [*] : not(/tou)
        TOU --> TOU : is(/tou)
        

        [*] --> Opportunities : is(/opportunities)
        Opportunities --> [*] : not(/opportunities)
        Opportunities --> Opportunities : is(/opportunities)
        

        [*] --> Sponsors : is(/sponsors)
        Sponsors --> [*] : not(/sponsors)
        Sponsors --> Sponsors : is(/sponsors)
        

        [*] --> Stats : is(/stats)
        Stats --> [*] : not(/stats)
        Stats --> Stats : is(/stats)
        

        [*] --> About : is(/about)
        About --> [*] : not(/about)
        About --> About : is(/about)
        

        [*] --> Github : is(github.com/citizenlabsgr)
        Github --> [*] : not(github.com/citizenlabsgr)
        Github --> Github : is(github.com/citizenlabsgr)
        

        [*] --> Slack : is(/slack.com)
        Slack --> [*] : not(/slack.com)
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
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (communityList))
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
Config --> Load : (page(title, subtitle, description, aboutTitle))
Load --> Show : ((page), (aboutList))
Show --> [*] : not(/about)
 
Show --> Show : /about
About --> About : aboutList 
```
