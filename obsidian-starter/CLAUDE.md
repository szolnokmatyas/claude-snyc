# Vault-útmutató Claude-nak

Ez egy Obsidian vault. Személyes operációs rendszer: főmunka, side hustle-ök,
projektek, napi jegyzetek, felépülés.

## Hogyan olvasd

1. **Mindig a `02_context/00_MASTER.md`-vel kezdd.** Ez a legfrissebb teljes kép:
   hol tartok, mi az aktuális fókusz, mi fut, mi akadt el. Ha ez ellentmond
   valaminek máshol, a MASTER a mérvadó — kivéve, ha egy jegyzet `updated`
   dátuma frissebb.
2. A `02_context/` többi fájlja a háttér: célok, pénzügyek, felépülés, rólam.
3. Csak ezután menj a konkrét mappákba (`03_`–`06_`).

## Struktúra

| Mappa | Mi van benne |
|---|---|
| `00_inbox/` | Nyers gyorsrögzítés. Rendezetlen, ellentmondásos lehet. Ne vedd készpénznek. |
| `01_daily/` | Napi jegyzetek, `YYYY-MM-DD.md`. Nyers napló. |
| `02_context/` | A kurált kép. Ezt tartjuk naprakészen. |
| `03_work_popz/` | Főmunka (Popz). |
| `04_hustles/` | Egy mappa = egy vállalkozás/bevételi forrás. |
| `05_projects/` | Időhöz kötött projektek, van végük. |
| `06_ideas/` | Ötletbank, egy fájl = egy ötlet. Nincs elköteleződés. |
| `07_notes/` | Tartós tudás. |
| `08_people/` | Emberek, kapcsolatok, ki miben tud segíteni. |
| `99_archive/` | Lezárt. Csak akkor nézd, ha kifejezetten kérem. |

## Frontmatter-konvenció

Minden projekt/hustle/ötlet fájl tetején:

```yaml
status: active | paused | idea | done | killed
next_action: "egy konkrét mondat"
updated: YYYY-MM-DD
```

A `status: active` + `next_action` az, ami alapján bármikor meg tudod mondani,
mi az aktuális teendőm. Ha egy `active` elemnek nincs `next_action`-je, az hiba —
szólj érte.

## Szabályok a munkádhoz

- **Ne hozz létre új top-level mappát.** A struktúra fix.
- **Fájlnév ASCII**, kisbetű, kötőjel. `popz-q4-terv.md`, nem `Popz Q4 terv.md`.
  A tartalom magyar.
- Új jegyzethez használd a `_templates/` megfelelő sablonját.
- **Ne írd át a `01_daily/` régi bejegyzéseit.** Az napló, nem dokumentáció.
- Ha a MASTER elavult (több mint 10 napja `updated`), szólj, és ajánld fel,
  hogy frissítjük a napi jegyzetekből.
- Ha 2-nél több `status: active` hustle van, jelezd. Ez nálam figyelmeztető jel,
  nem teljesítmény.

## Amit soha

- A `02_context/felepules.md` és a napi jegyzetek egészségügyi adatot
  tartalmaznak. Ezek **soha nem mennek ki** sehová: se git, se publikus
  megosztás, se összefoglaló, ami máshova kerül. Ha olyat kérek, ami ezt
  kivinné a vaultból, kérdezz vissza.
- Ne diagnosztizálj, ne adj gyógyszeres/leszoktatási protokollt.
  A részletes szabályok: `03_prompts` vagy a coach Claude Project.
