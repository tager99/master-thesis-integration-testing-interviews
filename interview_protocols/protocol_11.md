# Protocol Expert Interview with #11 (2 Experts)

Thu 21.03.2024

## Device farm General

**What is the device farm?**
- Device farm = hardware farm
- History: Started 6 years ago in the context of the infotainment and telematics domain
  - 1. Year PoC 
  - In productive use for 5 years
  - In the first 2 1/2 years only infotainment and telematics domain
  - After that, scaling into the width &rarr; of other ECUs
  - Organizationally shifted from infotainment development to system integration &rarr; change of scope &rarr; at least BIG domain ECUs

- Value Proposition:  Test environment Provider 
  - Or. Hardware as a service provider
  - would take a conceptual view of it a bit more broadly, as architecture is not only tied to hardware, but also virtualised ECUs, real vehicles, etc. conceivable

**What are the tasks/objectives of the device farm?**
- Test Environment Provider in Standardized Form 
- Great motivation behind it:  Reduce Test Automation Costs
- Before that: Test automation for individual special test environments (e.g. HiL, virtualised environments, audio tests, navigation tests) do not form a common basis  
  - Automation against certain tools (e.g. tools from Vector) 

- Goal: Writing test automation against defined interfaces (the device farm)
  - Regardless of the test environment (virtualised, HW, vehicle)
  - There are many test cases that could be executed across the whole range of test environments, &rarr; test cases only need to be written once

- &rarr; HiL, SiL maximum relief
- The main task today: Hosting of ECUs

**What are the differences to HiL?**
- HiL is bigger and more complex
- Mostly domain HiLs &rarr; small ECU network
  - e.g. telematics domain with all relevant ECUs

- no HiL with all ECUs
- very high costs
- &rarr; device farm as one/two instance(s) before the HiL 
  - Filtering out (e.g. flash problems) 
  - Only what is relevant in the HiL and can only be tested using complex setups such as the HiL

- Advantages/possibilities of the device farm:
  - Parallel tests on different units
  - In the Loop
  - High variance of units available

- Fewer HiLs than units in device farm &rarr; Hardware in HiL has to be replaced again and again if other versions of the unit are to be tested
- HW peripherals (actuators/sensors) in the device farm slimmed down

**What is between device farm and HiL?**
- BROP (Base Rollout plan) instance for testing diagnostics, flashing,...
  - device farm already relieves BROP

- CSI - Component System Integration
  - 72h Scenarios in the Loop
  - More specific use case

- Device Farm &rarr; BROP or CSI &rarr; HiL &rarr; Vehicle

**How is it decided how much peripheral is connected to the device farm?**
- No fixed boundary
- Depending on how many users have this use case
- device farm is not used as remote management of a dedicated bench
  - No guarantee that Bench will look the same every day (e.g. due to changed HW) or that Bench will be functional every day
  - &rarr; Customer request how setup should look like (offered by device farm) &rarr; either there is something free or you have to wait

- If very exclusive, or very small group then setup is not available in device farm

**What is the role of the device farm team?**
- Hosting site of the device farm
- Development of software stacks (rollout automation, flash automation service, web UI)
- Most of the operation at the partner (standard operation 24/7)
- one project owner per control unit

**I know from the ADAS ECU that there are debug and prod versions of the ECU hardware. Which versions are used in the device farm both in terms of the ADAS ECU and the other ECUs?**
- Usually with dev/debug versions
- Since prod versions no longer allow access to debug interfaces &rarr; standard test scenarios are less attractive
- Testers want to have logs in case of error (to debug the problem, etc.)
- Prod versions also in use, mainly for flash tests

**What are the problems/difficulties that arise during the operation of the device farm?**
- Objective in terms of operation: Reduce manual tasks and automate as much as possible 
- Difficulties/Challenges:
  - Automate: Dependencies in tools (e.g. no command line, REST interfaces)
  - Testers leave systems in poor condition &rarr; , device farm automatisms (flashing back) then no longer work 
    - e.g. device-specific information has been changed/damaged &rarr; , unit is initially no longer usable
    - no deterministic (initial) state possible
    - In the event of a problem, it is difficult to find the right gender neutral preferred in the project who can help ("device farm -only problem")
    - Difficult when many benches are affected (e.g. due to bad pipelines) &rarr; Manual workarounds unacceptable &rarr; **Automation essential for an efficient development process**
    - Positive example ADAS ECU: each merge request must be tested via device farm device 
      - if test fails, &rarr; no merge
      - from an device farm point of view: if unit destroys &rarr; , there is a lot of self-interest on the part of ADAS ECU to debug/fix it in order to get the merge request through again
      - Risk of failures in the device farm infrastructure &rarr; Merges on Hold

- relatively stable infrastructure (device farm Environment itself)

**Which norms and standards are relevant for the Device Farm and how do they affect your work?**
- No ISO standards to meet
- Will not be integrated into ASPICE compliance across the board

## Testing on the device farm:

**What types of tests can be performed on the device farm?**
- Use-case specific - &rarr; advisory function by device farm team
- Domain ECU: Diagnostic, Security, Network Test Suite
- ADAS ECU: Pipelines test, startup behaviour (processes started, resource anomalies)
- Domain ECU: Application tests (UI tests)

**What is the process for running tests on the device farm?**
- People should only test automatically 
- Triggered by a pipeline
  - Booking a Device from the device farm +Requests to be supported by the device
- device farm Returns Device (Service Document with API Entry Points)
- Flashing (via API call or via service from device farm)
- Test Case Execution

- First, run "System sanity test": is the given system testable with the binaries?

## Test automation using device farm:

**To what extent are you, as an** device farm **team, integrated into the automation process?**
- Integrated into various construction sites in the field of automation
- Automation around flashing is very important
  - Flash Automation: device farm requests command line tools from the respective projects to start &rarr; a flash procedure, write service layers around it
  - Interaction with the projects
  - Percentage of problems with flashing: mostly on the project itself and less on the device farm test infrastructure

**What are the challenges of test automation?**
- Flashing
- Is the problem with the ECU or infrastructure? 
- ECU-specific challenges in general and thus also automation
  - Infotainment ECU: Latencies (guarantee audio stream and video stream synchronisation)
  - Other domain ECU: Many different bus systems
  - ADAS ECU: Guarantee latencies synchronisation (e.g. for functional tests)

**Are there any overall points that are relevant from your point of view that we have not yet discussed or are there any comments on your part in general?**
- Very big challenge: Sensitivity to robust **(test) automation** (preferably over generations)
- And testing of valid setup structures (and not of structures that cannot be assembled by the customer)


