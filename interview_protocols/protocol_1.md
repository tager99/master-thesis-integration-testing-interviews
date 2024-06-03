# Protocol Expert Interview with #1

**Tue 20.02.2024**

_To begin with, could you_ **describe what your role in the testing process is and how long you have been involved in integration testing**

- Test methods and test automation for SWE 5

## Test Object - What?

**Can you explain what the black box does and if it is also part of integration testing?**
- _Black box for ML by supplier_
- Here, only the interfaces are tested, not the content of the Black box itself

**You're dealing with (test methods, & test automation). In which test categories (deployment, static/dynamic architecture or resource testing) are you involved?**

- Static and dynamic interface tests

**What is the goal of testing in terms of the test categories you mentioned?**
- Testing all interfaces
  - Static: each signal arrives, the signal is correct, source of the signal
  - Dynamic: the signal arrives on time

## Test Methods - How? – How

**Which test methods are used at the moment to achieve the previously mentioned goals like ....?**
- Currently two options, mainly for static testing
  - Using HW debugger
    - ! HW Debugger influences Dynamic behavior
  - SW debugger runs on the ECU
    - ! SW Debugger influences Resource consumption

- For details: Ask testers 

**Which norms and standards are relevant for the testing process how do they affect your work/ testing?**

- ISO26262 and ASPICE

## Testing problems - why not?

**Can the test object be fully tested in practice, and if not, what are the underlying problems?**
- Measurability; The main problem here is dynamic interface testing &rarr; looking for possibilities 
- Lack of test automation
- SW Debugger Problem
  - Also consumes resources
  - You can only deploy a part of the SW at a time

**What are possible solutions to the previously mentioned problems such as ... ?**
- Debuggers read static and global variables
- HW & SW Debugger
  - e.g.: Lauterbach (HW Debugger)
  - internal Debugger Testing Framework 
  - GNU Debugger (SW Debugger)

- For details please refer to other stakeholders

How do the debuggers work:

- Ask colleagues 

**I have looked at the** _internal testing framework_. **How does it connect to the ECU (with which interface)?**
- Communication via Ethernet 
  - SOME/IP + UDP

- Alternative to Debugger

Does this require any changes to be made to the software on the ECU?
- Yes 
  - Setting Correct Log Levels
  - the SW must be started with debug symbol
  - in order to read global and static variables, the source code must also be adapted

Will the test framework be further developed and what functionalities should be added?
- In the future, it should be possible to **carry out dynamic** tests
  - To do this, a SW debugger must be installed
  - SW Debugger Included in internal Test Framework

## Test Automation

**Why is test automation important for integration testing?**

- Without test automation, it is impossible to check all requirements (in terms of static & dynamic interface tests)

**Which test steps are automated and how is test automation implemented?**
- Test case generation and test case automation are equally important
- Test case generation with AI: But no one looked at this due to time constraints

Does the test object need to be modified to automate testing?
- You can only test part of it at a time, because SW-Debugger also runs on the ECU
  - For new component, new SW debugger
  - How to Use HW Debuggers for Test Automation?

Are there dependencies on other teams (or external partners) that influence the use of test automation?

- Regarding test automation, also ask (internal) testers

## Tools - with which ones?

**What tools are used to document the requirements for the object to be tested?**

Can you understand the pros and cons of using the tool? Explain?

Who or which groups are involved in the selection of the tool?
- Rhapsody is used by testers
  - Since not used by interviewee, no further statements

**Which tools do you use as part of the above-mentioned test methods or test automation?**
- Debugger
  - HW: Lauterbach 
    - From the company Lauterbach

  - SW: e.g. _internal test framework_

Where is the use of the tool helpful and how does it simplify your work?

- Enables measurability &rarr; of interface tests

Are there any drawbacks to using the tool...?
- SW Debugger: runs on the SW and thus influences the use of resources
- HW Debugger: dynamic tests are not possible because the signal transmission