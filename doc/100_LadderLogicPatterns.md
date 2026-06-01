# Patterns of Ladder Logic Programming

**Category**: Auxiliary / Foundational  
**Folder**: `DesignPatterns/100_PatternsOfLadderLogicProgramming`  
**Credit**: Scott Whitlock (contactandcoil.com)

## Intent

Capture common, recurring constructs in ladder logic as reusable, self-contained function blocks. These are not GoF patterns but rather the fundamental building blocks of safe, maintainable PLC code.

## PLC Context

Each FB encapsulates one well-understood ladder pattern, making it testable in isolation and reusable across projects. Together they cover latching, sequencing, mode selection, timing, and I/O mapping — the vocabulary every PLC programmer needs.

## Included Patterns

| FB | Purpose |
|---|---|
| `FbSetReset` | SR latch — Set-dominant bistable |
| `FbResetSet` | RS latch — Reset-dominant bistable |
| `FbSealedinCoil` | Sealed-in coil — self-latching with interlock |
| `FbDebounce` | Input debounce — filters contact chatter |
| `FbFlasher` | Blinking output — configurable ON/OFF times |
| `FbStartStopCircuit` | Classic start/stop with seal |
| `FbMode` | Mode selector — Auto / Manual handoff |
| `FbStep` | Sequential step with condition-based advance |
| `FbMission` | Mission sequencer — ordered step list |
| `FbStateCoilFaultCoil` | State + fault coil pair |
| `FbInputMap` | Maps physical inputs to logical signals |
| `FbFiveRung` | Five-rung safety pattern (IEC-style) |

## UML Diagram

```mermaid
classDiagram
    class FbSetReset {
        +bSet : BOOL
        +bReset : BOOL
        +bOut : BOOL
        +CyclicCall()
    }

    class FbResetSet {
        +bSet : BOOL
        +bReset : BOOL
        +bOut : BOOL
        +CyclicCall()
    }

    class FbSealedinCoil {
        +bStart : BOOL
        +bStop : BOOL
        +bInterlock : BOOL
        +bOut : BOOL
        +CyclicCall()
    }

    class FbDebounce {
        +bInput : BOOL
        +tDebounceTime : TIME
        +bOut : BOOL
        +CyclicCall()
    }

    class FbFlasher {
        +tOnTime : TIME
        +tOffTime : TIME
        +bOut : BOOL
        +CyclicCall()
    }

    class FbMode {
        +bAutoRequest : BOOL
        +bManualRequest : BOOL
        +bInAuto : BOOL
        +bInManual : BOOL
        +CyclicCall()
    }

    class FbStep {
        +bCondition : BOOL
        +nStepId : INT
        +bActive : BOOL
        +CyclicCall()
    }

    class FbMission {
        +nCurrentStep : INT
        +bComplete : BOOL
        +CyclicCall()
    }

    class FbStartStopCircuit {
        +bStart : BOOL
        +bStop : BOOL
        +bRunning : BOOL
        +CyclicCall()
    }

    note for FbSetReset "Foundational latching primitives"
    note for FbMode "Enables Auto/Manual handoff"
    note for FbMission "Sequences FbStep instances"

    FbMission --> FbStep : sequences
    FbSealedinCoil --> FbSetReset : conceptually extends
```
