# Protocol Expert Interview with #8

Fr 15.03.2024

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_

- Test manager for Software Integration Testing SWE 5
  - Work along with _colleague_ (also Test Manager) &rarr; support defining test strategy, test scope
  - Work closely with quality management with respect to KPI (process-wise)
  - Test strategy is defined on project test plan
    - How to implement requirements from ASPICE, _internal QM_ in testing
    - Strategy with respect to regression strategy, ...

- Joined _OEM_ Software Integration testing in 2022 December as Test Manager

## Test Object - What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**

- Focus mainly on static aspects, dynamic aspects (application and model-wise) and resource
- Deployment is seen as given/input

**How can the different aspects be prioritized?**

- Prioritization (Which Module to test first) is given by Release
  1. Dynamic architecture: Check performance and scheduling of applications
  2. Static Architecture: different modules interacting in the defined range
  3. Resources: each application is within the defined range

**For each previously mentioned aspect like .... What is the goal of testing?**

- Make sure that all Modules are integrated **properly**
  - Application level: one application is able to interact with other applications
  - Module level: Modules should interact properly
  - Scheduling
    - For example: higher priority application (master) it should publish semaphore &rarr; should be accepted by lower priority application and process data in given time range &rarr; master should log error if lower priority application does not process data in time

**What has to be tested in the context of (deployment, static, dynamic, resource utilization)**

- Dynamic: check the flow &rarr; sequence in a given time/cycle
  - Application level &rarr; check the overall application (e.g. init time); flow of application based on period
  - Module level

- Static:
  - Check If module receives Data from outside/Bus (RoV)
  - For all interfaces: Check if input and output data is in the defined range

- Resource utilization
  - RAM
  - ROM (static)
  - CPU Load
    - Core level: Utilization in % &rarr; core wise not more than 80% (very easy)
    - Applications level and module level (difficult): Max execution time in ms for modules &rarr; how much time does it take for execution

## Testing Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**

- Different options like equivalence class, error conditioning, analysis of use cases and scenarios, state machine, control flow analysis
- Dependent on input, pick suitable technique and coverage criteria
- Equivalence class portioning for static architecture testing:
  - 7 test cases (e.g. valid range from 0 to 100) with valid and invalid values:
    - 3 around lower boundary -1; 0; 1
    - 3 around upper boundary 99; 100; 101
    - 1 in the middle

- For dynamic as of now more about checking the scheduling by reading values
  - For module level: Checking based on state machine and scenario is planned for the future

**Does the test object need to be changed in order to apply the test methods, and if so, what needs to be changed?**

- Certain Preconditions have to be met (e.g. power train signal has to be 1, Features has to be enabled by variant coding (part of the flashing))
- No additional software has to be deployed

**For which use cases do you use SW-Debugger?**

- **For static** architecture 2 types of communication (IP-Communication and shared memory)
  - IP Communication &rarr; CANoe
  - Shared memory &rarr; SW-Debugger
    - Solution:
      - list of all processes running in the application
      - attach these processes to the Debugger
      - go to the Line of Code (by setting breakpoint) where tester wants to read or manipulate the data

- not used for dynamic aspects

**What are disadvantages of the SW-Debugger?**

- A lot of manual effort at the moment: analyze code, set breakpoints

**For which use case do you use HW-Debugger?**

- Will be used for communication between Classic AUTOSAR (_Microcontroller_) and Adaptive AUTOSAR (_CPU_) &rarr; has to be planned
- Lower priority than testing Adaptive since most of the Requirements are on the Adaptive AUTOSAR side

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**

- As for now all on the actual target hardware

**What are the major limitations of using a simulation environment:**

- Lot of signals are coming from RoV
- Not everything can be part of the SiL &rarr; would lead to performance issues
- Not all signals available in SiL which need to be manipulated for integration testing

**Which norms and standards are relevant for the testing process how do they affect your work/testing?**

- ASPICE
- _Internal QM standard_ &rarr; for process
  - Want to see the evidence for testing (not interested in the actual content, but see that it's done)
  - &rarr; use tool _internal testing tool_ for documenting and reviewing test cases

## Testing Issues - why not? ~ 15min

**Regarding static and dynamic testing, when is a test complete and what kind of (coverage) criteria is used, in order to measure completeness?**

- Static: all interfaces are tested with positive and negative scenarios
  - Open points: Communication Adaptive & _Black Box for ML_

- Dynamic: not fixed since very new topic

**What procedures do you follow to obtain high coverage of test cases and how much time does it take?**

- First check if the preconditions were met correctly
- Execute tests on different test benches
- If test fails on all test benches, and preconditions were set correctly &rarr; create bug ticket (assign to developer if known)

**What are the most significant problems you face during testing (this might include technical challenges as well as resource limitations)**

- Technical challenges:
  - Gap between architecture model and implementation in the code &rarr; not a major issue since it does not block
  - major problem: preconditions are not matched &rarr; testing activity is stopped
  - for dynamic testing: Variables (like semaphores) need to be accessed (&rarr; has to be set to public by developers)
  - timing delays in AUTOSAR Adaptive

**What are possible approaches for the previously mentioned problems like .... ?**

- static: mirror code without changing functional behavior and add instrumentation (in replica code) for testing purposes (should be possible since white-box)
- general: one tool or one framework for testing both Adaptive and Classic AUTOSAR without timing delays

## Test automation and tools: ~ 15min

**Can you describe the tool chain for the testing process (including test automation) and what the respective tool does?**

- Tool for Classic: Lauterbach (HW Debugger)
- Tool for Adaptive for shared memory: GDB (SW Debugger)
  - Cannot be automated

- No unified tool for Classic and Adaptive
- CANoe: for simulating Tools on the bus
- _Testing tool for black box for ML by supplier_
- Framework &rarr; for uploading test results directly into _internal testing tool for documentation_

**How do you ensure the tools you use for testing are up to date and capable of handling the latest technology?**

- In case something does not work or if new features adaptions are necessary
- In case of driver issues &rarr; update tools &rarr; if error persists get in contact with suppliers directly (vector, Lauterbach, ...)
- But mostly driver update, tool update is enough

**What role do _open-source tools_ play in the testing process?**

- No
