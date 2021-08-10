# 12 Factor Principles
## Monolithic application
- Deployed as a whole
- Application runs as one single process
- Modular boundaries are internal and can crossed to caused issues

### Pros
 - Less moving parts: easier to design, deploy
 - Less moving parts: less surface area to attack
 - Low operational complexity
 - Easy to debug
 - Easy to manage transaction and data sharing.
 
### Cons/ challanges
 - Large code base, makes it complex for developers.
 - Difficult to scale out
 - Larger impacted surface
 - modernization is complicated

## Micro services
### How MS solves the challanges
 - Fast deployment
 - Independent testing
 - Scale out
 - Lesser impacted surface
 - Any service can be rewritten independently

## but what exactly is MS
- Making multiple repos is not MS, deploying them separately is MS
- It is deployment concept, how you deploy across environment and change foot print
- It is about faster, independent and auto deployment

## Features of MS
- Split into smaller processes which are Container ready
- Cloud ready
- Fast developmet - multiple teams can work in parallel
- Auto deployment

## How 12F principles help to organise and maintain MS
- Principles are recommendations
- Not a silver bullet
- Should be applied as per requirement

## The 12F principles

   ### 1. Codebase
   - Single code base for application. 
   - Code is deployed to different environment from same code base.
   - Version controlling - git, svn
   
   ### 2. Dependencies
   - Explicitely declare and isolate dependencies
   - Library dependency are externalised
   - Application version to be referred from parent
   - Place jar in central repository
   - Use storage repository like JFrog, Nexus for storing libraries
   - Embed server in the artifact
   
   ### 3. Config
   - In monolith we put configuration in application.properties files and it is part of code, and change in config will require rebuild
   - Database connection, creadentials which are env specific and changing should not be part of code
   - All the configuration to be exetrnalise
	   - Make configs avaiable by using Config server.
	   - Store config in environment variables or start script
	   
   ### 4. Backing services
   - Apart from core code any other service used in application is backing service
   - Backing services should be treated as attached resources
   - Plug and play
   - Database, Cache, Message queue
   
   ### 5. Build, release, run
   - Seprate build and run stage
   - CI pipeline for build
   - CD pipeline for deployment
   - Automate build, release and deployment
   
   ### 6. Process
   - Execute app as single and stateless application
   - Two instances of application should be independent and should not store state in them
   - Share data with other applications with endpoint.
   - Store state data in Cache, Queue, DB
   
   ### 7. Port binding
   - Export services via port binding
   - Dont depend on physical servers
   - Instead use embedded server
   - Access services through embedded server
   - Application acts as standalone
   
   ### 8. Concurrency
   - Scale out
   
   ### 9. Disposibility
   - Startup and shutdown should be gracefull
   - Quick start and shutdown
   - Resilence incase of failure
   - Portability, scaling and maintainability
   
   ### 10. Dev/ Prod parity
   - Multiple environment should be similar as much as possible
   - Same version of OS, softwares should be installed on Dev/ QA/ Prod
   - Deploy on conatiner to achieve parity
   
   ### 11. Logs
   - Logs should be treated as event stream
   - Can be redirected to storage system like ELK, Splunk
   - Collect logs from multiple instance of application at same place and visualise on dashboard
   
   ### 12. Admin processes
- Any that is part of admin activity like spinning new server, upgarding DB server should be isolated
- Applications should be effected due to these admin activities

## MS design patterns
### Scaling
 - Vertical slicing
 - Separate DB for all MS

### Communication betweeen MS
 - Synchronous :- REST, json/http 
 - Async:- Event/ message queue 
 *It increase chatty communication between MS.*

## Recommendations
### Api Gateway
- Facade pattern to hide the implementation of service. Consumers are not impacted due to change in MS.
### Service discovery
Eureka
### Container readiness
- Container readiness/ Cloud ready
### Scaling
- Horizental / vertical scaling
### Statelessness
- Stateless application for fast scale up/down - Auto scale.
