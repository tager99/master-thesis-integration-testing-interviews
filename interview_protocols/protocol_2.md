# Protocol expert interview with #2

**Mi 28.02.2024**

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_
- Part of SWE 5 for ADAS ECU
- ASW (Application Software) Integration testing
- Testing of specific package/feature
  - Test case generation, test case execution, reporting
- 1 year for ADAS ECU
- Before also for ADAS ECU
- Integration testing for 2 years

## Test Object - What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**
- Communication Testing / Signal flow from one software component to other software components
  - All the interfaces of all the components
  - Test the whole architecture proposal
- Components from:
  - AUTOSAR Classic &rarr; Microcontroller
  - AUTOSAR Adaptive &rarr; CPU
  - Black Box for ML by supplier
  - RoV (Rest of Vehicle)

Which specific part of the architecture (your aspects) is most critical to test?
- Adaptive &harr; Adaptive (interprocess)
- Adaptive &harr; Black Box for ML
- Adaptive &harr; RoV
- Black Box for ML &harr; RoV

How can the different aspects be prioritized?
- Not so many components for AUTOSAR Classic
- &rarr; major focus on Adaptive

**For each previously mentioned aspect like ... What is the goal of testing?**
- Check all the interfaces (for one/all features)
- Test all features of a given Release

## Testing Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**
- Adaptive
  - Interface testing using SW Debugger
    - Set breakpoints
    - Read and insert data
  - Exploring other options such as the internal test framework
  - XCP not available
- Classic
  - XCP Stack for global variables
- Verify requirements
- Smoke Test
  - Device farm Test
  - Minimal Checks (version checks, vlan working, api working, applications are booted up)

**I know from #1 that Hardware and Software Debuggers are used for testing? For which use case do you use HW-Debugger? For which use cases do you use SW-Debugger?**
- HW-Debugger not used for testing, only for flashing the Microcontroller
- SW-Debugger for testing Adaptive Components
  - QNX has SW-Debugger included
  - Enable software side in order to use SW-Debugger
    - enable Debug port in order to access CPU
    - enable ip address in order to access CPU

What are the advantages and disadvantages of the SW-Debugger?
- Advantage: build in QNX
- Disadvantage: not safety relevant &rarr; cannot put more effort in automating the usage

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**
- Testing is performed on the target environment/hardware

Are you using any simulation environments for executing the test cases?
- There are multiple virtual environments
- There are a few tests, but no plan to further extend
- But in SiL there are restrictions, like you cannot access RoV
  - Really limited

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**
- ASPICE defines Planning and Testing processes
  - Prescribes reviewing and reporting
  - Bug ticket for issues
- According to ASPICE parallel development and testing
  - &rarr; Releases

## Testing Issues - why not?

**Regarding your specific field of work, when is a test complete?**
- Test all features of one release
  - Since not all features can be tested in one Release
  - Per new Release: new features and updates of old features
- No Deadline overall since Features can be planned to be in later Releases
  - But deadline given when Feature is in a given Release and there is a deadline for a given release

**What kind of (coverage) criteria is used, in order to measure completeness?**
- Number of features per Release
- Number of interfaces per feature

What procedures do you follow to obtain high