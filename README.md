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

# MyAdoptees
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(isModalVisible)
[*] --> Config : (isModalVisible)
AppState --> Load : currentUser
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (myAdopteeList))
Show --> [*] : not(isModalVisible)
 
Show --> Show : isModalVisible
 
```
  
# MyAdoptees *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> Adoptees
    Adoptees --> [*]
  }
 
*Show --> *Show : isModalVisible
Adoptees --> Adoptees : myAdopteeList[(pk, sk, tk, form(lat, lon, name, type, drain_id), owner, active, created, updated),...]
 
```
  
# MyAdoptees *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> AdopteeGetOwnerRequest : isModalVisible
    AppState --> AdopteeGetOwnerRequest : currentUser
    AdopteeGetOwnerRequest --> AdopteeGetOwnerHandler : (response[(pk, sk, tk, form(lat, lon, name, type, drain_id), owner, active, created, updated),...])
    AdopteeGetOwnerHandler --> [*] : myAdopteeList[(pk, sk, tk, form(lat, lon, name, type, drain_id), owner, active, created, updated),...]
  }
 
 
```

 
# About
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/about)
[*] --> Config : /about
Env --> Load : AAD_API_TOKEN
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
    [*] --> AboutGet : /about
    Env --> AboutGet : AAD_API_TOKEN
    AboutGet --> AboutGetHandler : (response[(id, title, description),...])
    AboutGetHandler --> [*] : (aboutList[(id, title, description),...])
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
 
*Show --> *Show : /about
About --> About : aboutList
 
```

# Adoption
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/home)
[*] --> Config : /home
Env --> Load : AAD_API_TOKEN,DW_AUTH_TOKEN,GOOGLE_MAPS_API_KEY
Config --> Load
Load --> Show : (datumDictionary(key(id, data (type, lat, lon, drain_id, name), key, toggle_state)))
Show --> [*] : not(/home)
 
Show --> Show : /home
 
```
  
# Adoption *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> LocationGetRequest
    LocationGetRequest --> LocationGetHandler : (response(coords(accuracy, altitude, heading, latitude, longitude, speed), timestamp))
    LocationGetHandler --> GoogleMapGetRequest : (location(lat, lng))
    GoogleMapGetRequest --> GoogelMapGetHandler : (response(mapObject))
    GoogelMapGetHandler --> LoadDrains : (mapObject)
    LoadDrains --> [*] : (datumDictionary(key(id, data (type, lat, lon, drain_id, name), key, toggle_state)))
  }
 
 
```
  
# Adoption *LoadDrain
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *LoadDrain
     {
    [*] --> AdopteeGetMBRRequest : (request(mbr(north, south, east, west)))
    AdopteeGetMBRRequest --> AdopteeGetMBRHandler : (response[(pk, sk, tk, form(lat, lon, name, type, drain_id), owner, active, created, updated),...])
    AdopteeGetMBRHandler --> DrainGetRequest : (datumDictionary(key(id, data (type, lat, lon, drain_id, name), key, toggle_state)))
    DrainGetRequest --> DrainGetHandler : (response(data [(dr_asset_id, dr_lat, dr_lon, etal),...], status, statusText))
    DrainGetHandler --> [*] : datumDictionary
  }
 
 
```
  
# Adoption *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Orphans
    Orphans --> Adoptees
    Adoptees --> YourAdoptees : authenticated
    Adoptees --> [*] : not(authenticated)
    YourAdoptees --> [*]
  }
 
*Show --> *Show : /home
YourAdoptees --> YourAdoptees : adopt
    YourAdoptees --> YourAdoptees : orphan
    YourAdoptees --> YourAdoptees : rename
 
```
  
# Adoption *YourAdoptees
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *YourAdoptees
     {
    [*] --> [*] : not(authenticated)
    [*] --> AdopteePostRequest : adopt
    [*] --> AdopteePutRequest : rename
    [*] --> AdopteeDeleteRequest : orphan
    AdopteePostRequest --> AdopteePostHandler
    AdopteePostHandler --> LoadMyAdoptees : Post Status
    AdopteePutRequest --> AdopteePutHandler
    AdopteePutHandler --> LoadMyAdoptees : Put Status
    AdopteeDeleteRequest --> AdopteeDeleteHandler
    AdopteeDeleteHandler --> LoadMyAdoptees : Delete Status
    LoadMyAdoptees --> [*] : status
  }
 
 
```

# Communities
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(isModalVisible)
[*] --> Config : isModalVisible
Env --> Load : AAD_API_TOKEN
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (communityList))
Show --> [*] : not(isModalVisible)
 
Show --> Show : abc
 
```
  
# Communities *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> CommunityGet : isModalVisible
    Env --> CommunityGet : AAD_API_TOKEN
    CommunityGet --> CommunityGetHandler : (response[(dr_jurisdiction, count, lat, lon),...])
    CommunityGetHandler --> [*] : (communityList[(name, count, lat, lon),...])
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
 
*Show --> *Show : isModalVisible
CommunityLinks --> CommunityLinks : communityList
    CommunityLinks --> CommunityLinks : moveMap
 
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


# Header
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> Config : /*
Config --> Show : (page(bannerImage, title, subtitle))
Show --> [*]
 
Show --> Show : /*
 
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
 
*Show --> *Show : /*
 
```

# Home
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/home)
[*] --> Show : /home
Show --> [*] : not(/home)
 
Show --> Show : /home
 
```
  
# Home *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Map
    Map --> [*]
  }
 
Map --> Map : map
    Map --> Map : adopt
    Map --> Map : orphan
    Map --> Map : name
 
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
SignOut --> SignOut : isModalVisible
 
```

# Opportunities
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/opportunities)
[*] --> Config : /opportunities
Env --> Load : AAD_API_TOKEN
Config --> Load : (page(title, subtitle, description, opportunityTitle))
Load --> Show : (page), (opportunityList)
Show --> [*] : not(/opportunities)
 
Show --> Show : /opportunities
 
```
  
# Opportunities *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> OpportunityGet : /opportunities
    Env --> OpportunityGet : AAD_API_TOKEN
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
 
*Show --> *Show : /opportunities
Opportunities --> Opportunities : opportunityList
 
```


# Signin
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(isModalVisible)
[*] --> [*] : (authenticated)
Env --> Authenticate : AAD_API_TOKEN
Config --> Show : (page(title, subtitle, feedback))
Show --> [*] : isModalVisible=false
Show --> Authenticate : (username, password)
[*] --> Config : not(authenticated)
Authenticate --> Show : not(authenticated)
Authenticate --> [*] : (authenticated)
 
Show --> Show : isModalVisible
    Show --> Show : not(authenticated)
 
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
 
*Show --> *Show : isModalVisible
    *Show --> *Show : not(authenticated)
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
    Env --> SignInRequest : AAD_API_TOKEN
    SignInRequest --> SignInHandler : response(msg, status, token)
    SignInHandler --> SetState : authenticationStatus
    SetState --> [*] : (authenticated)
    SetState --> [*] : not(authenticated)
  }
 
 
```

# SignOut
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : isModalVisible=false
[*] --> [*] : not(authenticated)
[*] --> Config : (authenticated)
Config --> Show : token
Show --> [*] : not(authenticated)
 
Show --> Show : authenticated
 
```

# Sponsor
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/sponsor)
[*] --> Config : /sponsor
Env --> Load : AAD_API_TOKEN
Config --> Load : (page(title, subtitle))
Load --> Show : (sponsorList[(id, title, description, website, source),...])
Show --> [*] : not(/sponsor)
 
Show --> Show : /sponsor
 
```
  
# Sponsor *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> SponsorGetRequest : /sponsor
    Env --> SponsorGetRequest : AAD_API_TOKEN
    SponsorGetRequest --> SponsorGetHandler : (response[(id, title, description),...])
    SponsorGetHandler --> [*] : (sponsorList[(id, title, description, website, source),...])
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
 
*Show --> *Show : /sponsor
Sponsors --> Sponsors : sponsorList
 
```

# Stats
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/stats)
[*] --> Config : /stats
Env --> Load : AAD_API_TOKEN
Config --> Load : (page(title, subtitle))
Load --> Show : ((page), (statsList))
Show --> [*] : not(/stats)
 
Show --> Show : /stats
 
```
  
# Stats *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> StatsGetRequest : /stats
    StatsGetRequest --> StatsGetHandler : (response[(id, title, description),...])
    StatsGetHandler --> [*] : (statsList[(id, title, description, count),...])
  }
 
 
```
  
# Stats *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> Title
    Title --> Subtitle
    Subtitle --> Statistics
    Statistics --> [*]
  }
 
*Show --> *Show : /stats
Statistics --> Statistics : statsList
 
```

# Tou
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
[*] --> [*] : not(/tou)
[*] --> Config : /tou
Env --> Load : AAD_API_TOKEN
Config --> Load
Load --> Show : ((communityList), (touList))
Show --> [*] : not(/tou)
 
Show --> Show : /tou
 
```
  
# Tou *Load
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Load
     {
    [*] --> CommunityGetRequest : /tou
    Env --> CommunityGetRequest : AAD_API_TOKEN
    Env --> TouGetRequest : AAD_API_TOKEN
    CommunityGetRequest --> CommunityGetHandler : (response[(dr_jurisdiction, count, lat, lon),...])
    CommunityGetHandler --> TouGetRequest : (communityList[(name, count, lat, lon),...])
    TouGetRequest --> TouGetHandler : (response[(active, created, form(i, p, w, doc_id), owner, pk, sk, tk, updated),...])
    TouGetHandler --> [*] : (touList[(id, paragraph),...])
  }
 
 
```
  
# Tou *Show
 
```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
 state *Show
     {
    [*] --> TouDocument
    TouDocument --> [*]
  }
 
*Show --> *Show : /tou
TouDocument --> TouDocument : touList
    TouDocument --> TouDocument : communityList
 
```

