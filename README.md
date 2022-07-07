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

# Sponsor
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/sponsor)
[*] --> Load : /sponsor
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (sponsorList))
Show --> [*] : not(/sponsor)
Mem --> Config 
Show --> Show : /sponsor
 
```
  
# Sponsor *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> SponsorGetRequest
    SponsorGetRequest --> SponsorGetHandler : (response[(id, title, description),...])
    SponsorGetHandler --> [*] : (output(sponsorList[(id, title, description, website, source),...]))
  }
 
 
```
  
# Sponsor *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> Sponsors
    Sponsors --> [*]
  }
 
Sponsors --> Sponsors : sponsorList
 
```
  
# Sponsor *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> SponsorGetRequest
    SponsorGetRequest --> SponsorGetHandler : (response[(id, title, description),...])
    SponsorGetHandler --> [*] : (output(sponsorList[(id, title, description, website, source),...]))
  }
 
 
```
 
# SignOut
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : isModalVisible=false
[*] --> [*] : not(authenticated(token))
[*] --> Config : authenticated(token)
Config --> Show : token
Show --> [*] : not(authenticated(token))
 
Show --> Show : authenticated(token)
 
```


# Signin
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%

stateDiagram
 
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
 
```
  
# Signin *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title : (page(title, subtitle, feedback))
    Title --> Subtitle
    Subtitle --> Username
    Username --> Password
    Password --> Feedback
    Feedback --> [*]
  }
 
Username --> Username : not(username)
Password --> Password : not(password)
 
```
  
# Signin *Authenticate
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Authenticate
     {
    [*] --> SignInRequest : (username),(password)
    SignInRequest --> SignInHandler : response(msg, status, token)
    SignInHandler --> [*] : token
  }
 
 
```

# Header
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> Config : /*
Config --> Show : (page(bannerImage, title, subtitle))
Show --> [*]
 
 
```
  
# Header *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> BannerImage : (page(bannerImage, title, subtitle))
    BannerImage --> Title
    Title --> Subtitle
    Subtitle --> [*]
  }
 
 
```

# Opportunities *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> OpportunityGet
    OpportunityGet --> OpportunityGetHandler : (response[(id, title, description),...])
    OpportunityGetHandler --> [*] : (opportunityList[(id, title, description),...])
  }
 
 
```
  
# Opportunities *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> Description
    Description --> OpportunityTitle
    OpportunityTitle --> Opportunities
    Opportunities --> [*]
  }
 
Opportunities --> Opportunities : opportunityList
 
```

# Nav
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> Adoptions : /*
Adoptions --> Communities
Communities --> Signup : not(authenticated)
Communities --> MyAdoptees : authenticated
Signup --> Signin
Signin --> [*] : not(authenticated)
MyAdoptees --> SignOut
SignOut --> [*]
 
Adoptions --> Adoptions : /
Communities --> Communities : isModalVisible
Signup --> Signup : /adopter
Signin --> Signin : isModalVisible
MyAdoptees --> MyAdoptees : isModalVisible
 
```


# Footer
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> TOU : /*
TOU --> Opportunities
Opportunities --> Sponsor
Sponsor --> Stats
Stats --> About
About --> Github
Github --> Slack : github.com/citizenlabsgr
Slack --> [*] : /slack.com
 
TOU --> TOU : /tou
Opportunities --> Opportunities : /opportunities
Sponsor --> Sponsor : /sponsor
Stats --> Stats : /stats
About --> About : /about
 
```

# Communities
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : isModalVisible=False
[*] --> Config : isModalVisible=True
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (communityList))
Show --> [*] : isModalVisible=false
 
Show --> Show : isModalVisible=true
 
```
  
# Communities *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> CommunityGet
    CommunityGet --> CommunityGetHandler : (response[(dr_jurisdiction, count, lat, lon),...])
    CommunityGetHandler --> [*] : (output(communityList[(name, count, lat, lon),...]))
  }
 
 
```
  
# Communities *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> CommunityLinks
    CommunityLinks --> [*]
  }
 
CommunityLinks --> CommunityLinks : communityList
    CommunityLinks --> CommunityLinks : moveMap
 
```

# About
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/about)
[*] --> Config : /about
Config --> Load : (page(title, subtitle, description, aboutTitle))
Load --> Show : ((page), (aboutList))
Show --> [*] : not(/about)
 
Show --> Show : /about
 
```
  
# About *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> AboutGet
    AboutGet --> AboutGetHandler : (response[(id, title, description),...])
    AboutGetHandler --> [*] : (output(aboutList[(id, title, description),...]))
  }
 
 
```
  
# About *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> Description
    Description --> AboutTitle
    AboutTitle --> About
    About --> [*]
  }
 
About --> About : aboutList
 
```

