# Architecture Drivers

1. **Projekt constraint (Korlát): Kis csapat (2-3 fő) és rövid határidő (14 hét)**
   - *Tervezési jelentőség:* Alacsony operációs komplexitásra és gyors lokális fejlesztésre van szükség, ami indokolja a monolitikus megközelítést.

2. **Security NFR (Biztonság): Privát adatokhoz csak jogosult felhasználó férhet hozzá**
   - *Tervezési jelentőség:* A hozzáférés-ellenőrzés (authorization) egy központi, több funkciót is érintő architekturális felelősség.

3. **Performance NFR (Teljesítmény): API válaszidő p95 < 800 ms (megadott terhelés mellett)**
   - *Tervezési jelentőség:* Befolyásolja a lekérdezések tervezését, az adatbázis indexelést és az API végpontok kialakítását.

4. **Portability NFR (Hordozhatóság): Reprodukálható fejlesztői környezet**
   - *Tervezési jelentőség:* A fő futtatható egységeknek konténerizálhatónak kell lenniük (pl. Docker/Compose), ami megköveteli a tiszta alkalmazáshatárokat.

5. **Maintainability (Karbantarthatóság): Dokumentálható és tanítható rendszer**
   - *Tervezési jelentőség:* Egyszerű, látható modulhatárokra és egyértelmű döntési nyomvonalra (ADR) van szükség a kódbázisban.