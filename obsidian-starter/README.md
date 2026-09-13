# Induló vault — személyes operációs rendszer

Telefon-központú Obsidian vault főmunkához, side hustle-ökhöz, projektekhez és
felépüléshez, úgy felépítve, hogy Claude mindig képben legyen.

---

## 1. Telepítés

**iPhone + Windows PC:** a teljes, lépésenkénti leírás a
[`SETUP-WINDOWS.md`](SETUP-WINDOWS.md)-ben van. Ott a sorrend számít
(előbb iPhone, utána PC), ezért azt kövesd, ne ezt a rövid változatot.

**Csak iPhone (vagy Mac is van):**

1. **Obsidian** letöltése az App Store-ból.
2. Első indításnál: *Create new vault* → név: `vault` → **`Store in iCloud` BE**.
   (Ez a kapcsoló később nem állítható át fájdalommentesen. Most kapcsold be.)
3. Másold be ennek a mappának a tartalmát a vaultba — Files app →
   iCloud Drive → Obsidian → vault. A `.gitignore`, `README.md` és
   `SETUP-WINDOWS.md` nem kell át, a többi igen.
4. Obsidian → Beállítások:
   - **Files & Links** → *Default location for new notes*: `00_inbox`
   - **Daily notes** (core plugin, kapcsold be) → mappa: `01_daily`,
     dátumformátum: `YYYY-MM-DD`, sablon: `_templates/napi.md`
   - **Templates** (core plugin) → sablonmappa: `_templates`
5. **Mobil eszköztár**: Beállítások → Appearance → *Manage toolbar options*.
   Tedd legelőre: checkbox, sablonbeszúrás, napi jegyzet.
6. **iOS Shortcut** (ez a legfontosabb lépés az egészben):
   Shortcuts app → új parancs → *Append to Text File* →
   fájl: `iCloud Drive/Obsidian/vault/00_inbox/inbox.md`, szöveg: *Ask for input*.
   Tedd ki a kezdőképernyőre. **Ez a gyorsrögzítő.**

Plugin ennyi. Mobilon minden további plugin csak lassít.

---

## 2. Hogyan működik

Négy réteg, kívülről befelé:

```
gyorsrögzítés  ->  napi jegyzet  ->  heti áttekintés  ->  MASTER  ->  Claude
  (0 másodperc)     (2 perc)          (20 perc/hét)      (a kép)
```

- **`00_inbox/`** — ide esik minden, gondolkodás nélkül. Rendetlen. Ez rendben van.
- **`01_daily/`** — napi jegyzet a sablonnal. Nyers napló, nem dokumentáció.
- **`02_context/`** — a kurált kép. Ez az, amit Claude kap.
- **`00_MASTER.md`** — egyetlen fájl, 1-2 oldal, ami elmondja, hol tartasz.

**A rendszer szíve a heti áttekintés.** Vasárnap 20 perc: inbox üresre,
aktívak átnézése, MASTER frissítése, feltöltés a Claude Projectbe.
Ha ezt elhagyod, három hét múlva a vault egy digitális fiókos szekrény lesz,
amiben semmit nem találsz. Sablon: `_templates/heti-review.md`.

---

## 3. Első feltöltés — a `02_context/` kitöltése

Másold át a `_templates/context-*.md` fájlokat a `02_context/` mappába,
és nevezd át őket:

| Sablon | Új név | Mire jó |
|---|---|---|
| `context-master.md` | `00_MASTER.md` | A teljes kép. Ezt töltöd fel Claude-nak. |
| `context-scoreboard.md` | `scoreboard.md` | A számok. Korai és késői jelzők. |
| `context-dontesek.md` | `dontesek.md` | Döntési napló. |
| `context-tokeallokacio.md` | `tokeallokacio.md` | Hová megy az idő és a pénz. |
| `context-nem-csinalom.md` | `nem-csinalom.md` | Amire tudatosan nemet mondtál. |
| `context-celok.md` | `celok.md` | 12 hónap / 90 nap / ez a hónap. |
| `context-penzugyek.md` | `penzugyek.md` | Enélkül minden üzleti tanács vakrepülés. |
| `context-rolam.md` | `rolam.md` | Hogyan működsz. Egyszer kitöltöd. |
| `context-felepules.md` | `felepules.md` | **Privát.** Csak a személyes coach Projectbe. |

## 3/b. A ritmus

Ez tartja életben az egészet. A mappák önmagukban nem érnek semmit.

| Mikor | Mennyi | Mit | Sablon |
|---|---|---|---|
| naponta | 3 perc | napi jegyzet, 3 prioritás | `napi.md` |
| hetente | 20 perc | inbox nullára, pipeline, MASTER frissítés | `heti-review.md` |
| havonta | 60 perc | scoreboard, minden aktív átnézése | `havi-review.md` |
| negyedévente | fél nap | tőkeallokáció, rátesz/tartja/kivezet | `negyedeves-review.md` |

A negyedéves a legfontosabb, és azt szokás leghamarabb lemondani.
A heti és a havi arról szól, hogy jól csinálod-e. A negyedéves arról,
hogy a jó dolgot csinálod-e.

---|---|---|
| `context-master.md` | `00_MASTER.md` | A teljes kép. Ezt töltöd fel Claude-nak. |
| `context-rolam.md` | `rolam.md` | Hogyan működsz. Egyszer kitöltöd, ritkán változik. |
| `context-celok.md` | `celok.md` | 12 hónap / 90 nap / ez a hónap. |
| `context-penzugyek.md` | `penzugyek.md` | Enélkül minden hustle-tanács vakrepülés. |
| `context-felepules.md` | `felepules.md` | **Privát.** Csak a személyes coach Projectbe. |

---

## 4. Két Claude előfizetés — így oszd szét

Két fiók = tiszta határvonal érzékeny és nem érzékeny között.
Ne keverd őket.

**Fiók A — személyes**
- Project: **Coach** — rendszerprompt: a felépülés-coach prompt.
  Knowledge: `felepules.md`, `rolam.md`, `celok.md`, `00_MASTER.md`.
  Ide jönnek a napi check-inek.

**Fiók B — üzlet**
- Project: **Üzlet** — Knowledge: `00_MASTER.md` (a felépülés-blokk nélkül),
  `celok.md`, `penzugyek.md`, az aktív hustle-ök `index.md`-jei.
  Ide jön a stratégia, árazás, szövegírás, döntések.
- Project: **Popz** — a főmunka. Knowledge: `03_work_popz/` releváns része.

A felépülési adat **soha nem megy a B fiókba**.

Ha van géped, a B fiókkal futtass **Claude Code-ot a vault mappájában** —
a `CLAUDE.md` már készen áll rá. Ott Claude az egész vaultot látja, keres,
átszervez, frissíti a MASTER-t.

---

## 5. A négy szabály, ami eldönti, működik-e

1. **Rögzíts azonnal, rendezz később.** Az inbox azért van, hogy ne kelljen
   gondolkodnod rögzítéskor.
2. **Minden `active` dolognak pontosan egy `next_action`-je van.**
   Ha nincs, nem aktív — csak nyugtalanít.
3. **Maximum 2 aktív hustle.** Főmunka + felépülés mellett a harmadik nem
   gyorsít, hanem mindhármat megöli. A többi `paused` vagy `idea`.
4. **Heti áttekintés vasárnap.** Egy kihagyott hét belefér. Három nem.

---

## 6. Adatvédelem

A vault egészségügyi adatot fog tartalmazni.

- Ez a repo **publikus**. A vault tartalma **soha nem kerül ide** —
  a `.gitignore` ezt ki is zárja.
- Ha egyszer verziózni akarod: külön, **privát** repo.
- iCloud: ne családi megosztás alatti mappában legyen.
