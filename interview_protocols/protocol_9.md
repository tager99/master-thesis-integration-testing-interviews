% docx2tex 1.9 --- "How I learned to stop worrying and love DOCX"
%
% docx2tex is Open Source and
% you can download it on GitHub:
% https://github.com/transpect/docx2tex
%

# Protocol Expert Interview with #9

Di 19.03.2024

_**To begin with, could you describe what your role was in the integration (testing) team, what your current role is in the architecture team and how long you have been working or have worked in these areas**_

- **Integration testing team**: work on Integration
  - First year:
    - Resolve issues appearing during integration (like system stalls, not properly aligned APIs, components where versions do not work together)
    - Prepare sample devices with new software configuration
    - CPU load task force – troubleshooting crashing IDC
  - Second year:
    - Product owner/manager for software updating
    - Identify work streams
    - Special focus on security

- Software architecture team for application software for 3 months
  - Software framework aspect &rarr; abstract design ideas

## Software Application Architecture

**I have heard many different keywords while familiarizing with ASPICE, ISO26262, Architecture Proposals, and expert interviews with the integration testing team. Can you explain or show me the following concepts (AUTOSAR Adaptive): SW application, SW Container, SW component, Module?**

- Container: Application compiled for a certain variant
- SW component = Module (in the context of the deployment diagrams)
- Inside applications modules
  - Further described in detailed design (not part of architecture)
- Keywords like application, container, component, module don’t really map 1 to 1 neither to implementation nor the language used in architecture

**Does the hierarchy always stay the same (1 level SW Container, 1 level SW component, 1 Level Modules)?**

- Yes, deployment hierarchy is relatively stable, hierarchies for framework/detailed design change more frequently as needed
- You cannot reverse engineer the hierarchy from the implementation
- Discrepancy between architecture in Rhapsody and Implementation (code)
  - Since no code generator inputs architecture diagram and outputs code (on the interface level)
- &rarr; Static and dynamic architecture artifacts serve as strong guides for implementers but they can be violated

**Who is defining the (functional) behavior of software architecture elements?**

- According to ASPICE Software Architecture (SWE 2)
- In practice: System function owners (SWE 1) collaborate frequently with module owners/developers (SWE 3) &rarr; System Requirements make it directly to the Developers
  - They also test the functional behavior

**Is the visibility of variables defined in the software architecture? If yes, when are variables set to global in Adaptive or Classic? Why don't set all variables used for communication just set to global?**

- Classic design question
  - If set to global, doesn’t disappear from the stack for the lifetime of the application &rarr; not necessary, consumes resources
- Pretty sure that ISO norm restricts global variables for ASIL critical use cases
- Suggestion for testing: add testing layer with global scope, but application code cannot have such design

**What are static aspects of the software architecture and where are they documented?**

- Deployment diagrams
- Class diagrams

**What are dynamic aspects of the software architecture and where are they documented?**

- Activity diagrams
- Sequence diagrams
- More detailed, specific descriptions (beyond artifacts above) in architecture decision records
  - Not captured in Rhapsody, captured in Doxygen comments in code, detailed design can be auto-generated from these comments
  - Goes more to detailed design

**How are the ASILs assigned to the elements of the software architecture?**

- By safety team
  - ASIL on module level (based on what the function does)
  - &rarr; then it is assigned to the respective **application**
- For more details **colleague**

**Can you explain the process of defining which feature is in which Release?**

Feature roll out plan (FROP) defines which feature should be in a particular release

- &rarr; translated into initiatives owned by function/system owner
- Integration view: Upcoming release date for which to prepare an integration branch
  - Tell developers: tag changes or target branch for merge request
  - Code reviewing is discouraging
  - &rarr; more just managing the merge requests (approving)

**Which norms and standards are relevant for the software architecture how do they affect your work?**

- ISO 26262
- ASPICE
- AUTOSAR Spec
- (For detailed design)
  - MISRA
  - C++14

**I know from previous interviews that testing the inter-module communication is difficult, since it is hard to measure and especially inject data since no tools are available. One approach could be to tackle integration testing early in the design phase of the software architecture. From an architecture point of view, is this doable?**

- Yes, but that should not really be the scope of architecture
  - Since it is not related to developing the product or solving problems to realize a feature
  - Architecture is already burdened with developing tasks
- But SWE2 should be consulted because integration testing depends on Software Architecture

**_All in all, are there any points that are relevant from your point of view that we haven't discussed? Do you have anything else to add?_**

- New requirements SWE 1 late in the project &rarr; also affects architecture
