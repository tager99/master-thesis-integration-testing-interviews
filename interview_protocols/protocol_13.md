# Protocol Expert interview with #13

Wed 17.04.2024

**"To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing?"**
- Focus on the next generation of the non ADAS ECU
- Not involved in in-house integration testing for the current generation

**Test Object -What?**

**What are the tasks of the non ADAS ECU and what does the associated architecture look like?**
- Connection of many bus systems: CAN, FleyRay, LIN, Ethernet

AUTOSAR Classic? Adaptive? Both?
- 100% AUTOSAR Classic
  - Parts of the software are not yet available.
    - Legacy Modules
  - Challenge

CPU and/or microcontroller?
- A microcontroller control unit for current generation

Is the ECU a real-time critical system?
- Yes

**ASPICE describes various aspects to be tested in the context of integration tests, such as deployment, static & dynamic aspects, resources. What aspects are tested and how can they be prioritised?**
- At OEM: pre Software Integration - Integration of the functional sets developed at OEM - objects are delivered to Tier 1 supplier
- T1 supplier then does the overall integration - creation of flash file
- Prioritization - ask colleague

**What is the goal of integration testing?**
- Differentiation between
  - Current generation: Pre-integration of functions - Object Files to Tier 1 Supplier for further details Colleagues
    - Also important here: Artifacts (ARXML) that come from OEM and are incorporated into the overall integration, and Base Layer Stack fit - together Consistency and compatibility of artefacts and supplier stack
  - Next Gen verification of integration of artefacts (then developed in-house) such as: communication matrix, information from PREEvision, middleware, LET (Logical Execution Timing - deterministic call order)

**Testing Methods - How?**

**What testing methods are currently being used to achieve the aforementioned goals?**
- There's a lot going on with the Tier 1 supplier
- For next gen: in-house team dealing with the interpretation of ASPICE and ISO 26262
  - Exact implementation: BROP (Basic Rollout Plan) Milestones for securing the basic software
  - Regression test for add-ons (not included in the base layer)
  - Gating concept for different branches under construction - Preconfigured tests from the regression tests - Ensuring that a minimum of green must be passed through before committing to the next industry level - In the end, a stable branch for serial software, testing, etc
- Signal Chain Tests
  - Software clusters (bundling of functions) have interfaces to the base layer, - function modules use this interface
  - Signal chain test checks whether consistency of interface to software cluster (with the help of dummy interfaces) via RTE, to bus systems (CAN, LIN, etc.) - Connectivity of software clusters to bus systems reading and writing (ECU limit)
    - No functional module behind it, it's all about consistency

**In which test environment are the test cases executed, and how does it differ from the target environment?**
- Current gen: Test on Tier 1 supplier side - therefore no insight
- Next Gen:
  - use of SiL
  - For basic software, target hardware is available at an early stage
    - First virtual, then target hardware

**Which norms and standards are relevant to the testing process, how do they affect your work/testing?**
- ASPICE
- ISO 26262
- Must be implemented for next gen itself
- Current requirement passed on to the Tier 1 supplier (via requirement specification)

**Testing Issues - why not?**

**When is integration testing complete?**
- For next gen: no statement currently possible
- In House Tests
  - Artifacts (middleware, LET, etc.) are coherent

**What (coverage) criteria are used to measure completeness?**
- For next gen: no statement currently possible
- In House Tests - for Details ask colleagues

**What are the biggest issues you face during testing (these can include technical challenges as well as resource limitations)?**
- Iterative process with supplier lengthy
- All OEM parts must work perfectly together with supplier components
- Different suppliers (e.g. Elektrobit, Vector) can implement - AUTOSAR differently, which is difficult if they are to be integrated together
- Interaction of software itself, tools and workflow

**What are possible solutions to the previously mentioned problems such as ... ?**
- Focus on one supplier/manufacturer?:
  - Base layer by Vector
  - Use of Vector tools (Davinci etc.)
    - Particularities: Cluster concept, LET topic (deterministic call order)
    - increase complexity for configuration, tooling, etc.

**Test**

**Why is test automation important?**
- Know and verify all requirements
- Traceability
  - Not only the results, but also how these results came about (which software version, which test instance, which time, testers)
- without test automation: Complexity as with discussed non ADAS ECU or ADAS ECU not manageable

**Which test steps are automated (especially in relation to test case creation)**
- Test scopes before a commit (topic gating)
- Integration tests at different levels
- Resource Testing and Resource Analysis

**What are the challenges of automating all test steps?**
- Requirements should be stored centrally (for deriving test cases)
  - DNG and PREEEvision
- Handling of various tools: DNG, PREEEvision, XRAY Plugin for Jira, internal tool for test management
  - Traceability
  - Standardization among each other
  - Robustness
  - Deriving Metrics
- In the end, many different pipelines that have to work together in an orchestrated way

**How is test automation implemented (tools)?**
- DNG, PREEEvision - Requirements
- XRAY Plugin for Jira
- Internal tool for test management - Documentation of Testing

**Tools - with what?**

**What tools are commonly used in the testing process and what is their job?**
- Compiler (TASKING)
- Davinci Developer for designing software architecture of software components
- DaVinci Configurator for configuring BSW and RTE
- DaVinci Team for Continuous Integration
- PREEvision for model based development
- Non ADAS ECU specific internal tools
  - In the focus of colleagues
  - "AUTOSAR" Tooling
  - Where Vector Tools Can Reach Their Limits
  - To be able to use AUTOSAR efficiently

**How do you make sure the tools you use for testing are up-to-date and can handle the latest technology?**
- For the internal tools:
  - Danger as few experts - high dependence

**What role do open source tools play in your AD testing process?**
- Should be possible, or is planned
- The basis for this is standardised interfaces that - link tools to them
  - Different tools for different test instances needed HiL, SiL, test bench, etc.
  - More Focus other Team

---

**Overall, are there any points that you think are relevant that we haven't discussed yet? Do you have anything to add?**
- Key points were discussed
