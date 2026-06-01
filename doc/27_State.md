# State

**Category**: Behavioral  
**Folder**: `DesignPatterns/27_State`  
**Credit**: 0w8states

## Intent

Allow an object to alter its behaviour when its internal state changes. The object will appear to change its class.

## PLC Context

`FB_ATM_Machine` models a bank ATM. Each operating mode is a separate function block (`FB_Off`, `FB_SelfTest`, `FB_Maintenance`, `FB_OutOfService`, `FB_Idle`, `FB_ServingCustomer`) that implements `I_State`. The context holds a reference to the current state and delegates all button/sensor events to it. States are responsible for transitioning the context to the next state — no giant CASE statement required.

## Key Components

| Component | Role |
|---|---|
| `I_State` | State interface — `Description` property, event handlers |
| `FB_ATM_Machine` | Context — delegates to current `I_State` |
| `FB_Off` | State — powered off |
| `FB_SelfTest` | State — startup self-test |
| `FB_Maintenance` | State — maintenance mode |
| `FB_OutOfService` | State — out of service |
| `FB_Idle` | State — waiting for customer |
| `FB_ServingCustomer` | State — transaction in progress |
| `E_StateDescription` | Enum — state identifiers |

## UML Diagram

```mermaid
classDiagram
    class I_State {
        <<interface>>
        +Description : E_StateDescription
        +OnPowerOn(ctx : FB_ATM_Machine)
        +OnPowerOff(ctx : FB_ATM_Machine)
        +OnCardInserted(ctx : FB_ATM_Machine)
        +OnCardRemoved(ctx : FB_ATM_Machine)
    }

    class E_StateDescription {
        <<enumeration>>
        OFF
        SELF_TEST
        MAINTENANCE
        OUT_OF_SERVICE
        IDLE
        SERVING_CUSTOMER
    }

    class FB_ATM_Machine {
        -_state : I_State
        +setState(state : I_State)
        +OnPowerOn()
        +OnPowerOff()
        +OnCardInserted()
        +OnCardRemoved()
    }

    class FB_Off {
        +Description : E_StateDescription
        +OnPowerOn(ctx : FB_ATM_Machine)
    }

    class FB_SelfTest {
        +Description : E_StateDescription
        +OnPowerOff(ctx : FB_ATM_Machine)
    }

    class FB_Idle {
        +Description : E_StateDescription
        +OnCardInserted(ctx : FB_ATM_Machine)
        +OnPowerOff(ctx : FB_ATM_Machine)
    }

    class FB_ServingCustomer {
        +Description : E_StateDescription
        +OnCardRemoved(ctx : FB_ATM_Machine)
    }

    class FB_Maintenance {
        +Description : E_StateDescription
    }

    class FB_OutOfService {
        +Description : E_StateDescription
    }

    I_State <|.. FB_Off
    I_State <|.. FB_SelfTest
    I_State <|.. FB_Idle
    I_State <|.. FB_ServingCustomer
    I_State <|.. FB_Maintenance
    I_State <|.. FB_OutOfService

    FB_ATM_Machine --> I_State : delegates to current
    I_State --> E_StateDescription : identifies as
```
