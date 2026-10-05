# ADR-001: Use a modular monolith for the TaskFlow backend

**Status:** Proposed
**Date:** 2026-10-05

## Context
A projekt architecture driverei alapján a csapat mérete kicsi (2-3 fő), és a fejlesztésre rendelkezésre álló idő rövid (14 hetes kurzus). Alapvető elvárás az egyszerű lokális futtathatóság (reprodukálható dev környezet) és az alacsony operációs komplexitás. Ugyanakkor a projekt oktatási célja, hogy a domén modulhatárait jól láthatóvá tegyük.

## Considered options
1. Egyszerű réteges monolit (Layered monolith)
2. Moduláris monolit (Modular monolith)
3. Független szolgáltatások (Microservices)

### Alternatívák összehasonlítása (Trade-offs)
| Szempont | Egyszerű monolit | Moduláris monolit | Független szolgáltatások |
| :--- | :--- | :--- | :--- |
| **Team size** | Megfelelő kis csapatnak. | Jó kompromisszum kis csapatnak. | Túl nagy teher (overhead) 2-3 főre. |
| **Deploy complexity** | Egyetlen deployolható egység (egyszerű). | Egyetlen deployolható egység (egyszerű). | Sok mozgó alkatrész (CI/CD bonyolult). |
| **Data consistency** | Egyszerű tranzakciók. | Egyszerű tranzakciók, de védett határok. | Elosztott tranzakciók (nagyon bonyolult). |
| **Scaling** | Csak egészben skálázható. | Csak egészben skálázható. | Modulonként függetlenül skálázható. |
| **Observability** | Alacsony üzemeltetési költség. | Alacsony üzemeltetési költség. | Magas költség (elosztott loggolás kell). |

## Decision
A TaskFlow backendet a félév során **moduláris monolitként** (Modular monolith) építjük fel.

## Consequences
**Pozitív következmények (+):**
* Egyszerűbb fejlesztés és telepítés (egy deployolható egység).
* Közös tranzakciókezelés lehetséges az adatbázisban, elkerülve az elosztott rendszerek bonyolultságát.
* A domén modulok felelősségei jól modellezhetők és láthatók maradnak.

**Negatív következmények (-):**
* Nincs lehetőség a modulok független telepítésére (deploy) vagy skálázására.
* A belső modulhatárokat nem védi hálózati réteg, így azokat a kódban (függőségi szabályok) és a kód felülvizsgálatok (code review) során szigorúan védeni kell a degradáció ellen.

## Revisit trigger
Ha a rendszer terhelése a jövőben megnő, és egy adott modul (pl. Notifications) önálló, a többitől eltérő skálázási vagy telepítési igénye mérhetően megjelenik, ezt a döntést egy új ADR-ben újraértékeljük.