# Singleton by Proxy

**Category**: Creational  
**Folder**: `DesignPatterns/04_SingletonByProxy`  
**Credit**: Kim Robbens

## Intent

Guarantee that a class has only one instance and provide a controlled access point to it. The "by proxy" variant wraps the singleton behind a proxy so callers never hold a direct reference to the underlying object — they always go through the proxy, which enforces the single-instance invariant.

## PLC Context

`Singleton` is a base FB with `fb_init` / `Construct` lifecycle methods. `MessageLoggerSingleton` extends it and implements `I_MessageLogger`. Callers receive an `I_Singleton` reference and retrieve the logger through `I_MessageLogger`, never touching the concrete type directly.

## Key Components

| Component | Role |
|---|---|
| `I_Singleton` | Interface — lifecycle contract for singleton pattern |
| `I_MessageLogger` | Interface — product service contract |
| `Singleton` | Base FB — single-instance enforcement logic |
| `MessageLoggerSingleton` | Concrete singleton — implements `I_MessageLogger` |
| `MessageLogger` | The actual logging service wrapped by the singleton |
| `MySingleton` | Demo program / client |

## UML Diagram

```mermaid
classDiagram
    class I_Singleton {
        <<interface>>
        +Construct()
    }

    class I_MessageLogger {
        <<interface>>
        +Log(sMessage : STRING)
    }

    class Singleton {
        #_bConstructed : BOOL
        +Construct()
        +fb_init()
    }

    class MessageLoggerSingleton {
        -_logger : MessageLogger
        +Construct()
        +Log(sMessage : STRING)
    }

    class MessageLogger {
        +Log(sMessage : STRING)
    }

    class MySingleton {
        -_instance : I_Singleton
        +Run()
    }

    I_Singleton <|.. Singleton
    Singleton <|-- MessageLoggerSingleton
    I_MessageLogger <|.. MessageLoggerSingleton
    MessageLoggerSingleton --> MessageLogger : delegates to
    MySingleton --> I_Singleton : accesses via
    MySingleton --> I_MessageLogger : uses
```
