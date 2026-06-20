# SAST
**Static Application Security Testing**

Analyzes sourcecode or binaries without executing the application to find vurlnibilities

SAST = "White-box" security testing 

Scans: Code, AST, Data Flow, Control Flow

Finds: SQLi, XSS, Path Traversal, 
=> Its a part of SDLC, its used to ensure that the code to be deployed with no bugs and no logical errors.

```
Deeloper ------------(code)---------->Tester------------->Deploy

IF error found 

Developer ---------------->Tester(failed)

     ^                      |
     |______________________|
(The power of left Shift)
Find and fix vurlnabalities before they reach production)
```
Software Testing Classifications: 
1. Testing Types:
   - Manual
   - Automated
2. Testing Methods:
   - Static
   - Dynamic
3. Testing Approach:
   - Black Box
   - White Box
   - Grey Box
4. Testing Levels:
   - Unit testing  [Where each module tested seprately]
   - Integration testing  [Set of modules]
   - System testing  [Whold system]
   - Acceptance testing  [To fullfill the requirments of client/customer]


# SAST vs MANUAL

#### SAST
PROS:- 

- Consistent & repeatable
- Scales to millions of LOC (Line of Code)
- Run on every commit
CONS:-

- can miss business logic flaws

#### Manual
PROS:- 

- Understand context & intent
- Finds complet logic bugs
  
CONS:-

-  Slow and expensive
-  Human fatigue and inconsistent (us bro us)


# SonarQube: 

Open source static code analysis tool Its used by developers to manage source code quality and consistency.
PORT :- 9000/TCP
Checks:- 

  - Bugs/vuln
  - Code Defects
  - Code Duplication
  - Excess Complexity
  - Code Smell (May genrate many false alarm)

#### It works with %)+ languages:
   - java
   - .net
   - js
   - py
   - c+=
   - php
   - etc ....

### SonarQube also works in CI/CD :-

 - To automate Code Analysis
 - Get access through webhooks & API
 - Integrate GitHub/Gitlab/bitbucket/local....
 - Analyse branch and pull request (PR)


# Install SonarQube on EC2 instance
-------------------------------------
Deploy sonarqube on docker:
```

docker run -d --name sonarqube-custom --restart unless-stopped -p 9000:9000 sonarqube:community

```
-- We are going to setup sonarqube community builts

**On EC2 instance**
```
sudo apt install docker
docker run -d --name sonarqube-custom --restart unless-stopped -p 9000:9000 sonarqube:community
```

STEPS:-
1. Create a project on sonarqube dashboard
     project display:- ditiss
   
     project key:- ditiss
   
     main branch name:- main
   
3. follows the instance defaults

4. Analysis Methods select **locally**


Default ID/PASS

ID:- admin

Pass:- admin

5. - genrate a token of your project
   - Run analysis on your project (ithe aaplya project chi language select kraychi aahe ani jr nahe paheje tr Common cli pick kraych)
          - in this pick Other(for Go, PHP, ...)
          - pick OS of developer machine
          - it give link go in that

6. On developer machine:-
   - copy the downoad link
   - make one new directory
   - then in that folder
   - wget Your_code_link
   - create a softlink of it
  
```
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-8.0.1.6346-linux-x64.zip
# unzip sonar-scanner-cli-8.0.1.6346-linux-x64.zip
# cd sonar-scanner-8.0.1.6346-linux-x64/bin/
# ln -s /root/sonar/sonar-scanner-8.0.1.6346-linux-x64/bin/sonar-scanner /bin/sonar-scanner

```


lkajd `#RRGGBB` jajh   `#RRGGBB`








 
