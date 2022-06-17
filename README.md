# System
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram

App --> API
API --> Service

AAD --> AADApi 
AADApi --> Data

AAD --> DataWorldApi 
DataWorldApi --> Drains

AAD --> GoogleMaps
GoogleMaps --> Map


```

# Adoption

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> LocationGetRequest
        LocationGetRequest --> LocationGetHandler
        LocationGetHandler --> GoogleMapGetRequest
        GoogleMapGetRequest --> GoogelMapGetHandler
        GoogelMapGetHandler --> [*]
     }    
         
    state Show {
             
        [*] --> Map
        Map --> [*]
     }    
         
    state Adopt {
             
        [*] --> AdopteePostRequest : post
        AdopteePostRequest --> AdopteePostHandler
        AdopteePostHandler --> LoadMyAdoptees
        LoadMyAdoptees --> AdopteePutRequest
        AdopteePutRequest --> AdopteePutHandler
        AdopteePutHandler --> [*]
     }    
         
[*] --> [*] : not(/home)
[*] --> Config : /home
Config --> Load
Load --> Show : xxx
Show --> [*] : not(/home)
Show --> Adopt : on(adopt)
Adopt --> Show : status(pass,fail)
 
Show --> Show : /home
Map --> Map : adopt
Map --> Map : orphan
Map --> Map : rename


```

# Home
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Show {
             
        Adoption
     }    
         
[*] --> [*] : not(/home)
[*] --> Show : /home
Show --> [*] : not(/home)
 
Show --> Show : /home
Adoption --> Adoption : map
```

# Tou

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> CommunityGetRequest
        CommunityGetRequest --> CommunityGetHandler : (response[(dr_jurisdiction, count, lat, lon),...])
        CommunityGetHandler --> TouGetRequest : (communityList[(name, count, lat, lon),...])
        TouGetRequest --> TouGetHandler : (response[(active, created, form(i, p, w, doc_id), owner, pk, sk, tk, updated),...])
        TouGetHandler --> [*] : (touList[(id, paragraph),...])
     }    
         
    state Show {
             
        [*] --> TouDocument
        TouDocument --> [*]
     }    
         
[*] --> [*] : not(/tou)
[*] --> Config : /tou
Config --> Load
Load --> Show : ((communityList), (touList))
Show --> [*] : not(/tou)
 
Show --> Show : /tou
TouDocument --> TouDocument : touList
TouDocument --> TouDocument : communityList

```

# Stats

```mermaid

```

# Sponsors

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
    state Load {
             
        [*] --> SponsorGet
        SponsorGet --> SponsorGetHandler : (response[(id, title, description),...])
        SponsorGetHandler --> [*] : (sponsorList[(id, title, description, website, source),...])
     }    
         
    state Show {
             
        [*] --> Title
        Title --> Subtitle
        Subtitle --> [*]
     }    
         
[*] --> [*] : not(/sponsor)
[*] --> Config : /sponsor
Config --> Load : (title, subtitle)
Load --> Show : ((page), (sponsorList))
Show --> [*] : not(/sponsor)
 
Show --> Show : /sponsor
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
