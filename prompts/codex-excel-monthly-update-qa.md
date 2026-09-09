# Codex prompt — Havi/negyedéves Excel riport frissítés + automatikus hibaellenőrzés

> Másold be az alábbi blokkot a ChatGPT Codexbe. A `<<< >>>` jelölt helyeket töltsd ki
> a saját fájlneveiddel / hónapokkal, mielőtt elküldöd.

---

## PROMPT

Egy Excel-alapú havi értékesítési riport frissítésének minőségellenőrzését és
automatizálását kell megoldanod. A cél nem egyszeri javítás, hanem egy
**újrafuttatható, determinisztikus folyamat**, amit minden hónap/negyedév végén
le lehet futtatni.

### Bemenetek
- `<<<riport.xlsx>>>` — a frissítendő (vagy már frissített, de gyanús) munkafüzet.
- `<<<előző_havi_riport.xlsx>>>` — a legutóbbi, jóváhagyott állapot (referencia).
- Forrásfájlok: `<<<Sales_EUR.xlsx>>>`, `<<<Bags.xlsx>>>`, opcionálisan
  `<<<Marketing.xlsx>>>`, `<<<P&L.xlsx>>>`.
- Új időszak: `<<<2026-09>>>`.

### Környezet és megkötések
- Python 3, `openpyxl` (formázás, képletek, diagramok megtartásához) + `pandas`
  (adat-összevetéshez). LibreOffice CLI használható a képletek újraszámolásához
  (`soffice --headless --convert-to xlsx`), ha kell tényleges cellaértékeket olvasni.
- **Soha ne írd felül az eredeti fájlt.** Mindig új verziót ments
  (`<<<riport>>>_<<<YYYY-MM>>>_v2.xlsx`), az eredetit hagyd érintetlenül.
- A munkafüzet meglévő szerkezetét, stílusait, diagramjait meg kell őrizni:
  ne generálj új fájlt nulláról, a meglévőt módosítsd.
- Minden módosítás legyen kódban leírva és megismételhető — kézi, egyszeri
  cellaszerkesztés nem elfogadható.

### 1. feladat — Auditáló szkript (`audit_report.py`)
Írj egy szkriptet, ami a munkafüzetet végigellenőrzi és **strukturált hibalistát**
ad vissza (konzolra táblázatosan + `audit_<<<YYYY-MM>>>.xlsx` / `.md` riportba),
minden találatnál: `fül | cella/tartomány | hiba típusa | jelenlegi érték | elvárt érték | súlyosság`.

Ellenőrzendő pontok:

1. **Termékek teljessége**
   - Minden termék, ami az előző időszaki riportban vagy a forrásadatokban szerepel,
     jelen van-e az új riportban is (és fordítva: nincs-e nem odavaló sor).
   - Külön figyelj a korábban problémás vevőkre/termékekre: **Amica**, **Sollar** —
     ezekre tételes összevetést kérek a forrásból.
   - Sor- és oszlopeltolódás detektálása az előző verzióhoz képest.

2. **Marketing / Freight költségek**
   - Ahol van ilyen költség, a **megfelelő vevőhöz** van-e rendelve.
   - Helyes-e a KPI-bontás és a levonás iránya/előjele (a költség csökkentse az eredményt).
   - Vevőnkénti Marketing/Freight összeg egyezik-e a forrásfájl összegével (±0,01).

3. **Képletek**
   - Nincs-e `#VALUE!`, `#REF!`, `#DIV/0!`, `#N/A`, `#NAME?`, `#NULL!`, `#NUM!`.
   - Minden képlet a **helyes tartományra** hivatkozik-e: az új hónap oszlopa/sora
     bele van-e véve a SUM/AVERAGE/SUMIFS tartományokba (klasszikus hiba: a tartomány
     nem bővült az új időszakkal).
   - Nincs-e hardcode-olt szám ott, ahol képletnek kellene lennie (a szám "jól néz ki",
     de nem számolt érték) — jelezd az előző verzióhoz képest képletből konstanssá
     vált cellákat.
   - Nincsenek-e külső, törött hivatkozások vagy más fájlra mutató linkek.
   - A képletek maradjanak egyszerűek és követhetők; ha egy képlet feleslegesen
     bonyolult, javasolj egyszerűbb, azonos eredményt adó változatot.

4. **Diagramok**
   - Minden diagramnak van-e adata (nem üres a series).
   - A series tartománya lefedi-e az új hónapot.
   - **EUR és Bags nem keveredhet** egy diagramon / egy tengelyen — jelezd, ha egy
     diagram vegyes mértékegységű series-t tartalmaz, vagy ha a cím/tengelyfelirat
     nem egyezik a hivatkozott adat mértékegységével.
   - A hivatkozott tartomány nem lóg-e ki a tényleges adatterületen túlra.

5. **Színezés**
   - Szabály: **maga a szám legyen piros/zöld (betűszín), NEM a cella háttérszíne.**
     Negatív érték → piros betű, pozitív → zöld betű.
   - Jelezz minden cellát, ahol a szabályt háttérszínnel oldották meg, ahol az előjel
     és a szín nem egyezik, illetve ahol hiányzik a színezés.
   - Ellenőrizd a feltételes formázási szabályokat is, ne csak a statikus formázást.

6. **Formázás / olvashatóság**
   - Sormagasság és oszlopszélesség: nincs-e levágott vagy `#####` tartalom
     (számold ki a szükséges szélességet a leghosszabb megjelenített értékből).
   - Tördelés (wrap text), egyesített cellák konzisztenciája.
   - Ezres tagolás és tizedesjegyek egységesek-e azonos típusú mezőkben
     (EUR: `#,##0`; Bags: `#,##0`; %: `0.0%` — vagy ami a fájlban a bevett minta).
   - Fejlécek megléte, rögzített ablaktábla (freeze panes), igazítás (szám jobbra,
     szöveg balra) — az előző verzió mintája szerint.

7. **Fülek és struktúra**
   - Ugyanazok a fülek, **ugyanabban a sorrendben**, mint az előző verzióban.
   - Amihez az új időszak miatt nem kell hozzányúlni, az **byte-szinten változatlan**
     maradjon — készíts diffet az előző verzióhoz és listázd a nem várt változásokat.
   - Rejtett fülek/sorok/oszlopok, elnevezett tartományok változatlansága.

8. **Keresztellenőrzés a fülek között**
   - `Executive Dashboard ↔ Product Insight ↔ KPI ↔ Monthly` — ugyanazon alapadatból
     ugyanaz az eredmény jöjjön ki minden fülön.
   - Vess össze minden közös metrikát (árbevétel EUR, mennyiség Bags, marzs, KPI-k)
     vevő/termék/hónap bontásban; tűréshatár ±0,01 (kerekítésből eredő eltérés).
   - Az eltéréseket tételesen listázd, ne csak összesítve.

9. **Forrásellenőrzés**
   - Végül minden aggregált szám vezessen vissza az eredeti **Sales EUR** és **Bags**
     forrásra, szükség esetén a **Marketing / P&L** forrásra.
   - Készíts egyeztető (reconciliation) táblát: forrás összeg | riport összeg | eltérés.

### 2. feladat — Javító szkript (`fix_report.py`)
Az audit találatai alapján javítsd a munkafüzetet, kizárólag ott, ahol a javítás
egyértelmű és determinisztikus (tartomány kiterjesztése az új hónapra, betűszín
szabály alkalmazása, oszlopszélesség, számformátum, fülsorrend, hiányzó termék
felvétele a forrásból). Minden javítás:
- legyen naplózva (`fixes_<<<YYYY-MM>>>.md`: mit, hol, miért, előtte→utána),
- legyen visszavonható (az eredeti fájl érintetlen marad),
- **ne** találgasson: ha egy eltérés üzleti döntést igényel, azt NE javítsd, hanem
  tedd külön "manuális döntést igénylő" listára, javaslattal együtt.

### 3. feladat — Regressziós ellenőrzés
A javítás után **futtasd újra az auditot** a javított fájlon, és mutasd meg, hogy
minden automatikusan javított hiba eltűnt, és nem keletkezett új. A végén adj egy
rövid összefoglalót: hány hiba volt kategóriánként, hány javult, mi maradt kézire.

### 4. feladat — Újrahasználhatóság
- Tedd a beállításokat (fülnevek, oszlopnevek, tűréshatárok, várt fülsorrend,
  számformátumok, kulcsvevők listája) külön `config.yaml` fájlba, hogy a következő
  hónapban csak a dátumot és a fájlneveket kelljen átírni.
- Egyetlen belépési pont: `python run_monthly_check.py --month <<<2026-09>>> --config config.yaml`.
- Írj rövid `README.md`-t: mit futtat, milyen kimenetet ad, mit kell havonta átállítani.
- Írj unit teszteket a kritikus ellenőrzőkre (szintetikus mini-xlsx fixture-ökkel):
  tartománykiterjesztés, EUR/Bags keveredés, betűszín vs. háttérszín, kereszt-egyezés.

### Elvárt kimenet
1. A szkriptek (`audit_report.py`, `fix_report.py`, `run_monthly_check.py`, `config.yaml`, tesztek).
2. `audit_<<<YYYY-MM>>>.md` — a talált hibák tételes listája fül/cella szinten.
3. A javított munkafüzet új néven + `fixes_<<<YYYY-MM>>>.md` változásnapló.
4. "Manuális döntést igénylő" lista, javaslatokkal.
5. Rövid összefoglaló arról, mely hibatípusokat érdemes a jövőben már a riport
   felépítésében (pl. dinamikus tartományok, táblázatok, elnevezett tartományok)
   megelőzni, hogy a negyedéves frissítés gyorsabb legyen.

### Munkamódszer
Kérdezz vissza, ha egy fülnév, oszlopnév vagy üzleti szabály nem egyértelmű a
fájlokból. Ne találgass üzleti logikát. Először derítsd fel a munkafüzet
szerkezetét (fülek, tartományok, képletminták) és mutasd meg, mit találtál, csak
utána kezdd az ellenőrzők írását.
