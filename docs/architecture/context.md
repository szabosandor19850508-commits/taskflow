# TaskFlow - C4 System Context diagram

```mermaid
graph TD
    %% Szereplők (Sötétkék)
    User1(["Projekt tag<br/>[Person]<br/>Feladatokat hoz létre, frissít, kommentel és követ."])
    User2(["Projektadminisztrátor<br/>[Person]<br/>Projektet, tagságot és jogosultságokat kezel."])

    %% Rendszer (Kék)
    System["TaskFlow<br/>[Software System]<br/>Kis csapatok projekt- és feladatkezelő rendszere."]

    %% Külső rendszer (Szürke)
    ExtSystem["E-mail szolgáltatás<br/>[External System]<br/>A TaskFlow kérésére e-mailt kézbesít."]

    %% Kapcsolatok (Nyilak)
    User1 -- "kezeli a projekteket és feladatokat" --> System
    User2 -- "tagságot és projektet kezel" --> System
    System -- "értesítési e-mailt küld" --> ExtSystem

    %% C4 Stílusok alkalmazása
    style System fill:#1168bd,color:#fff,stroke:#0b4884,stroke-width:2px
    style ExtSystem fill:#999999,color:#fff,stroke:#666666,stroke-width:2px
    style User1 fill:#08427b,color:#fff,stroke:#052e56,stroke-width:2px
    style User2 fill:#08427b,color:#fff,stroke:#052e56,stroke-width:2px