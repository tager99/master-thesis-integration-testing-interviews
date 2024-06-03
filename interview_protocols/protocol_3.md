# Protocol Expert Interview with #3 (2 experts)

**Di 05.03.2024**

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in (integration) testing**_

_Person 1:_
- Test manager of BSW ADAS ECU current GEN &rarr; SWE 4,5,6
- 12 years of experience at OEM
- 2 years of experience as test manager

_Person 2:_
- Integration Testing SWE 5
  - Main working activity: How to qualify platform software regarding SWE 5 & ISO 26262
- Before OEM: AUTOSAR Adaptive Developer @ supplier

## Test Object - What?

**How does the Basic Software (BSW) look like and what has to be tested in the context of BSW-Testing?**

_Person 2:_
- Provide Functionalities that are then used by the applications
- Mainly based on AUTOSAR Classic, AUTOSAR Adaptive, internal libraries to deliver functionalities/services that are on top of AUTOSAR
- Since we have 2 OS &rarr; communication between targets running these two systems
  - One is Adaptive AUTOSAR, and the other is Classic AUTOSAR; both are running on top of a hypervisor.
  - The reason for having two OS is to provide more safety and a fallback solution if something goes wrong, all ADAS functionalities are executed AUTOSAR Adaptive, while the AUTOSAR classic acts as a safety backup in case something goes wrong and to monitor sensor functionalities, generally speaking classic AUTOSAR is more stable/ Realtime than adaptive AUTOSAR that is why it is used as a safety backup, however adaptive AUTOSAR is able to provide more complex capabilities needed for ADAS functionalities
  - How to integrate?
  - How to test the communication at the main point of integration

- What has to be integrated/tested:
  - AUTOSAR Classic Functionalities,
  - AUTOSAR Adaptive Functionalities
  - Communication between BSW & ASW
  - Libraries which deliver functionalities/services

_Person 1:_
- BSW is the first layer after the hardware &rarr; features which is helpful for the ASW
- 5 to 6 main features
  - Startup shutdown
  - Diagnostics
  - State and error management
  - Platform health monitoring
  - Security features

Which parts are developed by OEM and which parts are developed by suppliers?
- Compliant Activity with several supplier and partners
- Classic AUTOSAR parts & communication parts mainly by supplier
- Some features 100% OEM like state and error management, platform health monitoring
- Realtime environment supplier for ADAS Capabilities
- Supplier for HW of the ECU, they also do the initial setup and configuration of the ECU to be later used by the workstream
- &rarr; 30 to 40% OEM based

How is testing BSW and Testing ASW connected? How are they influencing each other?
- In the past BSW was handled as a standalone product
- Now: due to the complexity, standalone testing is not possible:
  - E.g. state and error management: a lot of interactions with other stacks (not BSW)
  - Main focus: how are the basic software functionalities behave

- Interactions with ASW testing &rarr; where are the limits (when does BSW testing ends, and ASW testing start)

**When we focus on integration-testing of the BSW according to SWE 5, what are we testing?**
- Adaptive stack, Libraries, Black -Box for ML - messages
- Classic - messages
- between CPU and Microcontroller
- &rarr; check first message is there, second check message content, check message timing
- Performance test (CPU, RAM, code execution time (metric) for the BSW mainly, but also in collaboration with ASW (Budget for ASW & BSW together)

[if multiple] Which specific part of the architecture (your aspects) is most critical to test?
- Flashing is working
- system is up and running
- startup time
- very basic communication is up
- very Basic diagnostics

[if multiple] How can the different aspects be prioritized?
- &rarr; add gradually more functionalities (add more diagnostics, more communication, more system handling (shutdown, hard reset, soft reset)
- Most secured, most protected functionalities coming at last

**In terms of your field/your work, what is the goal of testing?**
- Main goal: there are some basics services (determined by release manager) available so that application teams can work/develop on this platform
  - Basic diagnostics
  - Basic communication
  - Secure communication
  - &rarr; not the entire set from the beginning
  - &rarr; gradually increase features/services

## Testing Methods - How?

**Which test methods (SWE5) are used at the moment to test the basic software functionalities?**
- Severing testing methods listed in ISO 26262 & based on ASIL Level
- Most important:
  - Interfaces are running fine, and all components are communicating according to architecture/ requirements
  - Fault injections
  - Cyclic redundancy check (CRC)
  - Check-sum checks
  - &rarr; mainly white box

Does the test object need to be changed in order to apply the test methods, and if so, what needs to be changed?
- Sometimes change the object BSW is interacting with (Mock or Stub)
- Test isolated component of BSW
- Usage of debugger &rarr; impacts running time
- Whenever a technique will impact the software &rarr; approval required &rarr; make sure it is not ending up in series production (developing branch) &rarr; disclaimer set of test cases where run on a modified software

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**
- Most common on target ECU (target environment) itself
- For integrating adaptive on CPU (checking POSIX) – QEMU on Linux
  - For emulating QNX on Linux machine

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**
- ISO 26262
- ASPICE
- ISO 29119 Software Testing
- internal standard
  - Technical aspects
  - And not technical aspects (how testing is done)

- Security standards 21434 – road vehicles cybersecurity engineering – currently not implemented by OEM (done by extern)
- &rarr; all standards must be met!

## Issues - why not?

**Regarding your specific field of work, when is a test complete?**

**What kind of (coverage) criteria is used, in order to measure completeness?**
- Number of architectural requirements
- Number of architecture elements (interfaces)
- Golden rules like: At least one architecture element/ interface covered by at least one test case
- Use cases are defined (because architecture elements not in good shape/ in progress)
  - For each use case: integration testing team is creating test cases

What procedures do you follow to obtain high coverage of test cases and how much time does it take?
- At the beginning, freeze of architecture element and software &rarr; dedicated time for testing, reviews, traceability
- If coverage not met &rarr; justification, have to be approved by test manager, release manager, product owners &rarr; risk assessment meeting

What happens in case of failed tests?
- JIRA or internal tool for testing defects → shared with defect manager and feature owner &rarr; fixed version (before next release for critical parts)
- Risk assessment of defects

**What are the most significant challenges/problems you face during testing (this might include technical challenges as well as resource limitations)**
- Get proper input &rarr; architecture team is first defining major qualifications requirements (SWE 1), later define more specific architecture elements into the project &rarr; deal with incomplete or moving input
- &rarr; what are the priorities at the beginning
- Changes in architecture with each release
  - Cannot perform full regression test
  - &rarr; impacts in timing, quality and traceability

- Testing starts delayed (in comparison to project start); general thing not only OEM

What are the main reason for later changes in the architecture?
- Misinterpretations of requirements on supplier site
- From a feature perspective: each feature is realized according to its requirements, but communication mismatches, or something is missing

**What are possible approaches for the previously mentioned problems like late changes in architecture/ moving input?**
- Revisit the process to prevent feature team or architecture team doing late changes
- Way to measure that: architecture bug (something is missing, incompatible)
- Ideal word: do everything right from the beginning including in compliance with all the standards

## Tools and automation - with what?

**Which role does test automation play for testing BSW and which tools are used in the context of test automation?**
- Gitlab & Jenkins pipeline
- On that pipeline python and CANoe for execution
- V-Test-Studio IDE for writing testcases for CANoe environment
- Static analysis tools (more on component level than on integration level) like Coverity

Which steps are automated?
- Test case specification
- Teas case creation
- Test case execution
- Test report

**Which tools are used to document the requirements of the test object to be tested?**
- Doors Next Generation (DNG)
  - Linking of requirements and how many test cases has to be executed is done manually

- Rhapsody (defines use cases & architecture)
  - Main disadvantage: linking/connection/traceability to DNG or internal testing tool (based on intermediate script), not easy to use because of high complexity &rarr; makes alignment with different teams difficult
  - For matching of Rhapsody and internal testing tool, person 1 already did some basic investigation on a tool but no deep investigation to match rhapsody model; but probably needs a lot of configuration

**Which tools do you use in the context of the above-mentioned test methods or for test case execution?**
- Testframework (internal)
- CANoe based Testing for test execution itself
- vTESTstudio for test execution itself
- For automation - Jenkins and Gitlab pipelines, and also python and CANoe
- internal testing tool
  - Test specification documented in internal testing tool
  - Test case creation and test case execution
  - Generate report
  - not easy to use because of high complexity &rarr; makes alignment with different teams difficult

How to inject data?:
- Depends on the OS
- POSIX:
  - Shell
  - Test application

- RTOS non POSIX (runs on Microcontroller):
  - Debugger

- (only) Classic AUTOSAR – XCP – but depends on configuration (is variable writable)
  - Mainly measurement