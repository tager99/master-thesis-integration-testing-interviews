# Protocol Expert Interview with #12

Wed 03.04.2024

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing?**_

- Part of a team that is responsible for resource testing - Divide work among others

## Test object -what?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**
- Resource Testing/ Performance Testing
  - Measurement (long-term measurement, debug measurement)
    - Responsible for methods of measurement
    - Responsible for selecting which software functionalities should be the focus
    - The actual measurement is carried out by testers
  - Analysis and optimisation suggestions

**What is the goal of resource testing?**
- AUTOSAR Classic (previously) + now in combination with AUTOSAR Adaptive
- Motivation Behind Resource Testing and Optimization:  Embedded Safe System needs to be developed/tested differently than application software/desktop software - many requirements in terms of optimising software to be efficient and minimise risks
  - If there is no memory available (as part of dynamic memory management) - software aborts
- Measurements/collection of utilisation/performance data
- Performance analysis and optimisation suggestions
  - Most difficult task
- Until SoP is below 80% resource utilisation - only the software that does not use more than 80% of the resources in total will be installed

**What needs to be tested as part of resource utilisation testing?**
- CPU
- RAM
- ROM

## Test Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**
- 2 types of measurements at runtime
  - Long-term measurement
    - What is needed here is a solution that is - not really intrusive: Minimalist - Finding Peaks
    - Peaks are relevant, not the average 
    - Average mostly good, but timing and framework conditions of peaks relevant
      - AUTOSAR Classic - XCP as a measurement technology for long-term measurements
  - Debug Measurement for Expert Analysis
    - Contains more information about threads, etc... so that experts can analyse a peak
    - Possible for old projects/Classic - Many frameworks/states could be read from the kernel
    - Temporary solution currently not possible - in Adaptive: Collect trace files
      - QNX has a microkernel (not a monolithic kernel) - in the kernel itself, no drivers/"third-party software" but only basic functions - light and minimalist
        - Drivers are in userspace instead
        - In kernelspace kernel only: "Conductor of the Orchestra"
      - low chance of the kernel crashing 
      - QNX Kernel offers a solution for measuring: tracelogger with 2 modes in QNX
        - Linear Buffer mode: when limit/80% of the buffer (memory zone in kernel space) full - tracelogger is run to flush - the buffer save to file
        - Scheduling of tracelogger affects system or trace itself
        - hence the second solution
        - Ringbuffer mode:  will be filled permanently, if full data is overwritten - on request buffer will be flashed - into file

**How can resource utilisation (CPU, RAM) be measured?**

- Is it output from the OS

**How do you specify test specifications/worst-case scenarios?**
- In the vehicle
- Peaks in utilisation are not known - in advance Worst-case scenarios cannot be specified in advance
- Trying to stress the software to create peaks
  - E.g. while driving, activate software functionality and combine it with a manoeuvre (e.g. (automated lane change)

**In which test environment are the test cases executed and why?**
- Simulation Environment - SiL
  - For e.g.  Memory leaks (not detectable by analysis of the code) - valgrind memcheck
  - For how long does software stay active in a block (percentage) - valgrind callgrind
  - On other OS
  - Absolute time-of-flight measurement makes no sense in simulation
  - With tool: Valgrind (instrumentation framework) - is very intrusive, but can be used in simulation because absolute runtime is not relevant
- Target hardware with target software (OS) 
  - Resource Measurement
  - HiL
    - Better than SiL, but worse than vehicle
    - Driving aspect is missing
    - On the basis of already existing data/trips, - the "new" is missing
    - Advantage if individual sensors want to be simulated (e.g. in the case that a sensor measurement is incomplete/incorrect during a journey)
- Vehicle
  - Best environment 
  - Target vehicle is better than (converted) test vehicles, as many components in the test vehicle can differ from the components installed later

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**
- ISO 26262
- Internal requirements:
  - Among other things:  Utilization of all resources must not be higher than 80%

## Testing Issues - why not?

**Regarding resource tests, when is a test complete?**
- Testing Goes Beyond the Limit of 80% Resource Utilization

**What kind of (coverage) criteria is used, in order to measure completeness?**
- CPU Usage in % ?
- RAM utilisation in % ?
What procedures do you follow to achieve high coverage of test cases, and how much time does it take?
- Analysis of the measurement and optimisation suggestion - Create ticket
  - E.g. use int instead of string

**What are the most significant problems you face during testing (this might include technical challenges as well as resource limitations)?**
- General: Introduction of new technology such as AUTOSAR Adaptive leads to new problems
  - In particular, the introduction of dynamic memory allocation is problematic (e.g.: Use of std::vector ) - dangerous for performance
- No XCP in Adaptive currently, as dynamic memory allocation - does not require predefined addresses in advance
- XCP is intrusive - XCP itself consumes resources/runtime

**What are possible approaches for the previously mentioned problems like ... ?**
- Ask Suppliers to Integrate XCP

## Test automation & tools - with what?

**In which test environments are resource tests automated?**
- In the HiL, resource tests are carried out automatically 
  - Useful in case of new software versions
- in the vehicle: Automation is not possible

**Can you describe the resource utilisation testing toolchain and what each tool does?**
- Vector Tools & XCP (available for AUTOSAR Classic Tools)
  - During the measurement, data is transported directly from the control unit to the measurement technology
- Valgrind (instrumentation framework - provides a number of debugging and profiling tools) - is very intrusive, but can be used in simulation because absolute runtime is not relevant
  - Can also be used on the control unit
  - Callgrind - which parts of the functions were called
  - Memcheck - detects memory management problems
- Gliwa (available for Classic and Adaptive)
  - Event-based
  - Requires a Windows laptop connected to the control unit during the entire measurement
  - For in-depth analysis
  - Can also  be used for long-term measurement
- tracelogger for In-Depth Analysis
- Lauterbach and Trace 32 for testing on a HW-Bench or HiL
  - Very intrusive
  - Uses debug interface of the control unit

**What do you consider to be the most significant challenges in automating resource tests?**

- Ensuring non-intrusiveness of the measurement
- Availability of interfaces for measurement

