# TaskFlow - Feladat létrehozása (Dinamikus nézet)

```mermaid
sequenceDiagram
    autonumber
    actor User as Projekt tag
    participant UI as Web UI
    participant API as Application / API
    participant Auth as Identity & Access
    participant Tasks as Tasks Module
    participant DB as Database

    User->>UI: Új feladat mentése
    UI->>API: POST /projects/{id}/tasks
    
    API->>Auth: Tag-e a projektben? (Jogosultság ellenőrzése)
    
    alt Jogosulatlan felhasználó (Hiba ág)
        Auth-->>API: Nem (Jogosulatlan)
        API-->>UI: 403 Forbidden (Hiba)
        UI-->>User: Hibaüzenet megjelenítése a felületen
    else Jogosult felhasználó (Sikeres ág)
        Auth-->>API: Igen (Jogosult)
        API->>Tasks: Adatok validálása és létrehozás
        Tasks->>DB: INSERT task (Új rekord mentése)
        DB-->>Tasks: Generált Task ID
        Tasks-->>API: Létrehozott feladat adatai
        API-->>UI: 201 Created + Task adatok
        UI-->>User: Új feladat megjelenítése a listában
    end