# Protocol Expert interview with #10

Wed 20.03.2024

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_

- Half a year for the ADAS ECU
  - Test Methodology – How to Test SWE 4/5

- Since 2016 Software Integration: SWE 4/SWE 5 Scopes, Tools, Process Description

  - Worked in different projects at OEM
  - in the context of gearbox &rarr; in this case "bare metal" software, i.e. without AUTOSAR
  - responsible for test automation (3 to 5 years ago)

## Test Object -What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**

- Current Focus: AUTOSAR Adaptive Application &rarr;, vertical integration &rarr;, focus on all interfaces that are controlled by the Adaptive applications
  - The basis for the assignment is the ISO26262-&rarr; requirements for methodology and tests, therefore static and dynamic aspects from the field of SWE5

- Highly dependent on the project context: In previous projects: reduced scope (mainly smoke tests), rest moved to system tests
  - The extent and when testing is carried out is determined by the test manager
  - Should be determined early
  - &rarr; not consistent: depends heavily on the architecture, the controllers used
    - Here ADAS ECU is special: because many architectures come &rarr; together Classic, Adaptive, Virtualization &rarr; many different interfaces

What works without QNX:

- Microcontroller with AUTOSAR Classic
- Additional components such as controllers for network switches run bare metal (without abstraction layer or OS)

**What is the goal of the integration test?**

- Alignment of requirements at the architecture level
  - Has all elements been integrated together correctly
  - the elements of architecture play together in the right way
  - All interfaces are operated

- Finding errors early in the process, and not only in the fully configured system (vehicle)
- Verification that standards such as ISO26262 are complied with (e.g. guarantee that certain signal transit times are met)
- Systematic testing (no longer possible at system level)

&rarr; Trade-off effort vs benefit 

## Testing Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**

- Test methods according to ISO26262
- Depending on the interface, different tools/protocols can be used:

**AUTOSAR Classic source**

Why is XCP fraught with question marks?

- Typical approach at Classic: XCP
  - Install &rarr; instrumentalized software Install switches in the software to activate error states or specify signals
  - Has XCP stack but is not used &rarr; cannot be used for testing purposes
    - Lack of instrumentation
    - Lack of configuration of the stack in the software components
  - Not finally clarified whether this will remain the case
  - XCP is the preferred solution, but currently technically not available

How does testing with XCP work and what changes do I need to make to the code?

- Software switch is built into the code with variable
- This variable is then parameterized via XCP (e.g. using CANoe)
- Measuring using XCP 
  - Variables in a function can be linked to XCP
  - A2L file contains information at which address a variable is stored
  - Variables must be statically allocated
  - Bandwidth is limited &rarr; Data cannot be sent on change, either periodized (high load!) or on demand

&rarr; Measuring and contributing value

&rarr; XCP stack needs to be configured and integrated, and software instrumentation in the implementation (both of which are missing for the ADAS ECU)


**CCPLEX APP source**

What changes do I need to make to the test object to use SW Debugger?

- No change to the target software
- QNX’ debug server needs to be started

How does the SW Debugger work and how does it affect testing:

- Adaptive AUTOSAR environment (basic software and application software) consists of many individual processes
- SW Debugger connects to a single process 
- SW Debugger + pauses execution at breakpoints (code sections relevant to the test) if desired
- Host PC with client application receives application with debug symbols (information that the debugger needs to observe the process)
- Debug server stops the process and reads addresses from &rarr; transfers to client
- You only stop one of many processes (relatively long lasting ~40 ms) &rarr; possible influence on the scheduling

Can all processes be stopped at the same time?

- The SW debugger can't do that (only gets to the process, but not to the hardware) &rarr; Operating system level
- But HW Debugger can do that because it stops the clock of the CPU

How can I test, if the SW debugger can mess up the scheduling?

- Static aspects possible:
  - If a signal arrives from A to B,
  - Time behaviour irrelevant

How can dynamic aspects then be tested?

- Time-of-flight measurement (scheduling)
  -  Gliwa Toolkit
  - Profiler by QNX

Within an application/process, is the use of a SW debugger sufficient? 

- In principle, yes
- but within an application no signal propagation times for signal transmission &rarr; no requirement signal has to be sent within X ms from A to B
- what's available in applications: Program Flow Cases

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**

- ASPICE 
- ISO 262626
- (ISO 9001 Requirements for Quality Management Systems) 

## Testing Issues - why not?

**When is a test (regarding? static/dynamic aspects) complete and which coverage criteria are used to measure completeness?**

- Are all requirements covered?
  - Usually not 100\% possible &rarr; , difficult to cover all states (e.g. certain RAM errors)
  - Ca. 85\% is already quite good (guideline)

**What are the most significant problems you face during testing (this might include technical challenges as well as resource limitations)**

- Black Box for ML Testing Tool does not work
- Hardware Debugger
- Software Debugger

**What are possible approaches for the previously mentioned problems like {\ldots} ?**

**Virtualized ECU:**

Isn’t SIL = virtualized ECU?

- Yes, there are: QEMU = CPU virtualisation
- but peripherals are only simulated in a reduced form (Ethernet, sensors, camera, I2C...) &rarr; The goal is usually to make the simulation executable

**AUTOSAR DLT \& Calibration:**

AUTOSAR DLT and calibration &rarr; promising

- Advantages: High performance, low cost
- Disadvantage: Testing must be taken into account in the design, in the implementation

How to calibrate in AUTOSAR Adaptive?

- via XCP to inject data &rarr; states/values "calibrated" via XCP
- and DLT to measure because much less overhead

Can XCP (interface) be implemented in AUTOSAR Adaptive?
- Not looked at in detail
- But don't know that XCP is not available in AUTOSAR Adaptive

Do you know if they are working on a tool (external) to test AUTOSAR adaptive communication?
- There is currently no tool on the market

## Testing Tools – with what?

**Which tools do you use in the context of the above-mentioned test methods?** 
- Rhapsody (here the requirements/architecture are documented) + Confluence
- HW Debugger; Examples: 
  - Lauterbach
  - Sysmon
- SW Debugger
- CANoe for ROV (Rest of Vehicle)
- Gliwa

**Overall, are there any points that you think are relevant that we haven't discussed yet? Do you have anything to add?**
- It is important to: think about how you want to test at an early stage, which tool is suitable
- No tool that covers everything, only individual tools for individual aspects to be tested
