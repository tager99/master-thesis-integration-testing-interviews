# Protocol Expert Interview with #4

**Do 07.03.2024**

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_
- Software preparation and integration testing at the current job 2.5 years and 8 years in total in integration

## Test Object - What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**
- Job is creating/integrating the software = taking change requests/bug fixes and creating/integrating the software
- Checking the deployment
  - Deployment report shows how many parts of an architecture are deployed, verifies that everything was integrated according to the architecture
  - Deployment report shows software components
  - 100% coverage not possible due to naming mismatches
    - Architecture &rarr; Deployment and Deployment &rarr; Architecture differ from each other
      - Different variants in deployment not being in the architecture and vice versa

**In the context of deployment testing what is the goal of testing?**
- Software for start of production, need high percentage in deployment testing &rarr; 100%
- Deployment has to be verified
  - Difference testing (passed or fail) and verification (has to pass)

## Testing Methods – How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**
- Test script based on Log output
- Diagnostic development takes time and has low priority to be reliable (makes us highly dependent on logs)
- Test: Init, Run, Terminate component and create logs in the debug method
  - Each module prints their state (initialize, start, running, ...)
    - Log level "debug" required
  - Running module is captured from the log
  - Module list is provided by a dump from Rhapsody
    - E.g., X number of internal modules
    - Run the software and get a list of modules
    - Excel sheet enables comparison Architecture &rarr; Deployment
- Deployment check: compares left side to right side of deployment list.
  - If something exists on the right and not on the left, the test fails

What part of the system creates the log?
- The execution manager checks if module is running or terminated etc.

Does the test object need to be changed in order to apply the test methods, and if so, what needs to be changed?
- No, only change log level
- Testing on development version of ECU since all logs are disabled on prod version

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**
- Always on the target environment &rarr; target ECU
- Testing on development version of ECU since all logs are disabled on prod version

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**
- Important for integration testing: ISO26262 is the most important foundation (especially part 6)
- Also Important: ASPICE (verify the architectural element) &rarr; different from traditional testing requirements, architectural design specifies state transition in the architecture and the interaction between the components. This is done by verifying the interfaces, i.e., if the communication works as expected (signal goes the right "paths")
  - Software component is the focus
  - Unit test verifies the unit, software unit design is tested
  - Here: architectural design is tested through the software components
  - They use ASPICE 3.1 not 4.x
  - It needs to be checked that the Unit is existing
  - To be checked = are the units part of the component as expected
- Security Norm
  - Defines that as a 3rd person, you should not be able to see what modules are running &rarr; then you would know what can be hacked
    - Additional guideline to be followed
  - Is it enough to set the log level to normal to be safe?
    - No, the log level can be changed during runtime as well to debug which would be a security violation

## Testing Issues - why not?

**Regarding your specific field of work, when is a test complete?**
- Verify that all the components and containers of the architecture are deployed

**What kind of (coverage) criteria is used, in order to measure completeness?**
- Number of components/containers deployed divided by number of components/containers listed in the architecture
- Number components/containers listed in the architecture divided by Number of components/containers deployed

**What are the most significant barriers/problems you face during testing (this might include technical challenges as well as resource limitations)**
- Architecture and way of implementation &rarr; few modules are very huge, you cannot just do a big bang integration, you need to slowly, incrementally integrate and improve
  - This incremental approaches is not often times used
  - New big changes will break the software in 99% cases
  - Biggest challenge: do an incremental approach instead of big bang
- At the end: you cannot test on the log level, because it is a non-realtime method
- Log output is not 100% certain
  - You need code reviews that also take a lot of time

**What are possible approaches for the previously mentioned problems like ... ?**
- Change from waterfall to agile &rarr; When an architectural element is created, challenges of integration can be considered better in an agile process
- Not using the log level would be desirable HOWEVER there is no tooling for adaptive available to do that and you still need to rely on the logs
- VECTOR also does not provide anything here

How do the classic AUTOSAR tools work for deployment testing
- LAUTERBACH is used for that, you can use a script to check the states
- In CLASSIC, you can work on memory/registers, in Adaptive, you cannot work on memory/registers

## Tools & automation - with what?

_Does Test automation play an important role in your case? If yes, why?_
- Test automation is the only method that gives you verification (= passed test), with manual testing not possible

_Which test steps are automated?_
- Yes, they are automated
- If changes are pushed that lead to failed tests, the pull request won’t be able to be merged &rarr; fully automated CI/CD

**Can you describe the tool chain, from the definition of the requirements to be checked to test execution and test automation?**
- Test automation: Python/Shell used for the pipeline programming
- General: QNX/ Linux
- CI/CD Pipeline
  - Gitlab, Jenkins, docker, jfrog artifactory
  - Static analysis tools: astree, Coverity, mxam
  - Testing TPT

_Do you work with Rhapsody?_
- Not really, only to fetch the excel sheet (list of components/containers)
- For interface testing Rhapsody is used but not for deployment

_What are disadvantages or annoying things of the tools in use?_
- End target is QNX, which is NOT a famous OS with good tool support
  - E.g., no CanOE support on QNX
  - On the other hand: it is a realtime OS
- Overall problem: tool support is very bad for AUTOSAR adaptive