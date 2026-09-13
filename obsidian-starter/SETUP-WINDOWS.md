# Windows PC + iPhone — a teljes beállítás

Mac nincs, de nem is kell. A Windows gép lesz a "műhely" (itt építesz, itt fut
a Claude Code), az iPhone a "terep" (itt rögzítesz és check-inelsz).

**A sorrend számít.** Előbb az iPhone, aztán a PC — fordítva nem jön létre a
mappa, amit keresel.

---

## 1. lépés — iPhone (5 perc, EZT CSINÁLD ELŐSZÖR)

1. App Store → **Obsidian** telepítés.
2. Indításkor: *Create new vault* → név: **`vault`** →
   **`Store in iCloud` kapcsoló BE.**

Ennyi. Egyelőre ne állíts be semmi mást a telefonon.

Ez a lépés hozza létre az iCloudban az `Obsidian/vault/` mappát. Amíg ez nincs
meg, a Windows gépen hiába keresed — nem létezik.

---

## 2. lépés — Windows (15 perc)

1. **Microsoft Store → iCloud** (az Apple hivatalos appja). Telepítés.
2. Belépés ugyanazzal az Apple ID-vel, mint a telefonon.
3. **iCloud Drive** bekapcsolása. Várd meg az első szinkront.
4. Nyisd meg az Intézőben:
   ```
   C:\Users\<felhasznalonev>\iCloudDrive\Obsidian\vault\
   ```
   Ha az `Obsidian` mappa nincs ott, az 1. lépés nem futott le, vagy még
   szinkronizál. Várj pár percet.
5. **Jobb klikk az `Obsidian` mappán → "Always Keep on This Device"**
   (Mindig tartsa meg ezen az eszközön).

   Ezt ne hagyd ki. Enélkül a Windows csak "helyőrző" fájlokat tart a lemezen,
   és az Obsidian desktop meg a Claude Code üres vagy hiányos fájlokat lát.
   Ez a leggyakoribb hibaforrás ebben a felállásban.
6. **Obsidian desktop** telepítése (obsidian.md) → *Open folder as vault* →
   válaszd a fenti útvonalat.
7. Másold be ide az `obsidian-starter/` tartalmát (a `.gitignore`,
   `README.md` és `SETUP-WINDOWS.md` nélkül).
8. Obsidian → Beállítások (elég egyszer, PC-n, szinkronizál a telefonra):
   - **Files & Links** → *Default location for new notes*: `00_inbox`
   - **Daily notes** (core) → mappa `01_daily`, formátum `YYYY-MM-DD`,
     sablon `_templates/napi.md`
   - **Templates** (core) → sablonmappa `_templates`

Nyisd meg a telefonon. Ott kell lennie mindennek.

---

## 3. lépés — iPhone gyorsrögzítő (5 perc)

Ez a legfontosabb apróság az egész rendszerben. Napközben nem fogsz mappákban
navigálni — egy gombot fogsz megnyomni.

Shortcuts app → új parancs:
- **Text** → *Ask For Input*
- **Append to Text File** → fájl:
  `iCloud Drive / Obsidian / vault / 00_inbox / inbox.md`

Mentsd `Rögzít` néven, tedd ki a kezdőképernyőre (vagy a Vezérlőközpontba).

---

## 4. lépés — Claude Code a vaulton (Windows)

Itt válik a vault passzív jegyzettárból működő támaszrendszerré.

```powershell
cd C:\Users\<felhasznalonev>\iCloudDrive\Obsidian\vault
claude
```

A `CLAUDE.md` már a vault gyökerében van — Claude ebből tudja, hogyan olvassa
a struktúrát, mi a frontmatter-konvenció, és mit nem szabad kivinnie.

Amit innentől tud:
- „Nézd át az inboxot és rendezd el" — a heti áttekintés fele elvégezve
- „Frissítsd a MASTER-t a hét napi jegyzeteiből"
- „Melyik hustle-nél nincs érvényes next_action?"
- „Írd meg a Domino City ajánlatot a korábbi jegyzeteim alapján"

Ezt a második Claude előfizetéseddel futtasd (az üzleti oldallal).

---

## Ha a szinkron akadozik

Őszintén: a Windows + iPhone az a párosítás, ahol az iCloud a leggyengébb.
Működik, de tud késni, és néha összeakad az `.obsidian` konfiguráción.

**Két egyszerű szokás, ami a problémák 90%-át megelőzi:**
1. Ne szerkeszd ugyanazt a fájlt egyszerre a telefonon és a PC-n.
2. Miután PC-n dolgoztál, várj pár másodpercet, mielőtt a telefonon nyitod.

**Ha két héten belül is bosszant** — eltűnő fájlok, `conflicted copy` nevű
másolatok, késő szinkron —, akkor válts **Obsidian Sync**-re. Fizetős,
havidíjas, de ebben a felállásban ez az egyetlen, ami tényleg megbízható,
és verziótörténetet is ad (ez visszahozza a véletlenül törölt jegyzetet).

Ne fizess előre. Előbb derüljön ki, hogy tényleg használod a rendszert.
De ha a vault a napi működésed gerince lesz, ez a pár euró a legjobban
elköltött pénz a listán.

**Amit ne próbálj:** OneDrive, Dropbox, Google Drive. Az Obsidian iOS-en
kizárólag iCloudból vagy saját helyi tárolóból tud vaultot nyitni —
a többi felhő nem játszik, bármit is ígér a saját appja.
