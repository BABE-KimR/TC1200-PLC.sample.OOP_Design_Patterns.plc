# Composite

**Category**: Structural  
**Folder**: `DesignPatterns/12_Composite`  
**Credit**: Kim Robbens

## Intent

Compose objects into tree structures to represent part–whole hierarchies. Clients treat individual objects and compositions uniformly through a common interface.

## PLC Context

An automation system has a `Machine` that contains sub-machines (`SubMachine1`, `SubMachine2`), which in turn contain leaf `Component` objects. Every node implements `IComposite` so that operations like `getStatus()` and `logStatus()` recurse naturally through the tree without the client needing to know the depth.

## Key Components

| Component | Role |
|---|---|
| `IComposite` | Common interface — `getChild()`, `getName()`, `getStatus()`, `logStatus()` |
| `Machine` | Composite node — holds an array of `IComposite` children |
| `SubMachine1`, `SubMachine2` | Intermediate composite nodes |
| `Component` | Leaf — no children, implements `IComposite` directly |
| `E_Status` | Enum — `OK`, `WARNING`, `ERROR` |

## UML Diagram

```mermaid
classDiagram
    class IComposite {
        <<interface>>
        +getChild(nIndex : INT) IComposite
        +getName() STRING
        +getStatus() E_Status
        +logStatus()
    }

    class E_Status {
        <<enumeration>>
        OK
        WARNING
        ERROR
    }

    class Machine {
        -_children : ARRAY OF IComposite
        -_name : STRING
        +getChild(nIndex : INT) IComposite
        +getName() STRING
        +getStatus() E_Status
        +logStatus()
        +addChild(child : IComposite)
    }

    class SubMachine1 {
        -_children : ARRAY OF IComposite
        +getChild(nIndex : INT) IComposite
        +getName() STRING
        +getStatus() E_Status
        +logStatus()
    }

    class SubMachine2 {
        -_children : ARRAY OF IComposite
        +getChild(nIndex : INT) IComposite
        +getName() STRING
        +getStatus() E_Status
        +logStatus()
    }

    class Component {
        -_name : STRING
        -_status : E_Status
        +getChild(nIndex : INT) IComposite
        +getName() STRING
        +getStatus() E_Status
        +logStatus()
    }

    IComposite <|.. Machine
    IComposite <|.. SubMachine1
    IComposite <|.. SubMachine2
    IComposite <|.. Component

    Machine o-- IComposite : children
    SubMachine1 o-- IComposite : children
    SubMachine2 o-- IComposite : children
    IComposite --> E_Status : returns
```
