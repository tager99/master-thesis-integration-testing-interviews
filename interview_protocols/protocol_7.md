# Protocol Expert Interview with #7

Thu 14.03.2024

**_"To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing"_**

- 2 Tasks
  - 1. Task: Bridging the gap between integration tests and _device farm_ tests (smoke tests &rarr; ) What are requirements that can be tested in the _device farm_? Are these requirements well tested in the _device farm_? How do the _device farm_ tests correlate with tests in the car?
  - 2. Vehicle flashing – How can flashing be improved? Perform CPU load tests.

- From October 1st at OEM &rarr; 6 months

## Test Object - What?

**On which aspect of integration testing (deployment, static or dynamic architecture, resources) do you focus on?**

- Resource Tests (CPU Load)
- Smoke Tests

**In terms of your field/your work, what is the goal of testing?**

- **Resource utilisation/CPU usage must be** &rarr; ready for series production must remain below a certain limit

## Testing Methods - How?

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**

- White-Box Testing Methods
  - Source code analysis
- Calculation/evaluation based on a lot of test data
- Test consists of different stages &rarr; takes a few minutes
  - Measurement
  - Evaluation

**How can CPU usage be measured?**

- CPU load can be output directly from the OS

**How do you specify test cases/worst-case scenarios?**

- Not in the scope of interviewee 

**On which test driver are the test cases executed and to what extent does it differ from the target environment?**

- On a single control unit: for individual engineers/use cases/software elements
- For the entire team/software:
  - _Device farm_ (relatively constant conditions)
  - HiL (comparable to a stationary car)
  - In the car:
    - standing or better driving

- Difference between _device farm_ and HiL
  - In HiL, all components of a vehicle are connected
  - At _device farm_, ECU is connected to only major components

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**

- ISO 26262 &rarr; in particular Part 5 Hardware relevant (Product development at the hardware level)

## Testing Issues - why not?

**When is a CPU Performance Test complete?**

- Reaching a certain ideal CPU usage (95-97% of the target) + when deadline is met

**What kind of (coverage) criteria are used to measure completeness?**

- CPU usage % as a target

**What procedures do you use to achieve high coverage of test cases, and how much time does it take?**

- Result is passed on to the (hardware) architecture team
  - Analysis of why high CPU load and initiation of countermeasures

**What are the most significant problems you face during testing (this might include technical challenges as well as resource limitations)**

- Hardware Resource Restriction: Limited number of available cars, which are used by several teams together (all teams in the _building_ that need to work on the car itself)
  - Car needs to be prepared (correct software version needs to be flashed)
    - Testers usually flash cars themselves
  - Different testers need different software versions
  - Colleagues who define requirements to be tested are not there during testing

- Different Approaches for _device farm_, HiL, and Vehicle

**What are possible approaches for the previously mentioned problems like .... ?**

- Better distribution/planning of vehicles
  - Assignment of specific vehicles to specific teams/groups

## Test automation & Tools - with what?

**Why is test automation important in the context of resource utilisation testing?**

- Automated testing of any version of the software
- Automated analysis of results
- Currently, software is only tested selectively

**Which test steps are automated and how is test automation implemented?**

- Automated execution and evaluation of measurement data (script)
- CPU Test – Automation with _device farm_
  - For more details ask _colleagues_
  - Test
  - Evaluation (not in the scope of interviewee)

- Procedure for test automation
  - First _device farm_, then HiL, then vehicle

**Can you describe the resource utilisation testing toolchain and what each tool does?**

- Linux computer to run the tests on the _ADAS ECU_
  - MobaXterm – SSH client to connect to _ADAS ECU_

- Test scripts from (hardware) architecture team
- Flashing using _internal tool_ for _ADAS ECU_
- CANoe
  - Verify that all IP connections are working
  - Does _ADAS ECU_ work?

- Gliwa ( [T1.timing / GLIWA embedded systems](https://www.gliwa.com/products/t1timing/) ) – for timing analysis
  - Not used by interviewee
  - Expert #12 works with it

**What are the drawbacks or annoying things of using these tools...?**

- To operate CANoe – internal communication must be &rarr; Knowledge transfer between colleagues necessary
