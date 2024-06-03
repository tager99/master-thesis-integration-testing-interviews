# Protocol Expert Interview with #6

**Mi 13.03.2024**

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_
- Product owner for integration test
  - Test the product (Integrated SW) includes req. analysis, Test specification & Test execution
  - Check Technical feasibility of a requirement to be tested
  - Responsible for requirements being derived into test specification
  - Responsible for efficiency and quality of integration testing
- 1 ½ years as Product owner (Current Project)

## Test Object - What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**
- Software-Software Integration
- Focusing on all aspects (deployment, static, dynamic, resources)

What are dynamic aspects to be tested?
- Different software components are bundled together.
- Communication happens in a particular sequence and should be completed in a given interval of time &rarr; two aspects: sequence and timing

Which specific part of the architecture (your aspects) is most critical to test?
- Everything is equally important &rarr; if one aspect is missed it can equally impact the product adversely (Software on ADAS ECU)
- Dynamic is very crucial, next resources

Are sensor interfaces also part of integration testing?
- Not sensor HW interface, focus is on software interface of the ADAS ECU
  - All software components are integrated and communicate according to the software architecture
- Sensors are tested at system testing, and functional testing

**For each previously mentioned aspect like ... What is the goal of integration testing?**
- Verify that all of the software components are integrated and communicate with each other for CPU, Microcontroller
  - 3 bundles to Integrate: Platform stack (Basis software for Microcontroller, CPU), Black Box for ML, Application Software
- Verify that every application runs in a given sequence in a given cycle
- Resource utilization:
  - Runtime execution of each software component
  - RAM, ROM usage for each software component
  - Monitor percentage of each core usage for the given worst-case scenario

## Testing Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ...?**
- For static test:
  - Equivalence partition testing – based on architecture interface contains a list of variables/attributes with a given value range, default value, and some other tags
  - Inject values (in the range) &rarr; measure output and check according to range of the output &rarr; no violations of the defined ranges!
  - Inputs: positive (inside range + boundaries) & negative (injecting faults i.e. beyond boundaries value)
- AUTOSAR Classic – XCP for reading and injecting data, but not available for Adaptive

How to inject data?
- Vector CANoe - simulating/inject rest of vehicles &rarr; inject data from other ECUs
  - Also monitor IP-Interface
- Software Debugger from QNX – to inject and monitor data inside AUTOSAR Adaptive Node

**For which use cases do you use SW-Debugger?**
- Software Debugger from QNX – to inject and monitor data inside AUTOSAR Adaptive Node

What are the disadvantages of the SW-Debugger?
- Disturbs the normal running/flow of the Software, because it holds the Software (setting breakpoints) &rarr; breaks continuity

How can the Software-Debugger be used for dynamic testing?
- Set breakpoints according to the application sequence in the cycle

**For which use case do you use HW-Debugger?**
- For Classic in use
- Explore iSystem Debugger for Classic & adaptive together

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**
- They are executed on the target hardware
- But it is not mandatory to be on the target hardware according to ASPICE SWE 5
- Deployment &rarr; can be done in a simulation environment
- Static &rarr; can be done in a simulation environment
- Dynamic &rarr; better to do on the target hardware (performance, sequencing, timing)
- Resource &rarr; must be done on the hardware

What are the major difficulties or disadvantage of using a simulation environment?
- Currently there is no simulation for all stacks (CPU, Microcontroller) in one package

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**
- ASPICE,
- ISO26262
  - Prescribes which methods can be used

## Testing Issues - why not?

**Regarding your specific field of work, when is a test complete?**
- Over all releases – all SWE 2 (architecture) requirements in rhapsody are verified and traceable with test specification in internal testing tool for testing (Results uploaded)

**What kind of (coverage) criteria is used, in order to measure completeness?**
- Measurement criteria: requirements from SWE2 (architectural design) documented in rhapsody as architecture model
  - Each interface has a unique id in rhapsody
- For static: cover every interface by a test case
  - Link test case and requirement id
- Overview over number of requirements passed, failed, not executed
  - Not executed, since incremental testing for every release (only test new things or changes)

What procedures do you follow to obtain high coverage of test cases and how much time does it take?
- Create a bug ticket in Jira
  - Expected behavior
  - Observed behavior
  - Possible root cause (optional)
  - Detail of the environment
- Make sure that the failure was consistent through many tests
- Assign to defect manager
- Either fixed in the same release or in the next release
  - When it is going to be fixed in the next Release &rarr; Risk analysis is mandatory

**What are the most significant problems you face during testing (this might include technical challenges as well as resource limitations)**
- Resource Tests: you cannot guarantee that test specification is worst-case scenario due to the open challenge of creating a simulation of the external world that stress the function to max.
  - &rarr; try to stress a customer function as much as possible
  - Really depends on the outside input
  - How to maximize Load/ find specifications:
    - Turn on all features which can run at the same time
    - Creating a scene/scenario where features is overloaded
- Technical Issue/blocker – since moving from classic to adaptive
  - Development has moved but test techniques and tools are not mature enough (e.g XCP vs SW-Debugger)
  - No appropriate tool for testing AUTOSAR Adaptive
  - Development comes first, Testing comes second
- Without a good tool &rarr; needs huge amounts of resources, since a lot of the testing has to be done manually
- Testing is located at the very end of the overall project &rarr; in case of delays it is always the test team who has to compromise on the scope of testing or on the project being delayed

**What are possible approaches for the previously mentioned problems like ... ?**
- Maybe when change requests are handled very well and are well known, it could be enough to test just the changes (when there is just little time left for testing)

## Test automation and tools:

**Why is test automation important?**
- Accuracy – well documented, everything is scripted
  - Manual: even if the first person documents all the steps very well, it cannot be replicated by the next person
- Reliability/consistency:
  - Manual testing not really consistent (human errors)

**Which test steps are automated and how is test automation implemented?**
- Static:
  - Tool for rhapsody to csv
  - Generate test specification from csv
- Cannot create test script for CANoe and Debugger at the same time &rarr; test script creation is not automated
- Test script generation, and test execution is manual
  - Could be automated in theory but too much work &rarr; on hold &rarr; wait for tool

**Can you describe the tool chain for test execution and test automation?**
- Internal Test management tool
  - Document test case (specification, result)
  - Link requirement (id in rhapsody)
- Rhapsody – documents requirements/model
- SW-Debugger for Adaptive
- CANoe – RoV and IP communication
  - Creates report
- Can be uploaded to Internal Test management tool
- For Classic Closed Loop: Internal Test management tool, Rhapsody, CANoe

_What are the disadvantages or annoying things using the Tool ... ?_
- Synchronization issues between Internal Test management tool and Rhapsody

_What role do open-source tools play in the testing process?_
- No open-source tools in use