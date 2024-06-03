# Protocol Expert Interview with #5

**Di 12.03.2024**

_**To begin with, could you describe what your role in the testing process is and how long you have been involved in integration testing**_
- Work with integration team for 2 years
- Flashing the ADAS ECU &rarr; work with Testers and Developers
- Smoke Test in HiL &rarr; work together with device farm

## Test Object - What?

**When flashing the ECU, are we flashing the whole platform stack or just single applications?**
- Microcontroller, CPU, Ethernet SWITCH
- ASW & BSW
- All applications together

**What is tested in the context of smoke-tests?**
- Basic setup test: ECU is up and stable
  - All applications are up and running and not crashing
  - Linux Server/QNX server is up and running
  - Check interfaces are up and running
    - Network interfaces QNX server &rarr; internal
  - Communications are sent & received

**Are there any other differences between debug and prod ECU, apart from the additional debugging interface?**
- Debug version only for development
  - Debugging enabled (channel and port)
- Prod version will go into cars
  - Debugging disabled and cannot be activated/ is not possible

## Testing Methods - How?

**Which elements of the HW (Microcontroller, CPU, Ethernet SWITCH) can a HW-Debugger (like Lauterbach) access?**
- It can access Microcontroller and Microprocessor in theory
  - But mainly used for Microcontroller

**What changes have to be done from a flashing perspective to enable HW- or SW-Debugging?**
- The same software image is deployed
- But the way of flashing is different
  - Different channel and port
  - Different tools for flashing
    - Prod: only internal flashing tool
    - Debug: Windows+ internal flashing tool or Linux PC

For SW & HW-Debugger: How to enable debug mode on the ECU?
- Nothing has to be enabled
- Debug is enabled by default on debug ECU

**Are there standards or norms that prescribe how the flashing or hardware setups should look like?**
- OEM conform &rarr; just the tool at the end
- No ISO (or similar) norm

## Testing Issues- why not?

**Flashing does take one hour right? Why does it take so long and are there any efforts to reduce this time?**
- Long time since data written on ECU is huge &rarr; compress to flash to reduce time (in development, released soon)
- Aim for 45 minutes

**What are the most significant problems you face during flashing the ECU (this might include technical challenges as well as resource limitations)**
- No precise/specific problem &rarr; can be Software or Hardware related problem
- Why Hardware problems:
  - Not all ECU work in the Same Manner, there are some defects &rarr; some have an Issue (after flashing Microcontroller do not come up)
  - This is a problem on supplier Site

How to differentiate between Software and Hardware issue?
- Same software is deployed to multiple devices
  - If the issue is coming up on most of the devices &rarr; Software Issue (can be replicated on a fresh sample)
  - ECU with Software Issue can be reflashed with updated software and Microcontroller starts
  - Hardware related issue &rarr; ECU is dead, it does not start, not able to recover
    - In case of an issue &rarr; report to logistics department

## Tools & automation - with what?

**Which steps of the flashing procedure are automated at the moment?**
- Not 100% automated since manually select which files should be flashed
- Fully automated through device farm (test environment):
  - For low level flashing: manually connect Lauterbach, jumper, and remove these again
  - For internal tool flashing: only connect one channel &rarr; more automated than low level flashing

**What are the difficulties in automating the Flashing procedure?**
- Ask this device farm

**Can you describe the tool chain in use for flashing the ECU?**
- Internal flashing tool
- Low Level:
  - Windows PC and Vector Box with CANoe to send network management message to start up ECU (based on Rest bus simulation)
  - Linux PC and shell script for flashing CPU
  - Lauterbach for flashing Microcontroller and SWITCH

**How do you ensure the tools you use for testing are up to date and capable of handling the latest technology?**
- Automatic Updates no manual updates

**What role do open-source tools play in your testing process for AD?**
- Not used