# SignIn

```mermaid

%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

 
[*] --> [*] : isModalVisible=false
[*] --> Config : isModalVisible=true
Config --> Load : (name,page,remote,isModalVisible)
Load --> Show : communityList
Show --> Show : MoveMap
Show --> Show : isModalVisible=true
Show --> [*] : isModalVisible=false
 
```

# SignIn

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

    
   
    [*] --> [*] : isModalVisible=false
    [*] --> Config : isModalVisible=true
    Config --> Show : signin=(title,subtitle,feedback)
    Show --> [*] : isModalVisible=false
 
    Show --> Authenticate : (nm, pw)
    Authenticate --> Show : fail
    Authenticate --> [*] : authenticated
```

# SignIn

```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 
    state Show {
      SmallHeader --> Collect
      Collect
    }
    state Collect  {
        
        Username --> Password
        Password --> [*]
    }
    state Authenticate {
      [*] --> authenticateGetRequest
      authenticateGetRequest --> authencateGetHandler
      authencateGetHandler --> [*]
    }
 
    [*] --> [*] : isModalVisible=False
    [*] --> Config : isModalVisible=True
    
    Config --> Show : signin=(title,subtitle,feedback)
    
    Show --> [*] : isModalVisible=False
    Authenticate --> [*] : authenticated
    Authenticate --> Collect : failed
    Collect --> Authenticate : (un, pw)
    
    
 


```

# Header 
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

    state Show  {
        BannerImage --> Title
        Title --> Subtitle
    }
 
 
    [*] --> Config : route=*
    Config --> Show : page=(bannerImage,title,subtitle)
    Show --> [*]
 
 
```
# About
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

    state Load  {
        [*] --> AboutGet
        AboutGet --> AboutGetHandler : remote=[(id,title,description),...]
        AboutGetHandler --> [*] : aboutList
    }
    state Show  {
        Title --> Subtitle
        Subtitle --> AboutList
    }
 
 
    [*] --> [*] : not(route=about)
    [*] --> Config : route=/about
    Config --> Load : page=(title,subtitle)
    Load --> Show : page+aboutList
    Show --> [*] : not(route=about)
 
AboutList --> AboutList : aboutList
 
```

# Community
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

    state Load  {
        [*] --> CommunityGet
        CommunityGet --> CommunityGetHandler : remote=[(name,count,lat,lon),...]
        CommunityGetHandler --> [*] : communityList
    }
    state Show  {
        Title --> Subtitle
        Subtitle --> Communities
    }
 
 
    [*] --> [*] : isModalVisible=False
    [*] --> Config : isModalVisible=True
    Config --> Load : page=(title,subtitle)
    Load --> Show : page+communityList
    Show --> [*] : isModalVisible=false
 
Show --> Show : isModalVisible=true
Communities --> Communities : communityList
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

# Opportunity
```mermaid
%%{init: {'securityLevel': 'loose', 'theme':'base'}}%%
stateDiagram
 

    state Load  {
        [*] --> OpportunityGet
        OpportunityGet --> OpportunityGetHandler : remote=[(id,title,description),...]
        OpportunityGetHandler --> [*] : oppList
    }
    state Show  {
        Title --> Subtitle
        Subtitle --> Description
        Description --> OpportunityTitle
        OpportunityTitle --> Opportunities
    }
 
 
    [*] --> [*] : not(route=opportunities)
    [*] --> Config : route=opportunities
    Config --> Load : page=(title,subtitle,description,oppTitle)
    Load --> Show : page+oppList
    Show --> [*] : not(route=opportunities)
 
Show --> Show : route=opportunities
Opportunities --> Opportunities : oppList

```
