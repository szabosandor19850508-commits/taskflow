# TaskFlow - Architektúra dokumentáció

Ez a mappa tartalmazza a TaskFlow rendszer architekturális döntéseit és diagramjait a C4 modell alapján.

## Architektúra index

* [Architecture Drivers](drivers.md) - A rendszertervezést befolyásoló fő követelmények és korlátok.
* [C4 System Context Diagram](context.md) - A rendszer határa és külső kapcsolatai.
* [C4 Container Diagram](containers.md) - A fő futtatható egységek és adattárolók.
* [Belső Modulok és Szabályok](modules.md) - A backend logikai felépítése és a függőségi szabályok.
* [Dinamikus Nézet (Feladat létrehozása)](dynamic-create-task.md) - A jogosultság és feladatlétrehozás szekvenciája.

## Döntési napló (ADR)
* [ADR-001: Moduláris monolit használata a backendhez](adr/0001-modular-monolith.md)