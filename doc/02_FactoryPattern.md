# Factory Method

**Category**: Creational  
**Folder**: `DesignPatterns/02_FactoryPattern`  
**Credit**: Kim Robbens

## Intent

Define an interface for creating an object, but let the factory decide which class to instantiate. Clients request objects by type without knowing the concrete class — the factory encapsulates the `__NEW` allocation and returns a typed pointer.

## PLC Context

`FB_ObjectFactory` holds a `CASE` statement keyed on the `E_OBJECTS` enum (`CYLINDER`, `DOOR`, `MOTOR`). It allocates the requested type with `__NEW`, stores it behind a `POINTER TO FB_Object` base pointer, and returns it to the caller. An `ST_ObjectDef` structure carries the type id, instance id, and a release flag so the factory also handles disposal.

## Key Components

| Component | Role |
|---|---|
| `FB_ObjectFactory` | Factory — creates concrete objects via `__NEW` |
| `E_OBJECTS` | Enum — `UNDEFINED`, `CYLINDER`, `DOOR`, `MOTOR` |
| `ST_ObjectDef` | Value object — type + id + release flag |
| `FB_Object` | Abstract base class |
| `FB_Cylinder` | Concrete product |
| `FB_Door` | Concrete product |
| `FB_Motor` | Concrete product |

## UML Diagram

```mermaid
classDiagram
    class FB_ObjectFactory {
        +Create(def : ST_ObjectDef) POINTER TO FB_Object
        +Release(pObj : POINTER TO FB_Object)
    }

    class ST_ObjectDef {
        +eType : E_OBJECTS
        +nId : INT
        +bRelease : BOOL
    }

    class E_OBJECTS {
        <<enumeration>>
        UNDEFINED
        CYLINDER
        DOOR
        MOTOR
    }

    class FB_Object {
        <<abstract>>
        +nId : INT
        +CyclicCall()
    }

    class FB_Cylinder {
        +CyclicCall()
    }

    class FB_Door {
        +CyclicCall()
    }

    class FB_Motor {
        +CyclicCall()
    }

    FB_Object <|-- FB_Cylinder
    FB_Object <|-- FB_Door
    FB_Object <|-- FB_Motor

    FB_ObjectFactory ..> FB_Cylinder : creates
    FB_ObjectFactory ..> FB_Door : creates
    FB_ObjectFactory ..> FB_Motor : creates
    FB_ObjectFactory --> ST_ObjectDef : uses
    ST_ObjectDef --> E_OBJECTS : typed by
```
