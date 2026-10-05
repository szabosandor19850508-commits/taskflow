# TaskFlow - Belső modulok és függőségi szabályok

A TaskFlow backend ("Application/API" container) belső, logikai felbontása a következő domén modulokra történik:

## 1. Modulok és felelősségek

*   **Identity & Access**
    *   *Felelősség:* Annak eldöntése, hogy ki a felhasználó, és jogosult-e az adott műveletre.
    *   *Fő függés:* Felhasználó és tagság (membership) adatok.
*   **Projects**
    *   *Felelősség:* Projekt létrehozása, archiválása, és a projekttagság életciklusának kezelése.
    *   *Fő függés:* Identity & Access házirendek (policy).
*   **Tasks**
    *   *Felelősség:* Feladatok létrehozása, módosítása, státuszváltási szabályok kezelése és hozzárendelés (assignment).
    *   *Fő függés:* Projects (tagság ellenőrzése).
*   **Comments**
    *   *Felelősség:* Feladatokhoz kapcsolódó kommunikáció (kommentek létrehozása, listázása).
    *   *Fő függés:* Tasks és jogosultság ellenőrzés.
*   **Notifications**
    *   *Felelősség:* Rendszereseményekből értesítések generálása és továbbítása a külső e-mail szolgáltató felé (adapter).
    *   *Fő függés:* Domén események figyelése.

## 2. Architekturális függőségi szabályok (Dependency Rules)

Ezeket a szabályokat a kódolás során szigorúan be kell tartani:
1.  **Adatbázis elszigeteltsége:** A Web UI kliens nem olvashat és nem írhat közvetlenül az adatbázisba. Minden adatforgalomnak az Application/API-n kell keresztülmennie.
2.  **Központosított jogosultságkezelés:** A logikai modulok (Projects, Tasks, Comments) a jogosultsági és hozzáférési döntéseket minden esetben az `Identity & Access` modultól kell, hogy kérjék, nem kényszeríthetnek ki saját, elszigetelt jogosultsági szabályokat.