# TC1200 — OOP Design Patterns for TwinCAT 3 PLC

Implementations of the [Gang of Four (GoF) Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns) in TwinCAT 3 Structured Text (IEC 61131-3). Each subproject demonstrates one pattern using realistic industrial-automation examples and TwinCAT 3 OOP features (interfaces, inheritance, `IMPLEMENTS`, `__NEW`).

---

## Creational Patterns

> Deal with object creation — how objects are created, composed, and represented.

| # | Pattern | Folder | Quick description | Doc |
|---|---------|--------|-------------------|-----|
| 00 | Abstract Factory | `DesignPatterns/00_AbstractFactory` | Create families of loggers (file / database) without coupling the client to concrete types | [doc](doc/00_AbstractFactory.md) |
| 01 | Builder | `DesignPatterns/01_Builder` | Assemble a complex product step-by-step via a Director that drives an ITF_Builder | [doc](doc/01_Builder.md) |
| 02 | Factory Method | `DesignPatterns/02_FactoryPattern` | Allocate Cylinder / Door / Motor objects by enum type using `__NEW` inside a factory FB | [doc](doc/02_FactoryPattern.md) |
| 04 | Singleton by Proxy | `DesignPatterns/04_SingletonByProxy` | Guarantee a single MessageLogger instance; callers access it only through an interface proxy | [doc](doc/04_SingletonByProxy.md) |

---

## Structural Patterns

> Deal with object composition — how classes and objects are combined to form larger structures.

| # | Pattern | Folder | Quick description | Doc |
|---|---------|--------|-------------------|-----|
| 10 | Adapter | `DesignPatterns/10_Adapter` | Wrap a Festo VTEM valve's proprietary API behind a standard ICylinder interface | [doc](doc/10_Adapter.md) |
| 12 | Composite | `DesignPatterns/12_Composite` | Model a Machine → SubMachine → Component tree; traverse status uniformly via IComposite | [doc](doc/12_Composite.md) |
| 13 | Decorator | `DesignPatterns/13_Decorator` | Add fluent method-chaining to a plain string buffer via a StringBuilder decorator FB | [doc](doc/13_Decorator.md) |
| 14 | Facade | `DesignPatterns/14_Facade` | Hide MC_Power / MC_Reset / MC_Halt complexity behind a simple MC_Axis facade | [doc](doc/14_Facade.md) |
| 16 | Proxy | `DesignPatterns/16_Proxy` | Gate access to sensitive data behind a password-checking proxy that shares the subject interface | [doc](doc/16_Proxy.md) |

---

## Behavioral Patterns

> Deal with communication between objects — algorithms and assignment of responsibilities.

| # | Pattern | Folder | Quick description | Doc |
|---|---------|--------|-------------------|-----|
| 20 | Chain of Responsibility | `DesignPatterns/20_ChainOfResponsibility` | Route a request through a linked handler chain; each handler processes or forwards | [doc](doc/20_ChainOfResponsibility.md) |
| 21 | Command | `DesignPatterns/21_Command` | Encapsulate Light/Gate actions as command objects wired to a 10-button panel invoker | [doc](doc/21_Command.md) |
| 23 | Iterator | `DesignPatterns/23_Iterator` | Traverse a NotificationCollection sequentially without exposing its internal array | [doc](doc/23_Iterator.md) |
| 24 | Mediator | `DesignPatterns/24_Mediator` | Route all chat messages through a central mediator so colleagues never reference each other | [doc](doc/24_Mediator.md) |
| 25 | Memento | `DesignPatterns/25_Memento` | Snapshot and restore RecipeEditor state without breaking encapsulation | [doc](doc/25_Memento.md) |
| 26 | Observer | `DesignPatterns/26_Observer` | Demonstrate both inheritance-based and composition-based publishers notifying subscriber FBs | [doc](doc/26_Observer.md) |
| 27 | State | `DesignPatterns/27_State` | Model an ATM machine whose behaviour (Off / SelfTest / Idle / ServingCustomer …) changes with state | [doc](doc/27_State.md) |
| 28 | Strategy | `DesignPatterns/28_Strategy` | Swap PT100 / PT1000 temperature-sensor algorithms inside a motor FB at runtime | [doc](doc/28_Strategy.md) |
| 29 | Template Method | `DesignPatterns/29_TemplateMethod` | Define a makePizza() skeleton in FB_Pizza; subclasses override only their topping step | [doc](doc/29_TemplateMethod.md) |
| 30 | Visitor | `DesignPatterns/30_Visitor` | Apply SysLog or XML export operations to Heater / Conveyor / IPC modules without modifying them | [doc](doc/30_Visitor.md) |

---

## Auxiliary

| # | Pattern | Folder | Quick description | Doc |
|---|---------|--------|-------------------|-----|
| 100 | Ladder Logic Patterns | `DesignPatterns/100_PatternsOfLadderLogicProgramming` | Foundational PLC building blocks: SR latch, debounce, flasher, start/stop, mode, step, mission sequencer | [doc](doc/100_LadderLogicPatterns.md) |

---

## Credits / Licenses

Parts of the implemented code are:

| Pattern | Author | License |
|---------|--------|---------|
| Decorator | [TcOpenGroup](https://github.com/TcOpenGroup/TcOpen) | Included |
| Chain of Responsibility | [0w8states](https://github.com/0w8States/PLC-Design-Patterns) | Included |
| Iterator | 0w8states | Included |
| Mediator | 0w8states | Included |
| Memento | 0w8states | Included |
| State | 0w8states | Included |
| Template Method | 0w8states | Included |
| Visitor | 0w8states | Included |
| Proxy | Armando Rene Narvaez Contreras → Alliazzz (CODESYS) → Kim Robbens (TwinCAT 3) | The Unlicense |
| Builder | Armando Rene Narvaez Contreras → Alliazzz (CODESYS) → Kim Robbens (TwinCAT 3) | The Unlicense |
| Command | Kim Robbens | Included |
| Observer | Kim Robbens | Included |
| Strategy | Kim Robbens | Included |
| Singleton by Proxy | Kim Robbens | Included |
| Abstract Factory | [Stephen Henneken](https://stefanhenneken.wordpress.com/2014/11/16/iec-61131-6-abstract-factory-english/) | Included |
| Ladder Logic Patterns | [Scott Whitlock](http://www.contactandcoil.com/patterns-of-ladder-logic-programming/) | The Unlicense |
| Factory Method | Kim Robbens | Included |
| Adapter | Kim Robbens | Included |
| Facade | Kim Robbens | Included |

If any license is violated, please open an issue and it will be corrected promptly.
